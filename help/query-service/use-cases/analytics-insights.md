---
title: 'Analysinsikter för webb- och mobilinteraktioner '
description: I det här dokumentet beskrivs hur du använder frågetjänsten för att skapa åtgärdbara insikter från inkapslade Adobe Analytics-data.
source-git-commit: cdceba9caf035831f4c376edf34356f666b79aa8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Analysinsikter för interaktion via webben och mobiler

Med Adobe Experience Platform kan ni importera data från Adobe Analytics rapporteringsprogram med hjälp av XDM-fält (Experience Data Model) för att fylla i datauppsättningar. Frågetjänsten kan sedan använda dessa analysdata genom att köra SQL-frågor för att generera värdefulla insikter från en användares beteende över de digitala plattformarna.

Det här dokumentet innehåller ett antal exempel på SQL-frågor som visar vanliga användningsfall när du skapar insikter från webb- och mobilanalysdata.

Se [Dokumentation för fältmappningar i analyser](../../sources/connectors/adobe-applications/mapping/analytics.md) för mer information om inhämtning och mappning av analysdata.

## Komma igång

För vart och ett av följande användningsfall anges ett parametriserat SQL-frågeexempel som en mall som du kan anpassa. Ange parametrar var du än ser `{ }` i SQL-exemplen för den datauppsättning, eVar, händelse eller tidsram som du är intresserad av att utvärdera.

## Mål

I följande exempel visas SQL-frågor för vanliga användningsområden för att analysera dina Adobe Analytics-data.

### Generera besökarantal för varje timme på en given dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Identifiera de 10 mest visade sidorna på en viss dag

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### Identifiera de 10 mest aktiva användarna

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Identifiera de 10 mest önskade städerna baserat på användaraktivitet

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Identifiera de 10 mest visade produkterna

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU,
              commerce.productviews.value   AS Product_Views
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL)
GROUP BY Product_SKU
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Identifiera de tio största orderintäkterna

```sql
SELECT Purchase_ID,
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID,
               Explode(productlistitems)   AS Product_Items
        FROM   {TARGET_TABLE}
        WHERE  commerce.`order`.purchaseid IS NOT NULL
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID
ORDER BY total_order_revenue DESC
LIMIT  10;
```
