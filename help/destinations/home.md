---
keywords: destinationer;adobe experience platform;platform;mål overview;activate data;activate;
title: Översikt över mål
description: Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda Destinationer i Adobe Experience Platform för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Destinations] översikt {#overview}

![Översiktsbanderoll för destinationer](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinationer och källor {#destinations-and-sources}

En av de viktigaste funktionerna i Platform är att inhämta era egna data och aktivera dem för era affärsbehov. Använd [källor](../sources/home.md) att importera data till plattformen och destinationer för att exportera data från plattformen.

## Destinationssteg {#steps}

* Välj bland en [självbetjäningskatalog](./catalog/overview.md) av alla destinationer som är tillgängliga i Platform.
* Använd destinationer för att skicka profiler eller segment till automatiserade marknadsföringsplattformar, digitala annonsplattformar med mera.
* Schemalägg dataexport till dina önskade destinationer vid regelbundna tidpunkter.

## Kontroller {#controls}

Kontrollerna i [målarbetsyta](./ui/destinations-workspace.md) kan du:

* Bläddra i katalogen med destinationsplattformar där du kan aktivera dina data;
* Skapa, redigera, aktivera och inaktivera dataflöden till destinationerna i katalogen,
* Skapa ett konto på en lagringsplats eller länkplattform till kontot på målplattformen.
* Välj vilka segment som ska aktiveras för destinationer.
* Välj vilken [XDM-fält (Experience Data Model)](../xdm/home.md) att exportera när segment aktiveras för e-postmarknadsföring.

## Måltyper och -kategorier {#types-and-categories}

Med Experience Platform kan ni aktivera data till olika typer av destinationer för att tillgodose era användningsbehov. Målen kan vara allt från API-baserade integreringar till integreringar med mottagningssystem för filer, sökmål för profiler och mycket annat. Mer information om alla tillgängliga destinationer finns i [måltyper och kategorier - översikt](./destination-types.md).

## Destinationer och åtkomstkontroller {#access-controls}

Målfunktionerna i Platform fungerar med Adobe Experience Platform åtkomstkontrollsbehörigheter. Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. Information om de enskilda behörigheterna finns i [Åtkomstkontroll i Adobe Experience Platform](../access-control/home.md) och rulla nedåt till sidans nederkant.

Följande tabell visar vilka behörigheter och behörighetskombinationer som krävs för att utföra vissa åtgärder på mål:

| Behörighetsnivå | Beskrivning |
| ---- | ----|
| **[!UICONTROL Manage Destinations]** | Om du vill ansluta till mål behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). |
| **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** | Aktivera segment till mål och aktivera [mappningssteg](ui/activate-batch-profile-destinations.md#mapping) i arbetsflödet behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** | Aktivera segment till mål och dölja [mappningssteg](ui/activate-batch-profile-destinations.md#mapping) i arbetsflödet behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). |

{style="table-layout:auto"}

Mer information om åtkomstkontroller finns i [Användarhandbok för åtkomstkontroll](../access-control/ui/overview.md).

### Attributbaserad åtkomstkontroll för mål {#attribute-based-access}

Med attributbaserad åtkomstkontroll i Adobe Experience Platform kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut.

Med attributbaserad åtkomstkontroll kan du tillämpa mappningskonfigurationer på fält som du har behörighet till. Dessutom kan du inte exportera data till ett mål om du inte har tillgång till alla fält i datauppsättningen.

Mer information om hur destinationer fungerar med attributbaserade åtkomstkontroller finns i [attributbaserad åtkomstkontroll - översikt](../access-control/abac/overview.md#destinations).

## Målövervakning {#destinations-monitoring}

När du har upprättat en anslutning till ett mål och slutfört aktiveringsarbetsflödet kan du övervaka dataexporten till mottagningssystemet. Läs [guide om övervakning av dataflöden till destinationer i användargränssnittet](/help/dataflows/ui/monitor-destinations.md) för mer information.

Du kan också validera om data kommer fram till målet. De flesta måldokumentationssidor i katalogen har en *Avsnittet Validera dataexport*, vilket visar hur du kan kontrollera på målplattformen att data har hämtats in från Experience Platform.

## Begränsningar för datastyrning vid aktivering av data till destinationer {#data-governance}

Datastyrningen används för plattformsdestinationer genom:

* *Marknadsföringsåtgärder* som du kan välja i arbetsflödet för att skapa destinationer,
* *Dataanvändningspolicyer* som förhindrar att data som innehåller vissa användningsetiketter aktiveras för destinationer med vissa marknadsföringsåtgärder.

Mer information om datastyrning i plattformsdokumentationen finns i Datastyrning i plattformsdokumentation [marknadsföringsaktiviteter](../data-governance/policies/overview.md) och [lösa överträdelser av datapolicyer](../data-governance/enforcement/auto-enforcement.md).

Mer information om hur du väljer marknadsföringsåtgärder i arbetsflödet för att skapa mål finns på följande sidor för de olika måltyperna i Platform:

* [Annonsmål - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Annonsmål - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Annonsmål - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Lagringsmål i molnet](./catalog/cloud-storage/overview.md)
* [E-postmarknadsföringsmål](./catalog/email-marketing/overview.md)
* [Sociala destinationer](./catalog/social/overview.md)

Mer information om brott mot datapolicyer i arbetsflödet för segmentaktivering finns i **[!UICONTROL Review]** steg i följande guider:

* [Aktivera målgruppsdata för att direktuppspela segmentexportmål](./ui/activate-segment-streaming-destinations.md#review)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](./ui/activate-streaming-profile-destinations.md#review)
* [Aktivera målgruppsdata för att batchprofilera exportmål](./ui/activate-batch-profile-destinations.md#review)
