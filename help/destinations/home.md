---
keywords: destinationer;adobe experience platform;platform;mål overview;activate data;activate;
title: Översikt över destinationer
seo-title: Översikt över destinationer
description: Lär dig hur du aktiverar Adobe Experience Platform-data till destinationer för flerkanalskampanjer, e-postmeddelanden, riktad reklam och mycket annat.
seo-description: Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda Destinationer i Adobe Experience Platform för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# [!DNL Destinations] översikt {#overview}

![Översiktsbanderoll för destinationer](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

## Destinationer och källor {#destinations-and-sources}

En av de viktigaste funktionerna i Platform är att inhämta era egna data och aktivera dem för era affärsbehov. Använd källor för att importera data till plattformen och destinationer för att exportera data från plattformen.

## Destinationssteg {#steps}

* Välj från en [självbetjäningskatalog](./catalog/overview.md) av alla mål som är tillgängliga i Platform.
* Använd **[!UICONTROL Destinations]** för att [aktivera](./ui/activate-destinations.md) och skicka profiler eller segment till automatiserade marknadsföringsplattformar, digitala annonsplattformar med mera.
* Schemalägg dataexport till dina önskade destinationer vid regelbundna tidpunkter.

## Kontroller {#controls}

Med kontrollerna på arbetsytan [Destinationer](./ui/destinations-workspace.md) kan du:

* Bläddra i katalogen med destinationsplattformar där du kan aktivera dina data;
* Skapa, redigera, aktivera och inaktivera dataflöden till destinationerna i katalogen,
* Skapa ett konto på en lagringsplats eller länkplattform till kontot på målplattformen.
* Välj vilka segment som ska aktiveras för destinationer.
* Välj vilka [XDM-fält (Experience Data Model)](../xdm/home.md) som ska exporteras när segment aktiveras till e-postmarknadsföringsmål.

## Måltyper och -kategorier {#types-and-categories}

Mer information finns i översikten över måltyper och kategorier](./destination-types.md).[

## Destinationer och åtkomstkontroller {#access-controls}

Målfunktionerna i Platform fungerar med Adobe Experience Platform åtkomstkontrollsbehörigheter. Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. Information om de enskilda behörigheterna finns i [Åtkomstkontroll i Adobe Experience Platform](../access-control/home.md) och rulla nedåt till på sidan.

Mer information om åtkomstkontroller finns i [Användarhandboken för åtkomstkontroll](../access-control/ui/overview.md).

## [!DNL Data Governance] begränsningar för att aktivera data till destinationer  {#data-governance}

Datastyrningen används för plattformsdestinationer genom:

* *Marknadsföringsanvändningsfall* som du kan välja i arbetsflödet för att skapa destinationer;
* *Dataanvändningsprinciper* som begränsar möjligheten att aktivera data som innehåller vissa användningsetiketter till destinationer med vissa användningsfall för marknadsföring.

Se [!DNL Data Governance] i plattformsdokumentationen för mer information om [användningsfall för marknadsföring](../data-governance/policies/overview.md) och [lösning av datapolicyöverträdelser](../data-governance/enforcement/auto-enforcement.md).

Mer information om hur du väljer användningsfall för marknadsföring i arbetsflödet för att skapa mål finns på följande sidor för de olika måltyperna i Platform:

* [Annonsmål - Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [Annonsmål - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Annonsmål - Google Display och Video 360  ](./catalog/advertising/google-dv360.md)
* [Lagringsmål i molnet](./catalog/cloud-storage/workflow.md)
* [E-postmarknadsföringsmål](./catalog/email-marketing/overview.md)
* [Målgrupper i sociala nätverk](./catalog/social/workflow.md)

Mer information om brott mot datapolicyer i arbetsflödet för segmentaktivering finns i granskningssteget i [Aktivera profiler och segment till ett mål](./ui/activate-destinations.md#review).