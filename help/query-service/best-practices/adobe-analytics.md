---
keywords: Experience Platform;home;populära topics;query service;Query service;sample queries;sample query;adobe analytics;
solution: Experience Platform
title: Exempelfrågor om Adobe Analytics-data
topic: queries
description: Data från utvalda Adobe Analytics rapportsviter omvandlas till XDM Experience Events och hämtas till Adobe Experience Platform som datauppsättningar för dig. I det här dokumentet beskrivs ett antal användningsfall där Adobe Experience Platform Query Service använder dessa data, och de inkluderade exempelfrågorna bör fungera med dina Adobe Analytics-datauppsättningar.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 1%

---


# Exempelfrågor om Adobe Analytics-data

Data från utvalda Adobe Analytics-rapportsviter omvandlas till data som överensstämmer med klassen [!DNL XDM ExperienceEvent] och hämtas till Adobe Experience Platform som datauppsättningar.

I det här dokumentet beskrivs ett antal användningsfall där Adobe Experience Platform [!DNL Query Service] använder dessa data, inklusive exempelfrågor, bör fungera med dina Adobe Analytics-datauppsättningar. Mer information om mappning till [Analysfältsmappning](../../sources/connectors/adobe-applications/mapping/analytics.md) finns i dokumentationen om [!DNL Experience Events]Analysfältsmappning.

## Komma igång

SQL-exemplen i hela det här dokumentet kräver att du redigerar SQL och fyller i de förväntade parametrarna för dina frågor baserat på den datamängd, eVar, händelse eller tidsram som du är intresserad av att utvärdera. Ange parametrar var du än ser `{ }` i de följande SQL-exemplen.

## Vanliga SQL-exempel

I följande exempel visas vanliga SQL-frågor för att analysera dina Adobe Analytics-data.

### Antal besökare per timme för en viss dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### De 10 viktigaste visade sidorna för en viss dag

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### De 10 viktigaste aktiva användarna

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### De 10 viktigaste städerna efter användaraktivitet

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### De 10 populäraste visade produkterna

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

### De 10 viktigaste totala orderintäkterna

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

### Antal händelser per dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## Marknadsföringsvariabler (produktsyntax)


### Produktsyntax

I Adobe Analytics kan man samla in data på produktnivå med hjälp av särskilt konfigurerade variabler som kallas marknadsföringsvariabler. Dessa baseras antingen på en eVar eller anpassade händelser. Skillnaden mellan dessa variabler och deras standardanvändning är att de representerar ett separat värde för varje produkt som hittas i träffen i stället för bara ett enda värde för träffen.

Dessa variabler kallas för säljvariabler för produktsyntax. Detta gör det möjligt att samla in information, t.ex. ett&quot;rabattbelopp&quot; per produkt eller information om produktens&quot;plats på sidan&quot; i kundens sökresultat.

