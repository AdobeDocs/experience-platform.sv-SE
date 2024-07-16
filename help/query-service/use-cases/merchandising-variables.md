---
title: Returnera och använda variabler från analysdata
description: Lär dig hur du tillhandahåller XDM-fält och exempelfrågor för att få tillgång till försäljningsvariablerna i era Analytics-datauppsättningar.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 0%

---

# Returnera och använda försäljningsvariabler från analysdata

Använd frågetjänsten för att hantera data som hämtas från Adobe Analytics till Adobe Experience Platform som datauppsättningar. I följande avsnitt finns exempelfrågor som du kan använda för att få tillgång till försäljningsvariablerna i dina Analytics-datauppsättningar. Mer information om [hur du importerar och mappar Adobe Analytics-data](../../sources/connectors/adobe-applications/mapping/analytics.md) via Analytics-källan finns i dokumentationen

## Marknadsföringsvariabler {#merchandising-variables}

Merchandising-variabler kan följa på en av två syntaxer:

* **Produktsyntax**: Associerar eVarna med en produkt. 
* **Konverteringsvariabelsyntax**: Associerar eVarna med en produkt endast om en bindningshändelse inträffar. Du kan välja händelser som fungerar som bindningshändelser.

## Produktsyntax {#product-syntax}

I Adobe Analytics kan man samla in data på produktnivå med hjälp av särskilt konfigurerade variabler som kallas marknadsföringsvariabler. Dessa baseras antingen på en eVar eller anpassade händelser. Skillnaden mellan de här variablerna och deras typiska användning är att de representerar ett separat värde för varje produkt som hittas i träffen i stället för bara ett enda värde för träffen.

Dessa variabler kallas för säljvariabler för produktsyntax. Detta gör det möjligt att samla in information, t.ex. ett&quot;rabattbelopp&quot; per produkt eller information om produktens&quot;plats på sidan&quot; i kundens sökresultat.

