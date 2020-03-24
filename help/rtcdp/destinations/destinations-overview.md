---
title: Destinationsöversikt
seo-title: Destinationsöversikt
description: Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från kunddataplattformen i realtid. Ni kan använda Destinationer i Adobes kunddataplattform i realtid för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad annonsering och många andra användningsfall.
seo-description: Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från kunddataplattformen i realtid. Ni kan använda Destinationer i Adobes kunddataplattform i realtid för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad annonsering och många andra användningsfall.
translation-type: tm+mt
source-git-commit: e66f4df13afb3c9f9ddb440ccb5e479caeef2142

---


# Destinationsöversikt

![Översiktsbanderoll för destinationer](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**Destinationer** är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från kunddataplattformen i realtid. Ni kan använda **Destinationer** för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

## Destinationer och källor

En av de viktigaste funktionerna i CDP i realtid är att inhämta era egna data och aktivera dem för era affärsbehov. Använd **[!UICONTROL Sources]** för att importera data till CDP i realtid och **[!UICONTROL Destinations]** för att exportera data från CDP i realtid.

## Destinationssteg

* Använd **[!UICONTROL Destinations]** för att [aktivera](/help/rtcdp/destinations/activate-destinations.md) och skicka profiler eller segment till automatiserade marknadsföringsplattformar, digitala annonsplattformar och mycket annat.
* Välj från en [självbetjäningskatalog](/help/rtcdp/destinations/destinations-catalog.md) med alla destinationer som är tillgängliga i CDP i realtid.
* Schemalägg dataexport till dina önskade destinationer vid regelbundna tidpunkter.

## Kontroller

Med kontrollerna på arbetsytan [](/help/rtcdp/destinations/destinations-workspace.md) Destinationer kan du:

* Bläddra i katalogen med destinationsplattformar där du kan aktivera dina data;
* Skapa, redigera, aktivera och inaktivera dataflöden till destinationerna i katalogen,
* Skapa ett konto på en lagringsplats eller länka CDP i realtid till kontot på målplattformen.
* Välj vilka segment som ska aktiveras för destinationer.
* Välj vilka XDM-fält ( [Experience Data Model)](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/xdm_system/xdm_system_in_experience_platform.md) som ska exporteras när segment aktiveras till e-postmarknadsföringsmål.

## Måltyper och -kategorier - videoöversikt

I Adobe Real-time CDP finns det två typer av destinationer: Profile Export Destinations och Segment Export Destinations. I videon nedan beskrivs de två typerna av destinationer.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Profilexportdestinationer

Profilexportdestinationer genererar en fil som innehåller profiler och/eller attribut. Dessa mål använder rådata, ofta med e-postadress som primärnyckel.

### Segmentexportdestinationer

Destinationer för segmentexport skickar profilerna och de segment som de är kvalificerade för. Dessa mål använder segment-ID eller användar-ID.

### Målkategorier

Destinationerna i [destinationskatalogen](/help/rtcdp/destinations/destinations-catalog.md) grupperas efter destinationskategori (**Advertising**, **Cloud storage** eller **Email marketing**). Mer information om var och en av dem finns i [målkatalogen](/help/rtcdp/destinations/destinations-catalog.md).

## Destinationer och åtkomstkontroller

Funktionerna i CDP i realtid fungerar med åtkomstkontrollsbehörigheterna i Adobe Experience Platform. **[!UICONTROL Destinations]** Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. Information om de enskilda behörigheterna finns i [Åtkomstkontroll i Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-overview.md) och rulla nedåt på sidan.

Mer information om åtkomstkontroller finns i användarhandboken för [åtkomstkontroll](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-user-guide.md).