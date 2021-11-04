---
keywords: destinationer;adobe experience platform;platform;mål overview;activate data;activate;
title: Översikt över mål
seo-title: Destinations overview
description: Lär dig hur du aktiverar Adobe Experience Platform-data till destinationer för flerkanalskampanjer, e-postmeddelanden, riktad reklam och mycket annat.
seo-description: Destinations are pre-built integrations with destination platforms that allow for the seamless activation of data from Adobe Experience Platform. You can use Destinations in the Adobe Experience Platform to activate your known and unknown data for cross-channel marketing campaigns, email campaigns, targeted advertising, and many other use cases.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# [!DNL Destinations] översikt {#overview}

![Översiktsbanderoll för destinationer](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

## Destinationer och källor {#destinations-and-sources}

En av de viktigaste funktionerna i Platform är att inhämta era egna data och aktivera dem för era affärsbehov. Använd [källor](../sources/home.md) att importera data till plattformen och destinationer för att exportera data från plattformen.

## Destinationssteg {#steps}

* Välj bland en [självbetjäningskatalog](./catalog/overview.md) av alla destinationer som är tillgängliga i Platform.
* Använd destinationer för att skicka profiler eller segment till automatiserade marknadsföringsplattformar, digitala annonsplattformar med mera.
* Schemalägg dataexport till dina önskade destinationer vid regelbundna tidpunkter.

## Kontroller {#controls}

Kontrollerna i [Arbetsytan Destinationer](./ui/destinations-workspace.md) kan du:

* Bläddra i katalogen med destinationsplattformar där du kan aktivera dina data;
* Skapa, redigera, aktivera och inaktivera dataflöden till destinationerna i katalogen,
* Skapa ett konto på en lagringsplats eller länkplattform till kontot på målplattformen.
* Välj vilka segment som ska aktiveras för destinationer.
* Välj vilken [XDM-fält (Experience Data Model)](../xdm/home.md) att exportera när segment aktiveras för e-postmarknadsföring.

## Måltyper och -kategorier {#types-and-categories}

Mer information finns i [måltyper och kategorier - översikt](./destination-types.md).

## Destinationer och åtkomstkontroller {#access-controls}

Målfunktionerna i Platform fungerar med Adobe Experience Platform åtkomstkontrollsbehörigheter. Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. Information om de enskilda behörigheterna finns i [Åtkomstkontroll i Adobe Experience Platform](../access-control/home.md) och rulla nedåt till sidans nederkant.

Mer information om åtkomstkontroller finns i [Användarhandbok för åtkomstkontroll](../access-control/ui/overview.md).

## Begränsningar för datastyrning vid aktivering av data till destinationer {#data-governance}

Datastyrningen används för plattformsdestinationer genom:

* *Marknadsföringsåtgärder* som du kan välja i arbetsflödet för att skapa destinationer,
* *Dataanvändningspolicyer* som begränsar data som innehåller vissa användningsetiketter från att aktiveras till destinationer med vissa marknadsföringsåtgärder.

Mer information om datastyrning i plattformsdokumentationen finns i Datastyrning i plattformsdokumentation [marknadsföringsaktiviteter](../data-governance/policies/overview.md) och [lösa överträdelser av datapolicyer](../data-governance/enforcement/auto-enforcement.md).

Mer information om hur du väljer marknadsföringsåtgärder i arbetsflödet för att skapa mål finns på följande sidor för de olika måltyperna i Platform:

* [Annonsmål - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Annonsmål - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Annonsmål - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Lagringsmål i molnet](./catalog/cloud-storage/overview.md)
* [E-postmarknadsföringsmål](./catalog/email-marketing/overview.md)
* [Sociala destinationer](./catalog/social/overview.md)

Mer information om brott mot datapolicyer i arbetsflödet för segmentaktivering finns i steget Granska i följande handböcker:

* [Aktivera målgruppsdata för att direktuppspela segmentexportmål](./ui/activate-segment-streaming-destinations.md#review)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](./ui/activate-streaming-profile-destinations.md#review)
* [Aktivera målgruppsdata för att batchprofilera exportmål](./ui/activate-batch-profile-destinations.md#review)