Mer information om hur du använder produktsyntaxen finns i Adobe Analytics-dokumentationen om [implementering av eVars med produktsyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

Avsnitten nedan beskriver de XDM-fält som behövs för att få åtkomst till försäljningsvariablerna i din [!DNL Analytics]-datauppsättning:

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: Indexvärdet för arrayen som du försöker komma åt.
* `evar#`: Den specifika eVar-variabel som du använder.

### Anpassade händelser

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: Indexvärdet för arrayen som du försöker komma åt.
* `event#`: Den specifika anpassade händelsevariabeln som du använder.

## Användningsexempel för produktsyntax {#product-use-cases}

Följande användningsexempel fokuserar på att returnera en eVar från arrayen `productListItems` med hjälp av SQL.

### Returnera eVar och evenemang för försäljning

Frågan nedan returnerar en eVar och händelse för försäljning för den första produkten som hittas i arrayen `productListItems`.

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

### Utvidga arrayen productListItems och returnera eVar och händelse för varje produkt.

Nästa fråga tar bort arrayen `productListItems` och returnerar varje eVar och händelse för försäljning per produkt. Fältet `_id` inkluderas för att visa relationen till den ursprungliga träffen. Värdet `_id` är en unik primärnyckel för datauppsättningen.

>[!NOTE]
>
>Funktionen explodera delar upp elementen i en array i flera rader. Det exkluderar null-värden.

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
> Om du försöker hämta ett fält som inte finns i den aktuella datauppsättningen inträffar felet&quot;Inget sådant strukturfält&quot;. Utvärdera orsaken som returnerades i felmeddelandet för att identifiera ett tillgängligt fält, uppdatera frågan och kör den igen.
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Syntax för konverteringsvariabel {#conversion-variable-syntax}

En annan typ av försäljningsvariabel som finns i Adobe Analytics är konverteringsvariabelsyntax. Syntax för konverteringsvariabel används när eVarna inte är tillgänglig för att anges i variabeln products. Det här scenariot innebär vanligtvis att sidan inte har något sammanhang för försäljningskanalen eller sökmetoden. I dessa fall bör du ange variabeln för försäljning innan användaren kommer till produktsidan, och värdet kvarstår tills bindningshändelsen inträffar.

Scenariot nedan visar till exempel hur de data som krävs kan finnas på en sida innan konverteringen eller händelsen som är relaterad till produkten inträffar.

1. En användare gör en intern sökning efter &quot;vinterhatt&quot; som anger att eVar6 kan köpas med konverteringssyntaxen till &quot;intern sökning:vinterhatt&quot;.
2. Användaren klickar på&quot;våffelsbeanie&quot; och hamnar på produktinformationssidan.\
   a. Landing here utlöser en `Product View`-händelse för &quot;waffle beanie&quot; för 12,99 USD.\
   b. Eftersom `Product View` är konfigurerad som en bindningshändelse är produkten &quot;våffle beanie&quot; nu bunden till eVar6-värdet för &quot;intern sökning:vinterhatt&quot;. När en produkt med&quot;våfflbeanie&quot; samlas in är den kopplad till&quot;intern sökning:vinterhatt&quot;. Detta inträffar antingen tills eVarnas förfalloinställning har nåtts eller tills ett nytt eVar6-värde har angetts och bindningshändelsen inträffar med produkten igen.
3. Användaren lägger till produkten i sin kundvagn och utlöser händelsen `Cart Add`.
4. Användaren gör en annan intern sökning efter&quot;sommarskjorta&quot; som ställer in konverteringssyntaxen som möjliggör försäljning av eVar6 till&quot;intern sökning:sommarskjorta&quot;.
5. Användaren väljer &quot;sportskjorta&quot; och hamnar på produktinformationssidan.\
   a. Landing here utlöser ett `Product View`-event för &quot;sportig t-shirt för 19,99 USD.\
   b. Eftersom händelsen `Product View` är bindningshändelsen är produkten &quot;sportskjorta&quot; nu bunden till eVar6-värdet för &quot;intern sökning:sommarskjorta&quot;. Den tidigare produkten &quot;waffle beanie&quot; är fortfarande bunden till eVar6-värdet &quot;internal search:waffle beanie&quot;.
6. Användaren lägger till produkten i sin kundvagn och utlöser händelsen `Cart Add`.
7. Användaren checkar ut med båda produkterna.

Vid rapporteringen kan order, intäkter, produktvisningar och kundvagnstillägg rapporteras mot eVar6 och anpassas till den inbundna produktens aktivitet.

| eVar6 (produktsökningsmetod) | intäkt | order | produktvyer | kundvagn lägger till |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| intern sökning:sommarskjorta | 19,99 | 1 | 1 | 1 |
| intern sökning:vintertid | 12,99 | 1 | 1 | 1 |

Mer information om hur du använder syntaxen för konverteringsvariabler finns i Adobe Analytics-dokumentationen om [implementering av eVars med syntax för konverteringsvariabler](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

Nedan visas XDM-fälten som skapar konverteringsvariabelsyntaxen i din [!DNL Analytics]-datauppsättning:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: Den specifika eVar-variabel som du använder.

#### Produkt

```console
productListItems[#].sku
```

* `#`: Indexvärdet för arrayen som du försöker komma åt.

## Konverteringsvariabeln använder fall {#conversion-variable-use-cases}

Användningsexemplen nedan återspeglar scenarier som kräver syntax för konverteringsvariabel.

### Bind värdet till det specifika produkt- och händelseparet

Frågan nedan binder värdet till det specifika produkt- och händelseparet. I det här exemplet är värdet bundet till produktvyhändelsen.

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

### Behåll det bundna värdet för efterföljande förekomster av respektive produkt

Exempelfrågan nedan består av det bundna värdet till efterföljande förekomster av respektive produkt. Den lägsta underfrågan fastställer värdets relation till produkten i den deklarerade bindningshändelsen. Nästa underfråga utför attribueringen av det bundna värdet i efterföljande interaktioner med respektive produkt. SELECT på den översta nivån aggregerar resultaten för att skapa rapporteringen.

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

## Nästa steg

Genom att läsa det här dokumentet bör du få en bättre förståelse för hur du returnerar en eVar med produktsyntax och binder ett värde till en viss produkt med syntaxen för konverteringsvariabler.

Om du inte redan har gjort det bör du läsa [Analysinsikter för interaktionsdokumentation för webb och mobiler](./analytics-insights.md) härnäst. Här finns exempel på vanliga användningsområden och visar hur man använder frågetjänsten för att skapa åtgärdbara insikter från Adobe Analytics-data för webben och mobiler.