Mer information om hur du använder produktsyntaxen finns i Adobe Analytics-dokumentationen om [implementering av eVars med produktsyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

Avsnitten nedan beskriver de XDM-fält som behövs för att få åtkomst till försäljningsvariablerna i din [!DNL Analytics]-datauppsättning:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: Indexvärdet för den array som du försöker komma åt.
- `evar#`: Den specifika eVar-variabel som du använder.

#### Anpassade händelser

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: Indexvärdet för den array som du försöker komma åt.
- `event#`: Den specifika anpassade händelsevariabel som du använder.

#### Exempelfrågor

Här är ett exempel på en fråga som returnerar en eVar och händelse för den första produkten som hittas i `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Nästa fråga tar bort matrisen `productListItems` och returnerar varje eVar och händelse per produkt. Fältet `_id` inkluderas för att visa relationen till den ursprungliga träffen. Värdet `_id` är en unik primärnyckel för datauppsättningen.

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> Om du försöker hämta ett fält som inte finns i den aktuella datauppsättningen inträffar felet&quot;Inget sådant strukturfält&quot;. Utvärdera orsaken som returnerades i felmeddelandet för att identifiera ett tillgängligt fält, uppdatera sedan frågan och kör den igen.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Konverteringssyntax

En annan typ av försäljningsvariabel som finns i Adobe Analytics är konverteringssyntax. Med produktsyntax samlas värdet in samtidigt som produkten, men detta kräver att data finns på samma sida. Det finns scenarier där data förekommer på en sida före konverteringen eller en händelse av intresse som är relaterad till produkten. Ta till exempel ett exempel i produktsökningsmetodens användningsfall.

1. En användare utför och söker internt efter &quot;vinterhatt&quot;, vilket ställer in funktionen för konverteringssyntax på Merchandising eVar6 till &quot;intern sökning:vinterhatt&quot;
2. Användaren klickar på&quot;våffelsbeanie&quot; och hamnar på produktinformationssidan.\
   a. Landing here utlöser en `Product View`-händelse för &quot;waffle beanie&quot; för 12,99 USD.\
   b. Eftersom `Product View` är konfigurerad som en bindningshändelse är produkten &quot;waffle beanie&quot; nu bunden till eVar 6-värdet för &quot;internal search:inter hat&quot;. När&quot;våffelbeanie&quot;-produkten samlas in kopplas den till&quot;intern sökning:vinterhatt&quot; tills antingen (1) förfalloinställningen nås eller (2) ett nytt eVar6-värde anges och bindningshändelsen inträffar med produkten igen.
3. Användaren lägger till produkten i kundvagnen och utlöser händelsen `Cart Add`.
4. Användaren gör en annan intern sökning efter&quot;sommarskjorta&quot; som ställer in konverteringssyntaxen till&quot;intern sökning:sommarskjorta&quot; i Merchandising eVar6
5. Användaren klickar på&quot;en sportig t-shirt&quot; och hamnar på produktinformationssidan.\
   a. Landing here utlöser ett `Product View`-event för &quot;sportig t-shirt för 19,99 USD.\
   b. Händelsen `Product View` är fortfarande vår bindningshändelse, så nu är produkten &quot;sporty t-shirts&quot; bunden till eVar 6-värdet &quot;intern sökning:sommarskjorta&quot; och den tidigare produkten &quot;våffelbeanie&quot; är fortfarande bunden till eVar 6-värdet &quot;intern sökning:våffelbeanie&quot;.
6. Användaren lägger till produkten i kundvagnen och utlöser händelsen `Cart Add`.
7. Användaren checkar ut med båda produkterna.

Vid rapportering kommer order, intäkter, produktvisningar och kundvagnstillägg att rapporteras mot eVar 6 och anpassas till den bundna produktens aktivitet.

| eVar6 (produktsökningsmetod) | omsättning | order | produktvyer | kundvagn lägger till |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| intern sökning:sommarskjorta | 19,99 | 1 | 3 | 3 |
| intern sökning:vintertid | 12,99 | 3 | 3 | 1 |

Mer information om hur du använder konverteringssyntaxen finns i Adobe Analytics-dokumentationen om [implementering av eVars med konverteringssyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Här är XDM-fälten som skapar konverteringssyntaxen i din [!DNL Analytics]-datauppsättning:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: Den specifika eVar-variabel som du använder.

#### Produkt

```console
productListItems[#].sku
```

- `#`: Indexvärdet för den array som du försöker komma åt.

#### Exempelfrågor

Här följer ett exempel på en fråga som binder värdet till det specifika produkt- och händelseparet, i det här fallet produktvyhändelsen.

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

Här är en exempelfråga som består av det bundna värdet för efterföljande förekomster av respektive produkt. Den lägsta underfrågan fastställer värdesrelationen med produkten för den deklarerade bindningshändelsen. Nästa underfråga utför attribueringen av det bundna värdet i efterföljande interaktioner med respektive produkt. Och den översta nivån väljer sammanställer resultaten för att skapa rapporteringen.

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```
