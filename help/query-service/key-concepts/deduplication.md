---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Frågetjänst;datadeduplicering;deduplicering;
solution: Experience Platform
title: Datadeduplicering i frågetjänsten
type: Tutorial
description: Det här dokumentet innehåller exempel på delurval och fullständiga exempelfrågor för borttagning av dubbletter av tre vanliga användningsfall - Experience Events, purchase och metrics.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Datadeduplicering i [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] stöder datadeduplicering. Datadeduplicering kan utföras när det krävs att en hel rad tas bort från en beräkning eller att en viss uppsättning fält ignoreras eftersom endast en del av data i raden är dubblettinformation.

Borttagning av dubbletter innebär vanligtvis att funktionen `ROW_NUMBER()` används i ett fönster för ett ID (eller ett par ID:n) över ordnad tid, vilket returnerar ett nytt fält som representerar det antal gånger en dubblett har identifierats. Tiden representeras ofta av fältet [!DNL Experience Data Model] (XDM) `timestamp`.

När värdet för `ROW_NUMBER()` är `1` refererar det till den ursprungliga instansen. I allmänhet är det den instans som du vill använda. Detta görs oftast inuti en undermarkering där borttagningen av dubbletter görs på en högre nivå, `SELECT`, som att utföra en sammanställning.

Användningsfall vid borttagning av dubbletter kan antingen vara globala eller begränsade till ett enda användar- eller slutanvändar-ID inom `identityMap`.

I det här dokumentet beskrivs hur du utför borttagning av dubbletter för tre vanliga användningsområden: Experience Events, purchase och metrics.

Varje exempel innehåller omfattningen, fönsternyckeln, en översikt över dedupliceringsmetoden samt den fullständiga SQL-frågan.

## Experience Events {#experience-events}

Om Experience Events dupliceras kommer ni troligen att ignorera hela raden.

>[!CAUTION]
>
>Många datauppsättningar i [!DNL Experience Platform], inklusive de som har skapats av Adobe Analytics Data Connector, har redan borttagning av dubbletter på händelsenivå. Därför är det inte nödvändigt att återanvända den här nivån av borttagning av dubbletter, vilket kommer att göra frågan långsammare.
>
>Det är viktigt att förstå källan till datauppsättningarna och veta om borttagning av dubbletter på Experience-Event-nivå redan har tillämpats. För alla datauppsättningar som direktuppspelas (till exempel datauppsättningar från Adobe Target) måste du **använda borttagning av dubbletter på Experience-Event-nivå, eftersom dessa datakällor har minst en semantik.**

**Omfång:** Global

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

Om du har dubblerade inköp vill du förmodligen behålla merparten av raden [!DNL Experience Event], men ignorera de fält som är kopplade till köpet (till exempel måttet `commerce.orders`). Inköp innehåller ett särskilt fält för köp-ID, som är `commerce.order.purchaseID`.

Vi rekommenderar att du använder `purchaseID` i besökaromfånget, eftersom det är standardsemantiskt fält för köp-ID:n i XDM. Besökaromfånget rekommenderas för att ta bort dubbletter av inköpsdata eftersom frågan är snabbare än om det globala omfånget används och det är inte troligt att ett köp-ID dupliceras över flera besökar-ID:n.

**Omfång:** Besökare

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

>[!NOTE]
>
>I vissa fall där de ursprungliga Analytics-data har dubblerade inköps-ID:n för besökar-ID:n, kanske **måste** köra dubblettinventeringen av inköps-ID:n för alla besökare. Om det inte finns något inköps-ID kräver den här metoden att du inkluderar ett villkor som i stället använder händelse-ID för att frågan ska gå så snabbt som möjligt.

### Fullständigt exempel

I exemplet nedan används en villkorssats för att använda händelse-ID om det inte finns något köp-ID.

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

**Omfång:** Besökare

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

Det här dokumentet innehåller exempel på datadeduplicering och beskriver hur datadeduplicering ska utföras i Query Service. Mer information om hur du skriver frågor med hjälp av frågetjänsten finns i [handboken om skrivna frågor](../best-practices/writing-queries.md).
