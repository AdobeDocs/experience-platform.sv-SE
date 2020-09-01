---
keywords: Experience Platform;home;popular topics;query service;Query service;data deduplication;deduplication;
solution: Experience Platform
title: Datadeduplicering
topic: queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Datadeduplicering i [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] har stöd för datadeduplicering när det kan behövas att ta bort en hel rad från en beräkning eller ignorera en viss uppsättning fält eftersom endast en del av data i raden är en dubblett. I det vanliga mönstret för borttagning av dubbletter används funktionen i ett fönster för ett ID, eller ID-par, över den ordnade tiden (med hjälp av `ROW_NUMBER()` XDM- [!DNL Experience Data Model] `timestamp` fältet) för att returnera ett nytt fält som representerar det antal gånger en dubblett har identifierats. När det här värdet är `1`refererar det till den ursprungliga instansen, och i de flesta fall är det instansen som du vill använda, och ignorerar alla andra instanser. Detta görs oftast inuti en undermarkering där borttagningen av dubbletter görs på en högre nivå `SELECT` som att utföra en sammanställning.

## Användningsfall

Vissa användningsfall för borttagning av dubbletter är globala inom datumintervallet och vissa är begränsade till ett enda besökar- eller slutanvändar-ID inom `identityMap`.

Det här dokumentet innehåller exempel på delval och fullständig exempelfråga för borttagning av dubbletter av tre vanliga användningsområden:
- [ExperienceEvents](#experienceevents)
- [Inköp](#purchases)
- [Mätvärden](#metrics)

### ExperienceEvents {#experienceevents}

Om ExperienceEvents dupliceras vill du troligen ignorera hela raden.

>[!CAUTION]
>
>Många DataSets i [!DNL Experience Platform], inklusive de som har skapats av Adobe Analytics Data Connector, har redan borttagning av dubbletter på ExperienceEvent-nivå. Därför är det inte nödvändigt att återanvända den här nivån av borttagning av dubbletter, vilket kommer att göra frågan långsammare. Det är viktigt att förstå källan till dina DataSets och veta om borttagning av dubbletter på ExperienceEvent-nivå redan har tillämpats. För alla datauppsättningar som direktuppspelas (till exempel uppsättningar från Adobe Target) måste du använda borttagning på ExperienceEvent-nivå eftersom dessa datakällor har minst en semantik.

**Omfång:** Global

**Fönsternyckel:** id

#### Delmarkera

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### Fullständigt exempel

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

### Inköp {#purchases}

Om du har dubblerade inköp vill du förmodligen behålla de flesta av ExperienceEvent-raderna, men ignorera de fält som är kopplade till inköpet (till exempel `commerce.orders` måtten). För inköp finns det ett särskilt fält för inköps-ID. Det här fältet är `commerce.order.purchaseID`.

**Omfång:** Besökare

**Fönsternyckel:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

#### Delmarkera

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

#### Fullständigt exempel

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

### Mätvärden {#metrics}

Om du har ett mätvärde som använder det valfria unika ID:t och en dubblett av det ID:t visas, vill du troligtvis ignorera det måttvärdet och behålla resten av ExperienceEvent. I XDM använder nästan alla mätvärden den datatyp som innehåller ett valfritt `Measure` `id` fält som du kan använda för borttagning av dubbletter.

**Omfång:** Besökare

**Fönsternyckel:** identityMap[$NAMESPACE].id och id för måttobjektet

#### Delmarkera

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

#### Fullständigt exempel

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```
