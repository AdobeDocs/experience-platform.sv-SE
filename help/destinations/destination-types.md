---
keywords: mål;mål;måltyper
title: Måltyper och -kategorier
description: Läs mer om de olika typerna och kategorierna av destinationer i Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: c6019737e93756f3f524d5a85ea57383baa1a31d
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Måltyper och -kategorier

Läs den här sidan om du vill veta mer om de olika typerna och kategorierna av Adobe Experience Platform-mål.

## Måltyper {#destination-types}

I Adobe Experience Platform skiljer vi mellan olika måltyper - anslutningar, datauppsättningsexport och tillägg. Det finns flera typer av anslutningsmål, så att du kan exportera data till API-baserade mål, sociala mål, CRM-plattformar och många andra.

Slutligen kan anslutningar även särskiljas mellan offentliga destinationer som är tillgängliga för alla organisationer i destinationskatalogen och privata destinationer som Real-Time CDP Ultimate-kunder kan skapa för att tillgodose sina specifika exportanvändningsfall.

![Typer av destinationsdiagram.](./assets/destination-types/types-of-destinations-no-highlight.png)

## Anslutningar {#connections}

**[!UICONTROL Profile Export]**, **[!UICONTROL Streaming Audience Export]** och **[!DNL Edge Personalization]** mål i Adobe Experience Platform samlar in händelsedata och kombinerar dem med andra datakällor för att skapa [kundprofilen i realtid](../profile/home.md), tillämpa segmentering och exportera målgrupper och kvalificerade profiler till destinationer.

## Profilexportdestinationer {#profile-export}

Profilexportdestinationer tar emot rådata, ofta med e-postadress som primärnyckel. Experience Platform har för närvarande stöd för två typer av profilexportdestinationer:

* [Exportmål för direktuppspelningsprofil (företagsmål)](#streaming-profile-export)
* [Batchmål (filbaserade)](#file-based)

### Exportmål för direktuppspelningsprofil (företagsmål) {#streaming-profile-export}

>[!IMPORTANT]
>
>Företagsmål, eller exportmål för direktuppspelningsprofiler, är endast tillgängliga för [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) -kunder.

Använd dataanslutningarna för företag för att leverera Adobe Real-time Customer Data Platform-profiler i nära realtid till interna system eller till andra tredjepartssystem för datasynkronisering, analys och fler användningsfall för profilberikning.

Dessa mål tar emot målgrupps- och profildata som dataströmmar från Experience Platform.

Företagets mål är:

* [HTTP API-mål](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)

### Batchmål (filbaserade) {#file-based}

Filbaserade mål tar emot `.csv` filer som innehåller profiler och/eller attribut. [Amazon S3](catalog/cloud-storage/amazon-s3.md) är ett exempel på en destination där du kan exportera filer som innehåller profilexporter.

## Målgrupper för direktuppspelad export {#streaming-destinations}

Målgrupper för målgruppsexport tar emot Experience Platform-målgruppsdata. Dessa mål använder målgrupps-ID eller användar-ID. Advertising och sociala mål som [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) eller [Facebook](catalog/social/facebook.md) är exempel på sådana mål.

## Edge personaliseringsmål {#edge-personalization-destinations}

Edge personaliseringsmål i Experience Platform omfattar [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) och [Anpassat personaliseringsmål](/help/destinations/catalog/personalization/custom-personalization.md). Genom att använda dessa destinationer kan ni möjliggöra användning av samma sida och nästa sida för personalisering för era kunder.

Läs mer om hur du [konfigurerar anpassningsmål för samma sida och nästa sida-personalisering](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Profilexport och målgruppsexportdestinationer - videoöversikt {#video}

I videon nedan beskrivs de två typerna av destinationer:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Typer av exporterade målgrupper {#exported-audiences-types}

Du kan exportera tre typer av målgrupper från Experience Platform till olika destinationer:

* Målgrupper
* Målgrupper
* Potentiella målgrupper

Läs mer om [olika målgruppstyper](/help/segmentation/ui/account-audiences.md#terminology).

En symbol på målkortet visar vilka typer av målgrupper du kan exportera till varje mål.

![Exempel på målkort med symboler som visar vilka målgruppstyper som kan exporteras.](/help/destinations/assets/destination-types/types-of-audiences.png)


## Exportmål för datauppsättning {#dataset-export-destinations}

Vissa molnlagringsmål i målkatalogen stöder datauppsättningsexporter. Använd dessa mål för att exportera rådatauppsättningar till molnlagringsplatser.

Läs mer om hur du [exporterar datauppsättningar](/help/destinations/ui/export-datasets.md).

## Tillägg {#extensions}

Plattformen utnyttjar tagghanteringens kraft och flexibilitet, vilket gör att du kan konfigurera taggtillägg i användargränssnittet.

>[!TIP]
>
>Detaljerad information om taggtillägg, inklusive användningsexempel och hur du hittar dem i gränssnittet, finns i [Översikt över taggtillägg](./catalog/launch-extensions/overview.md).

Med taggtillägg vidarebefordras råa händelsedata till flera typer av mål. Tänk på tillägg som en **typ av mål för**-händelsevidarebefordran. Detta är en enklare typ av integrering med målplattformar, som bara vidarebefordrar råhändelsedata. Exempel på sådana är [Gainsight-tillägget för personalisering](./catalog/personalization/gainsight.md) eller [Bekräfta röst för kundtillägget](./catalog/voice/confirmit-digital-feedback.md).

![Taggtillägg jämfört med andra mål](./assets/common/launch-and-other-destinations.png)

## När anslutningar och tillägg ska användas {#when-to-use}

Som marknadsförare kan du använda en kombination av anslutningar och tillägg för att hantera dina användningsfall.

Anslutningar är användbara när det är nödvändigt att utnyttja en fullständig centraliserad kundprofil eller en kundpublik för aktivering. Använd till exempel anslutningar om du kopplar beteendedata från ett analyssystem med överförda CRM-data för att kvalificera en användare för en viss målgrupp innan du levererar ett anpassat meddelande till den användaren.

Tillägg är användbara när händelsedata används för att utlösa en åtgärd eller för att utföra segmentering i en extern miljö. Om beteendedata till exempel behöver vidarebefordras till ett externt system utan att kopplas till andra datakällor i filen för en viss användare.

## Målkategorier {#categories}

Anslutningarna och tilläggen i [målkatalogen](https://platform.adobe.com/destination/catalog) grupperas efter målkategori (**Advertising**, **Cloud-lagring**, **Undersökningsplattformar**, **E-postmarknadsföring** osv.), beroende på vilken marknadsföringsåtgärd de hjälper dig att uppnå. Mer information om var och en av kategorierna, samt vilka mål som ingår i varje kategori, finns i dokumentationen för [målkatalogen](./catalog/overview.md).

![Målkategorier är markerade på katalogsidan.](./assets/destination-types/destination-categories-menu.png)
