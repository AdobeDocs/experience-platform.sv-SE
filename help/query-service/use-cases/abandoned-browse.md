---
keywords: Experience Platform;frågetjänst;frågetjänst;fråga
title: Exempel på användningsfall för Adobe Experience Platform Query Service
description: Ett heltäckande exempel som demonstrerar mångsidigheten och fördelarna med Adobe Experience Platform Query Service.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Exempel på användningsfall för Adobe Experience Platform [!DNL Query Service]

Det här dokumentet och den medföljande videopresentationen ger ett avancerat arbetsflöde som visar hur Adobe Experience Platform [!DNL Query Service] kan hjälpa din organisations strategiska affärsinsikter. I den här guiden visas följande viktiga begrepp:

* Den centrala vikten av databearbetning för att maximera Adobe Experience Platform potential.
* Olika sätt att bygga frågan baserat på din befintliga dataarkitektur.
* Säkerställ den datakvalitet som uppfyller era behov och metoder för att minska eventuella brister.
* Processen för att schemalägga en fråga att köras med en fast frekvens för användning längre fram i segmenteringen och destinationer för personalisering.
* Det är enkelt för marknadsförare att inkludera härledda datauppsättningar i sina målgrupper med kraften hos [!DNL Query Service].

## Mål {#objectives}

Den här arbetsflödesdemonstrationen bygger på flera Adobe Experience Platform-tjänster. Om du vill följa med i utvecklingen rekommenderar vi att du har en bra förståelse för följande funktioner och tjänster:

* [Grunderna i XDM-schemakompositionen (Experience Data Model)](../../xdm/schema/composition.md)
* Så här [skapar du datauppsättningar och importerar data](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* Så här [importerar du data med Adobe Analytics-källanslutningen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)
* [Segmentering](../../segmentation/home.md)
* [Mål](../../destinations/home.md)

Exemplet på bläddringsavhopp fokuserar på att använda Adobe [!DNL Analytics]-data för att skapa en viss åtgärdbar målgrupp. Målgruppen är att inkludera alla kunder som har besökt webbplatsen de senaste fyra dagarna men inte har gjort något inköp. Varje profil i målgruppen målgruppsanpassas sedan med den mest prisvärda SKU som följer av kundens beteendemönster.

Själva frågan är mycket preskriptiv och innehåller bara data som uppfyller användningsfallskriterierna för segmentdefinitionen. Detta förbättrar prestanda genom att minimera mängden [!DNL Analytics] data som bearbetas. Den beställer också data efter pris från högsta till lägsta och väljer den SKU som användaren valde till det högsta priset.

Frågan som används i presentationen visas nedan:

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] exempel på bläddring efter övergivna med hjälp av Adobe Analytics {#video-example}

Videopresentationen nedan ger ett helhetsbaserat exempel på hur dina Experience Platform-data kan användas i verkligheten med fokus på [!DNL Query Service]- och Adobe-analyser-integreringar.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Fördelar med [!DNL Query Service] {#benefits}

Funktionerna från [!DNL Query Service] har många syften. Ni kan använda den för att få plats med komplex logik för segmentering, för att beräkna olika anpassade attribut för användning längre fram i kedjan eller för att avsevärt förenkla hur ni bygger ut era målgrupper.

Med [!DNL Query Service] kan du inkludera begränsningar i dina frågor för att förenkla målgruppsbyggandeprocessen. Detta förbättrar datakvaliteten genom att säkerställa att rätt data kvalificeras för era målgrupper. Att hålla kvaliteten på frågan ger en korrekt målgrupp och bidrar till tillförlitlighet i datan. Du kan också spara målgruppen genom att skapa scheman och anpassade tabeller baserade på attribut som härletts från din fråga. En anpassad tabell kan aktiveras för profil och du kan använda dessa datapunkter för segmentering och personalisering. Den här funktionen hjälper marknadsförare som vill skapa en tydlig målgrupp av människor.

Genom att ta med logik i frågan som uppfyller alla återkommande eller statiska villkor, extraherar [!DNL Query Service] även bördan av avancerad segmentering.

Adobe Experience Platform tillhandahåller ett datalager och de verktyg som krävs för att aktivera data på ett effektivt och tillförlitligt sätt. Genom att lagra data i Experience Platform kan ni härleda attribut samtidigt som ni kör andra processer och eliminerar behovet av att exportera data till verktyg från tredje part för manipulering och bearbetning. Sådana allmänna omkostnader kan i hög grad påverka en projekttidslinje när man arbetar med hundratals attribut eller kampanjer. Detta ger marknadsförarna en enda plats där de kan få tillgång till sina data och bygga ut kampanjer samt ett mycket dynamiskt sätt att segmentera och personalisera sina meddelanden.

## Nästa steg

Genom att läsa det här dokumentet bör du nu förstå hur [!DNL Query Service] påverkar inte bara kvaliteten på dina data och hur lätt det är att segmentera, utan även hur viktig den är i din dataarkitektur för hela arbetsflödet från början till slut. Mer tillämpliga SQL-exempel som använder Adobe Analytics med [!DNL Query Service] finns i [Adobe Analytics marknadsföringsvariabler använder case](./merchandising-variables.md).

Andra dokument som demonstrerar fördelarna med [!DNL Query Service] för din organisations strategiska affärsinsikter är exemplet med [startsfiltreringsanvändning](./bot-filtering.md).

De här dokumenten kan även hjälpa dig att förstå [!DNL Query Service]-funktioner:

* [Vägledning för frågekörning](../best-practices/writing-queries.md)
* [Vägledning för dataresursorganisation](../best-practices/organize-data-assets.md).


