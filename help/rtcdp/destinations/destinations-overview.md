---
title: Destinationsöversikt
seo-title: Destinationsöversikt
description: Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från kunddata i realtid på Platform. Ni kan använda Destinationer i Adobe Real-time Customer Data Platform för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
seo-description: Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från kunddata i realtid på Platform. Ni kan använda Destinationer i Adobe Real-time Customer Data Platform för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
translation-type: tm+mt
source-git-commit: a61a2a4d9d51c402bb50153c06a93d255a3613cb
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---


# Destinations Overview {#overview}

![Översiktsbanderoll för destinationer](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**Destinationer** är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från Real-time Customer Data Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

## Destinationer och källor {#destinations-and-sources}

En av de viktigaste funktionerna i CDP i realtid är att inhämta era egna data och aktivera dem för era affärsbehov. Använd källor för att importera data till CDP i realtid och destinationer för att exportera data från CDP i realtid.

## Destinationssteg {#steps}

* Välj från en [självbetjäningskatalog](/help/rtcdp/destinations/destinations-catalog.md) med alla destinationer som är tillgängliga i CDP i realtid.
* Använd **[!UICONTROL Destinations]** för att [aktivera](/help/rtcdp/destinations/activate-destinations.md) och skicka profiler eller segment till automatiserade marknadsföringsplattformar, digitala annonsplattformar och mycket annat.
* Schemalägg dataexport till dina önskade destinationer vid regelbundna tidpunkter.

## Kontroller {#controls}

Med kontrollerna på arbetsytan [](/help/rtcdp/destinations/destinations-workspace.md) Destinationer kan du:

* Bläddra i katalogen med destinationsplattformar där du kan aktivera dina data;
* Skapa, redigera, aktivera och inaktivera dataflöden till destinationerna i katalogen,
* Skapa ett konto på en lagringsplats eller länka CDP i realtid till kontot på målplattformen.
* Välj vilka segment som ska aktiveras för destinationer.
* Välj vilka XDM-fält ( [Experience Data Model)](../../xdm/home.md) som ska exporteras när segment aktiveras till e-postmarknadsföringsmål.

## Destination types and categories {#types-and-categories}

Mer information finns i Översikt över [måltyper och kategorier](/help/rtcdp/destinations/destination-types.md).

## Destinationer och åtkomstkontroller {#access-controls}

Målfunktionerna i CDP i realtid fungerar med åtkomstkontrollsbehörigheter i Adobe Experience Platform. Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. Information om de enskilda behörigheterna finns i [Åtkomstkontroll i Adobe Experience Platform](../../access-control/home.md) och rulla nedåt till sidans nederkant.

Mer information om åtkomstkontroller finns i användarhandboken för [åtkomstkontroll](../../access-control/ui/overview.md).

## Begränsningar för datastyrning vid aktivering av data till destinationer {#data-governance}

Datastyrning upprätthålls för CDP-destinationer i realtid genom:

* *Marknadsföringsanvändningsfall* som du kan välja i arbetsflödet för att skapa destinationer;
* *Dataanvändningsprinciper* som begränsar data som innehåller vissa användningsetiketter från att aktiveras till mål med vissa användningsfall för marknadsföring.

Läs Data Governance i CDP-dokumentation i realtid om du vill ha mer information om [användningsfall](/help/rtcdp/privacy/data-governance-overview.md#destinations) för marknadsföring och [lösning av brott mot](/help/rtcdp/privacy/data-governance-overview.md#enforcement)datapolicyn.

Mer information om hur du väljer användningsfall för marknadsföring i arbetsflödet för att skapa mål finns på följande sidor för de olika måltyperna i CDP för realtid:

* [Annonsmål - Google Ad Manager ](/help/rtcdp/destinations/google-ad-manager-destination.md)
* [Annonsmål - Google Ads](/help/rtcdp/destinations/google-ads-destination.md)
* [Annonsmål - Google Display och Video 360 ](/help/rtcdp/destinations/google-dv360-destination.md)
* [Lagringsmål i molnet](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)
* [E-postmarknadsföringsmål](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Målgrupper i sociala nätverk](/help/rtcdp/destinations/social-network-destinations-workflow.md)

Mer information om brott mot datapolicyer i arbetsflödet för segmentaktivering finns i steg 7 i [Aktivera profiler och segment till ett mål](/help/rtcdp/destinations/activate-destinations.md).