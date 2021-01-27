---
keywords: Experience Platform;home;popular topics;query service;Query service;data deduplication;deduplication;
solution: Experience Platform
title: Datadeduplicering
topic: queries
type: Tutorial
description: Det här dokumentet innehåller exempel på delurval och fullständiga exempelfrågor för borttagning av dubbletter av tre vanliga användningsfall - Experience Events, purchase och metrics.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# Datadeduplicering i [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] stöder datadeduplicering. Datadeduplicering kan utföras när det krävs att en hel rad tas bort från en beräkning eller att en viss uppsättning fält ignoreras eftersom endast en del av data i raden är dubblettinformation.

Deduplicering innebär vanligtvis att du använder funktionen `ROW_NUMBER()` i ett fönster för ett ID (eller ett par ID:n) över ordnad tid, vilket returnerar ett nytt fält som representerar det antal gånger en dubblett har identifierats. Tiden representeras ofta av fältet [!DNL Experience Data Model] (XDM) `timestamp`.

När värdet för `ROW_NUMBER()` är `1` refererar det till den ursprungliga instansen. I allmänhet är det den instans som du vill använda. Detta görs oftast inuti en undermarkering där borttagningen av dubbletter görs på en högre nivå `SELECT`, som att utföra en sammanställd räkning.

Användningsfall vid borttagning av dubbletter kan antingen vara globala eller begränsade till ett enda användar- eller slutanvändar-ID inom `identityMap`.

I det här dokumentet beskrivs hur du utför borttagning av dubbletter för tre vanliga användningsområden: Upplev händelser, köp och mätvärden.

Varje exempel innehåller omfattningen, fönsternyckeln, en översikt över dedupliceringsmetoden samt den fullständiga SQL-frågan.

## Experience Events {#experience-events}

Om Experience Events dupliceras kommer ni troligen att ignorera hela raden.

>[!CAUTION]
>
>Många datauppsättningar i [!DNL Experience Platform], inklusive de som har skapats av Adobe Analytics Data Connector, har redan borttagning av dubbletter på händelsenivå. Därför är det inte nödvändigt att återanvända den här nivån av borttagning av dubbletter, vilket kommer att göra frågan långsammare.
>
>Det är viktigt att förstå källan till datauppsättningarna och veta om borttagning av dubbletter på Experience-Event-nivå redan har tillämpats. För alla datauppsättningar som direktuppspelas (till exempel datauppsättningar från Adobe Target) måste du **använda borttagning av dubbletter på Experience-Event-nivå, eftersom dessa datakällor har minst en semantik.**

**omfång:** globalt

**Fönsternyckel:** `id`

### Exempel på borttagning av dubbletter

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Fullständigt exempel

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

## Inköp {#purchases}

Om du har dubblerade inköp vill du förmodligen behålla de flesta av Experience Event-raderna, men ignorera de fält som är kopplade till köpet (till exempel `commerce.orders`-måttet). Inköp innehåller ett särskilt fält för köp-ID, som är `commerce.order.purchaseID`.

**omfång:** Besökare

**Fönsternyckel:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### Exempel på borttagning av dubbletter

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

### Fullständigt exempel

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

## Mätvärden {#metrics}

Om du har ett mätvärde som använder det valfria unika ID:t och en dubblett av det ID:t visas, vill du troligtvis ignorera det måttvärdet och behålla resten av Experience Event.

I XDM använder nästan alla mått datatypen `Measure` som innehåller ett valfritt `id`-fält som du kan använda för borttagning av dubbletter.

**omfång:** Besökare

**Fönsternyckel:** identityMap[$NAMESPACE].id och ID för måttobjektet

### Exempel på borttagning av dubbletter

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

### Fullständigt exempel

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

## Nästa steg

I det här dokumentet beskrivs hur du utför borttagning av datadubbletter inom frågetjänsten samt exempel på borttagning av datadubbletter. Mer information om hur du skriver frågor med hjälp av frågetjänsten finns i [handboken om att skriva frågor](./writing-queries.md).