---
keywords: mål;mål;måltyper
title: Måltyper och -kategorier
description: Läs mer om de olika typerna och kategorierna av destinationer i Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 606038116391e75ba4ffc36bab11757f963a8346
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Måltyper och -kategorier

Läs den här sidan om du vill veta mer om de olika typerna och kategorierna av Adobe Experience Platform-mål.

## Måltyper {#destination-types}

I Adobe Experience Platform skiljer vi mellan två måltyper - anslutningar och tillägg. Det finns två typer av anslutningsmål: Profilexportmål och Segmentexportmål.

![Typer av destinationer](./assets/destination-types/types-of-destinations.png)

## Anslutningar {#connections}

**[!UICONTROL Profile Export]**, **[!UICONTROL Streaming Segment Export]** och **[!DNL Edge Personalization]** mål i Adobe Experience Platform hämta händelsedata, kombinera dem med andra datakällor för att skapa [Kundprofil i realtid](../profile/home.md), tillämpa segmentering och exportera segment och kvalificerade profiler till destinationer.

## Profilexportdestinationer {#profile-export}

Profilexportdestinationer tar emot rådata, ofta med e-postadress som primärnyckel. Experience Platform har för närvarande stöd för två typer av profilexportdestinationer:

* [Exportmål för direktuppspelningsprofil (företagsmål)](#streaming-profile-export)
* [Batchmål (filbaserade)](#file-based)

### Exportmål för direktuppspelningsprofil (företagsmål) {#streaming-profile-export}

>[!IMPORTANT]
>
>Företagsmål, eller exportmål för direktuppspelningsprofiler, är tillgängliga för [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) endast kunder.

Använd dataanslutningarna för företag för att leverera Adobe Real-time Customer Data Platform-profiler i nära realtid till interna system eller till andra tredjepartssystem för datasynkronisering, analys och fler användningsfall för profilberikning.

Dessa mål tar emot segment- och profildata som dataströmmar i Experience Platform.

Företagets mål är:

* [HTTP API-mål](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Batchmål (filbaserade) {#file-based}

Filbaserade mål tar emot `.csv` filer som innehåller profiler och/eller attribut. [Amazon S3](catalog/cloud-storage/amazon-s3.md) är ett exempel på ett mål där du kan exportera filer som innehåller profilexporter.

## Målgrupper för direktuppspelad segmentexport {#streaming-destinations}

Segmentexportdestinationer tar emot data från Experience Platform segment. Dessa mål använder segment-ID eller användar-ID. Annonsering och sociala medier som [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), eller [Facebook](catalog/social/facebook.md) är exempel på sådana destinationer.

## Destinationer för kantanpassning {#edge-personalization-destinations}

De främsta målsättningarna för personalisering i Experience Platform är bland annat [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) och [Anpassat personaliseringsmål](/help/destinations/catalog/personalization/custom-personalization.md). Genom att använda dessa destinationer kan ni möjliggöra användning av samma sida och nästa sida för personalisering för era kunder.

Läs mer om hur [konfigurera anpassningsmål för personalisering på samma sida och nästa sida](/help/destinations/ui/configure-personalization-destinations.md).

## Profilexport och segmentexportdestinationer - videoöversikt {#video}

I videon nedan beskrivs de två typerna av destinationer:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## (Beta) Exportmål för datauppsättning {#dataset-export-destinations}

Vissa molnlagringsmål i målkatalogen stöder datauppsättningsexporter. Använd dessa mål för att exportera rådatauppsättningar till molnlagringsplatser.

Läs mer om hur [exportera datamängder](/help/destinations/ui/export-datasets.md).

## Tillägg {#extensions}

Plattformen utnyttjar tagghanteringens kraft och flexibilitet, vilket gör att du kan konfigurera taggtillägg i användargränssnittet.

>[!TIP]
>
>Detaljerad information om taggtillägg, inklusive användningsexempel och hur du hittar dem i gränssnittet finns i [taggtillägg - översikt](./catalog/launch-extensions/overview.md).

Med taggtillägg vidarebefordras råa händelsedata till flera typer av mål. Tänk på tillägg som **Vidarebefordran av händelser** typ av mål. Detta är en enklare typ av integrering med målplattformar, som bara vidarebefordrar råhändelsedata. Exempel på sådana är [Tillägg för personalisering med Gainsight](./catalog/personalization/gainsight.md) eller [Bekräfta rösten för kundtillägget](./catalog/voice/confirmit-digital-feedback.md).

![Märkordstillägg jämfört med andra mål](./assets/common/launch-and-other-destinations.png)

## När anslutningar och tillägg ska användas {#when-to-use}

Som marknadsförare kan du använda en kombination av anslutningar och tillägg för att hantera dina användningsfall.

Anslutningar är användbara när det är nödvändigt att utnyttja en fullständig centraliserad kundprofil eller ett kundsegment för aktivering. Använd till exempel anslutningar om du kopplar beteendedata från ett analyssystem med överförda CRM-data för att kvalificera en användare för ett visst segment innan du levererar ett anpassat meddelande till användaren.

Tillägg är användbara när händelsedata används för att utlösa en åtgärd eller för att utföra segmentering i en extern miljö. Om beteendedata till exempel behöver vidarebefordras till ett externt system utan att kopplas till andra datakällor i filen för en viss användare.

## Målkategorier {#categories}

Anslutningarna och tilläggen i [målkatalog](https://platform.adobe.com/destination/catalog) grupperas efter målkategori (**Reklam**, **molnlagring**, **Undersökningsplattformar**, **E-postmarknadsföring**, osv.), beroende på vilka marknadsföringsåtgärder de hjälper dig att uppnå. Mer information om var och en av kategorierna, samt vilka destinationer som ingår i varje kategori, finns i [Dokumentation för målkatalog](./catalog/overview.md).

![Målkategorier markerade på katalogsidan.](./assets/destination-types/destination-categories-menu.png)
