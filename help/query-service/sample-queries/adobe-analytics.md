---
keywords: Experience Platform;home;populära topics;query service;Query service;sample queries;sample query;adobe analytics;
solution: Experience Platform
title: Exempelfrågor om Adobe Analytics-data
description: Data från utvalda Adobe Analytics-rapportsviter omvandlas till XDM ExperienceEvents och hämtas till Adobe Experience Platform som datauppsättningar. I det här dokumentet beskrivs ett antal användningsfall där frågetjänsten använder dessa data och innehåller exempelfrågor som är utformade för att fungera med dina Adobe Analytics-datauppsättningar.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Exempelfrågor om Adobe Analytics-data

Data från utvalda Adobe Analytics-rapportsviter omvandlas till data som överensstämmer med [!DNL XDM ExperienceEvent] och inkapslat i Adobe Experience Platform som datauppsättningar.

Det här dokumentet innehåller en översikt över ett antal användningsfall där Adobe Experience Platform [!DNL Query Service] använder dessa data. Läs dokumentationen om [Mappning av analysfält](../../sources/connectors/adobe-applications/mapping/analytics.md) för mer information om mappning till [!DNL Experience Events].

Se [dokumentation om användning av analysexempel](../use-cases/analytics-insights.md) om du vill lära dig hur du använder frågetjänsten för att skapa åtgärdbara insikter från inkapslade Adobe Analytics-data.

## Deduplicering

[!DNL Query Service] har stöd för datadeduplicering. Se [Datadeduplicering i [!DNL Query Service] dokumentation](../best-practices/deduplication.md) för information om hur nya värden genereras när frågan ställs [!DNL Experience Event] datauppsättningar.

## Marknadsföringsvariabler (produktsyntax)

I följande avsnitt finns XDM-fält och exempelfrågor som du kan använda för att få åtkomst till försäljningsvariablerna i [!DNL Analytics] datauppsättning.

### Produktsyntax

I Adobe Analytics kan man samla in data på produktnivå med hjälp av särskilt konfigurerade variabler som kallas marknadsföringsvariabler. Dessa baseras antingen på en eVar eller anpassade händelser. Skillnaden mellan de här variablerna och deras typiska användning är att de representerar ett separat värde för varje produkt som hittas i träffen i stället för bara ett enda värde för träffen.

Dessa variabler kallas för säljvariabler för produktsyntax. Detta gör det möjligt att samla in information, t.ex. ett&quot;rabattbelopp&quot; per produkt eller information om produktens&quot;plats på sidan&quot; i kundens sökresultat.

Mer information om hur du använder produktsyntaxen finns i Adobe Analytics-dokumentationen på [implementera eVars med produktsyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

Avsnitten nedan beskriver de XDM-fält som behövs för att få tillgång till varuvariablerna i [!DNL Analytics] datauppsättning:

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

Här är ett exempel på en fråga som returnerar en eVar och händelse för den första produkten som finns i `productListItems`.

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

Nästa fråga tar bort `productListItems` och returnerar varje eVar och händelse per produkt. The `_id` fältet inkluderas för att visa relationen till den ursprungliga träffen. The `_id` värdet är en unik primärnyckel för datauppsättningen.

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

En annan typ av försäljningsvariabel som finns i Adobe Analytics är konverteringssyntax. Med produktsyntax samlas värdet in samtidigt som produkten, men detta kräver att data finns på samma sida. Det finns scenarier där data förekommer på en sida före konverteringen eller den händelse av intresse som är relaterad till produkten. Ta till exempel ett exempel i produktsökningsmetodens användningsfall.

1. En användare utför och söker internt efter &quot;vinterhatt&quot;, vilket ställer in funktionen för konverteringssyntax på Merchandising eVar6 till &quot;intern sökning:vinterhatt&quot;
2. Användaren klickar på&quot;våffelsbeanie&quot; och hamnar på produktinformationssidan.\
   a. Landing here utlöser en `Product View` event för &quot;waffle beanie&quot; för 12,99 USD.\
   b. Sedan `Product View` är konfigurerad som en bindningshändelse, är produkten &quot;waffle beanie&quot; nu bunden till eVar6-värdet &quot;internal search:vinterhat&quot;. När&quot;våffelbeanie&quot;-produkten samlas in kopplas den till&quot;intern sökning:vinterhatt&quot; tills antingen (1) förfalloinställningen nås eller (2) ett nytt eVar6-värde anges och bindningshändelsen inträffar med produkten igen.
3. Användaren lägger till produkten i sin kundvagn, vilket ger `Cart Add` -händelse.
4. Användaren gör en annan intern sökning efter&quot;sommarskjorta&quot; som ställer in konverteringssyntaxen till&quot;intern sökning:sommarskjorta&quot; i Merchandising eVar6
5. Användaren klickar på&quot;en sportig t-shirt&quot; och hamnar på produktinformationssidan.\
   a. Landing here utlöser en `Product View` för &quot;sportskjorta för 19,99 dollar.\
   b. The `Product View` -händelsen är fortfarande vår bindningshändelse, så nu är produkten &quot;sporty t-shirts&quot; bunden till eVar 6-värdet av &quot;intern sökning:sommarskjorta&quot; och den tidigare produkten &quot;waffle beanie&quot; är fortfarande bunden till eVar 6-värdet &quot;intern sökning:waffle beanie&quot;.
6. Användaren lägger till produkten i sin kundvagn, vilket ger `Cart Add` -händelse.
7. Användaren checkar ut med båda produkterna.

Vid rapportering kommer order, intäkter, produktvisningar och kundvagnstillägg att rapporteras mot eVar 6 och anpassas till den bundna produktens aktivitet.

| eVar6 (produktsökningsmetod) | intäkt | order | produktvyer | kundvagn lägger till |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| intern sökning:sommarskjorta | 19.99 | 1 | 1 | 1 |
| intern sökning:vintertid | 12.99 | 1 | 1 | 1 |

Mer information om hur du använder konverteringssyntaxen finns i Adobe Analytics-dokumentationen på [implementera eVars med konverteringssyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Här är XDM-fälten som skapar konverteringssyntaxen i [!DNL Analytics] datauppsättning:

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
