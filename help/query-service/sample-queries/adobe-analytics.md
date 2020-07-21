---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exempelfrågor
topic: queries
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---


# Exempelfrågor om Adobe Analytics-data

Data från utvalda rapportsviter från Adobe Analytics omvandlas till XDM [!DNL ExperienceEvents] och hämtas till Adobe Experience Platform som datauppsättningar åt dig. I det här dokumentet beskrivs ett antal användningsfall där Adobe Experience Platform använder dessa data och där de inkluderade exempelfrågorna ska fungera med dina Adobe Analytics-datauppsättningar. [!DNL Query Service] Mer information om mappning till XDM finns i dokumentationen [för fältmappning i](../../sources/connectors/adobe-applications/mapping/analytics.md) Analytics [!DNL ExperienceEvents].

## Komma igång

SQL-exemplen i hela det här dokumentet kräver att du redigerar SQL och fyller i de förväntade parametrarna för dina frågor baserat på den datamängd, eVar, händelse eller tidsram som du är intresserad av att utvärdera. Ange parametrar var du än ser `{ }` i de följande SQL-exemplen.

## Vanliga SQL-exempel

### Antal besökare per timme för en viss dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

### De 10 viktigaste visade sidorna för en viss dag

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### De 10 viktigaste aktiva användarna

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### De 10 viktigaste städerna efter användaraktivitet

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
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
       FROM   {target_table}
       WHERE  _acp_year = {target_year}
              AND _acp_month = {target_month}
              AND _acp_day = {target_day}
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
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
               AND _acp_year = {target_year} 
               AND _acp_month = {target_month}  
               AND _acp_day = {target_day}) 
GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Antal händelser per dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND _acp_year = {target_year} 
        AND _acp_month = {target_month}  
        AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

## Marknadsföringsvariabler (produktsyntax)

I Adobe Analytics kan man samla in data på produktnivå med hjälp av särskilt konfigurerade variabler som kallas&quot;Merchandising Variables&quot;. Dessa baseras antingen på en eVar- eller anpassad händelse. Skillnaden mellan dessa variabler och deras standardanvändning är att de representerar ett separat värde för varje produkt som hittas i träffen i stället för bara ett enda värde för träffen. Dessa variabler kallas för produktsyntaxvariabler. Detta gör det möjligt att samla in information som&quot;rabattbelopp&quot; per produkt eller information om produktens&quot;plats på sidan&quot; i kundens sökresultat.

Här är XDM-fälten för att komma åt de variabler som ingår i din [!DNL Analytics] datauppsättning:

### eVars

```
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

Där `[#]` är ett arrayindex och `evar#` är den specifika eVar-variabeln.

### Anpassade händelser

```
productListItems[#]._experience.analytics.event1to100.event#.value
```

Där `[#]` är ett arrayindex och `event#` är den specifika anpassade händelsevariabeln.

### Exempelfrågor

Här är ett exempel på en fråga som returnerar en eVar och händelse för den första produkten som hittas i `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Nästa fråga &#39;exploderar&#39; `productListItems` och returnerar varje eVar- och -händelse som handlar per produkt. Fältet `_id` inkluderas för att visa relationen till den ursprungliga träffen. Värdet `_id` är en unik primärnyckel i [!DNL ExperienceEvent] datauppsättningen.

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
  WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### Vanligt fel vid implementering av exempelfrågor

Felet &quot;Inget sådant strukturfält&quot; påträffas när du försöker hämta ett fält som inte finns i den aktuella datauppsättningen. Utvärdera orsaken som returnerades i felmeddelandet för att identifiera ett tillgängligt fält och uppdatera sedan frågan och kör den igen.

```
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## Marknadsföringsvariabler (konverteringssyntax)

En annan typ av en Merchandising-variabel som finns i Adobe Analytics är Conversion Syntax. Med produktsyntax samlas värdet in samtidigt som produkten, men detta kräver att data finns på samma sida. Det finns scenarier där data förekommer på en sida före konverteringen eller den händelse av intresse som är relaterad till produkten. Ta till exempel ett exempel till exempel ett exempel på hur rapportmetoden för produktsökning används.

1. En användare utför och söker internt efter &quot;vinterhatt&quot;, vilket anger att Merchandising eVar6 har aktiverat för konverteringssyntaxen till &quot;intern sökning:vinterhatt&quot;
2. Användaren klickar på&quot;våffelsbeanie&quot; och hamnar på produktinformationssidan.\
   a. Landing here utlöser en `Product View` händelse för &quot;waffle beanie&quot; för 12,99 dollar.\
   b. Eftersom produkten `Product View` är konfigurerad som en bindningshändelse är den nu bunden till eVar6-värdet för&quot;intern sökning:vinterhatt&quot;. När&quot;våffelbeanie&quot;-produkten samlas in kopplas den till&quot;intern sökning:vinterhatt&quot; tills antingen (1) förfalloinställningen nås eller (2) ett nytt eVar6-värde anges och bindningshändelsen inträffar med produkten igen.
3. Användaren lägger till produkten i kundvagnen och startar `Cart Add` händelsen.
4. Användaren gör en annan intern sökning efter&quot;sommarskjorta&quot; som ställer in funktionen för konverteringssyntax för Merchandising eVar6 till&quot;intern sökning:sommarskjorta&quot;
5. Användaren klickar på&quot;en sportig t-shirt&quot; och hamnar på produktinformationssidan.\
   a. Landing here utlöser ett `Product View` event för &quot;sportskjorta&quot; för 19,99 dollar.\
   b. Evenemanget är fortfarande vår bindningshändelse, så nu är produkten &quot;sporty t-shirts&quot; bunden till eVar6-värdet för &quot;intern sökning:sommarskjorta&quot; och den tidigare produkten &quot;waffle beanie&quot; är fortfarande bunden till eVar6-värdet &quot;intern sökning:waffle beanie&quot;. `Product View`
6. Användaren lägger till produkten i kundvagnen och startar `Cart Add` händelsen.
7. Användaren checkar ut med båda produkterna.

Vid rapporteringen kommer order, intäkter, produktvisningar och kundvagnstillägg att kunna rapporteras mot eVar6 och anpassas till den bundna produktens aktivitet.

| eVar6 (produktsökningsmetod) | omsättning | order | produktvyer | kundvagn lägger till |
|---|---|---|---|---|
| intern sökning:sommarskjorta | 19.99 | 1 | 1 | 1 |
| intern sökning:vintertid | 12.99 | 1 | 1 | 1 |

Här är XDM-fälten som skapar konverteringssyntaxen i din [!DNL Analytics] datauppsättning:

### eVars

```
_experience.analytics.customDimensions.evars.evar#
```

Var `evar#` är den specifika eVar-variabeln.

### Produkt

```
productListItems[#].sku
```

Där `[#]` är ett matrisindex.

### Exempelfrågor

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
