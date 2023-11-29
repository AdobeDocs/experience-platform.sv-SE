---
keywords: Experience Platform;frågetjänst;frågetjänst;kapslade datastrukturer;kapslade data;förenkla;förenkla kapslade data;
title: Förenkla kapslade datastrukturer för användning med BI-verktyg
description: Det här dokumentet förklarar hur du förenklar XDM-scheman för alla tabeller och vyer under en session när du använder BI-verktyg från tredje part med Query Service.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Förenkla kapslade datastrukturer för användning med BI-verktyg från tredje part

Adobe Experience Platform Query Service stöder `FLATTEN` ställa in vid anslutning till en databas via BI-verktyg från tredje part. Den här funktionen förenklar kapslade datastrukturer i BI-verktyg från tredje part för att förbättra deras användbarhet och minska den arbetsbelastning som krävs för att hämta, analysera, omvandla och rapportera data.

Många BI-verktyg som [!DNL Tableau] och [!DNL Power BI] stöder inte kapslade datastrukturer. The `FLATTEN` inställning tar bort behovet av att skapa SQL-vyer ovanpå dina data för att tillhandahålla en platt version, eller för att använda frågetjänsten `CTAS` eller `INSERT INTO` jobb för att duplicera datauppsättningar till platta versioner när du använder ad hoc-scheman.

The `FLATTEN` inställning hämtar strukturen för varje bladfält till tabellens rot och ger fältet namn efter det ursprungliga namnutrymmet. Detta gör att du kan använda punktnotation för att matcha ett fält med dess XDM-sökväg (Experience Data Model) samtidigt som fältets kontext bevaras.

## Förutsättningar

Använda `FLATTEN` För inställningen krävs en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [XDM-system](../../xdm/home.md): En översikt på hög nivå över XDM och dess implementering i Experience Platform.

   * [Skapa ett ad hoc-schema](../../xdm/tutorials/ad-hoc.md): Ett XDM-schema med fält som bara namnges av en enda datauppsättning kallas för ett ad hoc-schema. Ad hoc-scheman används i olika arbetsflöden för dataöverföring för Experience Platform och för att skapa vissa typer av källanslutningar.

* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

* [Kapslade datastrukturer](./nested-data-structures.md): Det här dokumentet innehåller exempel på hur du skapar, bearbetar eller omformar datauppsättningar med komplexa datatyper, inklusive kapslade datastrukturer.

## Ansluta till en databas med FLATTEN-inställningen {#connect-with-flatten}

The `FLATTEN` När du anger förenklas kapslade datastrukturer till separata kolumner där attributnamnet blir det kolumnnamn som innehåller radvärdena. När du arbetar med data i BI-verktyg som inte har stöd för kapslade datastrukturer, förbättrar den här inställningen användbarheten för ad hoc-scheman och minskar den nödvändiga arbetsbelastningen.

Lägg till `FLATTEN` till databasnamnet. Mer information om hur du ansluter ett specifikt BI-verktyg finns i respektive dokumentation i [ansluta klienter till frågetjänsten - översikt](../clients/overview.md). Anslutningssträngen ska innehålla:

* Sandlådenamnet.
* Ett kolon följt av `all` eller ett specifikt datauppsättnings-ID, vy-ID eller databasnamn.
* Ett frågetecken (?) följt av `FLATTEN` nyckelord.

Indata ska ha följande format:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

En exempelanslutningssträng kan se ut så här:

```terminal
prod:all?FLATTEN
```

## Exempel {#example}

Det exempelschema som används i den här guiden använder standardfältgruppen [!UICONTROL Commerce Details], som använder `commerce` objektstruktur och `productListItems` array. Läs XDM-dokumentationen för [mer information om [!UICONTROL Commerce Details] fältgrupp](../../xdm/field-groups/event/commerce-details.md). En representation av schemastrukturen visas i bilden nedan.

![Ett schemadiagram över fältgruppen Commerce Details som innehåller `commerce` och `productListItems` strukturer.](../images/essential-concepts/commerce-details.png)

Om ditt BI-verktyg inte stöder kapslade datastrukturer kan det vara svårt att referera till kapslade fält om de innehåller serialiserade värden (till exempel `commerce` och `productListItems` i exempelschemat). Dessa värden kan visas som delar av en enda kodad `commerce` strängfält och är inte realistiskt oanvändbara.

Följande värden representerar `commerce.order.priceTotal` (3018.0) `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180), och `commerce.purchases.value`(1.0) i dåligt formaterade kapslade fält.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Genom att använda `FLATTEN` kan du komma åt separata fält i schemat eller hela avsnitt i den kapslade datastrukturen genom att använda punktnotation och deras ursprungliga sökvägsnamn. Ett exempel på det här formatet med `commerce` fältgruppen anges nedan.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

The `FLATTEN` -inställningen har vissa begränsningar när den hanterar andra datastrukturer. Fullständig information finns i [begränsningsavsnitt](#limitations).

### Använd citattecken för fält i frågor {#quotation-marks}

De förenklade rotfälten använder nu punktnotation för att matcha sina XDM-sökvägar. När de används i en fråga måste fälten omges av citattecken (&quot; &quot;).

I SQL-exemplet nedan visas det ursprungliga läget för den kapslade frågan:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

När du använder de förenklade datafälten skrivs frågan med punktnotation och omsluts av citattecken enligt nedan:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Begränsningar {#limitations}

The `FLATTEN` -inställningen förenklar för närvarande inte följande datastrukturer:

| Datastruktur | Begränsning |
|---|---|
| Arrayer | Använd ett explicit matrisindex eller `EXPLODE` -funktion för att komma åt arrayer. |
| Kartor | Använd strängnyckeln för att komma åt ett värde under en karta för att komma åt kartor. |

Om du vill lösa både mappnings- och matrisbegränsningar måste du använda BI-verktygen för SQL-redigering, som de avancerade alternativen -> SQL-satsen i Power BI.

BI-verktyg som rå SQL-redigering krävs för att lösa både mappnings- och matrisbegränsningar. Se guiden om hur man [använda avancerade alternativ för Power BI för att ange en anpassad SQL-fråga](../clients/power-bi.md#import-tables-using-custom-sql) i SQL-satsdelen.

## Nästa steg

I det här dokumentet beskrivs hur du förenklar kapslade datastrukturer för användning med BI-verktyg från tredje part. Om du inte redan har anslutit klienten kan du läsa [Översikt över klientanslutningen](../clients/overview.md) för en lista över tredjepartsklienter som stöds.
