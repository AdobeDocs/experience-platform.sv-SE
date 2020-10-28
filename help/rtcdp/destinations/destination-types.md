---
keywords: destinations;destination;destination types
title: Destinationstyper och -kategorier
seo-title: Destinationstyper och -kategorier
description: 'På Adobe kunddataplattform i realtid samlar mål för profiler och segmentexport in händelsedata, kombinerar dem med andra datakällor, tillämpar segmentering och exporterar segment och kvalificerade profiler till destinationer. Med Experience Platform Launch-tillägg vidarebefordras råa händelsedata till flera typer av destinationer. '
seo-description: På Adobe kunddataplattform i realtid samlar mål för profiler och segmentexport in händelsedata, kombinerar dem med andra datakällor, tillämpar segmentering och exporterar segment och kvalificerade profiler till destinationer. Med Experience Platform Launch-tillägg vidarebefordras råa händelsedata till flera typer av destinationer.
translation-type: tm+mt
source-git-commit: e6276eac05f0a20a668051034e83831002a464f0
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# Måltyper och -kategorier

Läs den här sidan om du vill veta mer om de olika typerna och kategorierna av kunddataplattformsmål för Adobe i realtid.

## Måltyper

På Adobe kunddataplattform i realtid skiljer vi mellan två måltyper - anslutningar och tillägg. Det finns två typer av anslutningsmål: Profilexportmål och Segmentexportmål.

![Typer av destinationer](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Anslutningar {#connections}

**[!UICONTROL Profile Export]** och mål **[!UICONTROL Segment Export]** i kunddataplattformen i Adobe i realtid samlar in händelsedata, kombinerar dem med andra datakällor för att skapa kundprofilen [i](/help/profile/home.md)realtid, tillämpa segmentering och exportera segment och kvalificerade profiler till destinationer.

<br> 

#### Profilexportdestinationer

Profilexportdestinationer genererar en fil som innehåller profiler och/eller attribut. Dessa mål använder rådata, ofta med e-postadress som primärnyckel. Molnlagringsmålet [för](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 är ett exempel på destinationen där du kan placera filer som innehåller profilexporter.

#### Segmentexportdestinationer

Destinationer för segmentexport skickar profilerna och de segment de är kvalificerade för till målplattformarna. Dessa mål använder segment-ID eller användar-ID. Reklamdestinationer som [[!DNL Google Display & Video 360]](/help/rtcdp/destinations/google-dv360-destination.md) eller [[!DNL Google Ads]](/help/rtcdp/destinations/google-ads-destination.md) är exempel på dessa typer av destinationer.

#### Destinationer för profilexport och segmentexport - videoöversikt

I videon nedan beskrivs de två typerna av destinationer:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Tillägg {#extensions}

Adobe CDP i realtid utnyttjar kraften och flexibiliteten i Adobe Experience Platform Launch för att inkludera tillägg för Platform Launch i CDP-gränssnittet i realtid i Adobe.

>[!TIP]
>
>Mer information om Adobe Experience Platform Launch-tillägg, inklusive användningsexempel och hur du hittar dem i gränssnittet, finns i [Adobe Experience Platform Launch-tilläggsöversikten](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

Plattformsstartstillägg vidarebefordrar råa händelsedata till flera typer av destinationer. Tänk på tillägg som en **typ av mål för vidarebefordran** av händelser. Detta är en enklare typ av integrering med målplattformar, som bara vidarebefordrar råhändelsedata. Exempel på sådana är tillägget [](/help/rtcdp/destinations/gainsight-extension.md) Gainsight-anpassning eller [bekräftelsen från kundens tillägg](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

![Experience Platform Launch-tillägg jämfört med andra destinationer](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### När anslutningar och tillägg ska användas

Som marknadsförare kan du använda en kombination av anslutningar och tillägg för att hantera dina användningsfall.

Anslutningar är användbara när det är nödvändigt att utnyttja en fullständig centraliserad kundprofil eller ett kundsegment för aktivering. Använd till exempel anslutningar om du kopplar beteendedata från ett analyssystem med överförda CRM-data för att kvalificera en användare för ett visst segment innan du levererar ett anpassat meddelande till användaren.

Tillägg är användbara när händelsedata används för att utlösa en åtgärd eller för att utföra segmentering i en extern miljö. Om beteendedata till exempel behöver vidarebefordras till ett externt system utan att kopplas till andra datakällor i filen för en viss användare.

<br> 

## Målkategorier

Anslutningarna och tilläggen i [destinationskatalogen](https://platform.adobe.com/destination/catalog) grupperas efter destinationskategori (**Advertising**, **Cloud storage**, **Survey platforms**, **Email marketing** osv.), beroende på vilket marknadsföringsexempel de hjälper dig med. Mer information om var och en av kategorierna, samt vilka mål som ingår i varje kategori, finns i dokumentationen till [målkatalogen](/help/rtcdp/destinations/destinations-catalog.md).

![Målkategorier](/help/rtcdp/destinations/assets/destination-categories-menu.png)

