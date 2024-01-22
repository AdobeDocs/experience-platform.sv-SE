---
title: Översikt över destinationer
description: Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda Destinationer i Adobe Experience Platform för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 6dd6190f1b006ffb3346eea6dc917ce52e0aa1c6
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# [!DNL Destinations] översikt {#overview}

![Översiktsbanderoll för destinationer.](./assets/overview/destinations-overview-banner.png)

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
* Använd destinationer för att skicka målgrupper eller datauppsättningar till automatiserade marknadsföringsplattformar, digitala annonsnätverk med mera.
* Schemalägg dataexport till dina önskade destinationer vid regelbundna tidpunkter.

## Kontroller {#controls}

Kontrollerna i [målarbetsyta](./ui/destinations-workspace.md) kan du:

* Bläddra i katalogen med destinationsplattformar där du kan aktivera dina data;
* Skapa, redigera, aktivera och inaktivera dataflöden till destinationerna i katalogen,
* Skapa ett konto på en lagringsplats eller länkplattform till kontot på målplattformen.
* Välj vilka målgrupper eller datamängder som ska aktiveras för destinationer,
* Välj vilken [XDM-fält (Experience Data Model)](../xdm/home.md) exportera när målgrupper aktiveras till vissa destinationer, som e-postmarknadsföringsmål, CRM-plattformar, molnlagringsplatser med mera.
* Aktivera olika typer av profiler och målgrupper för destinationer - personer, konton och potentiella kunder.

## Måltyper och -kategorier {#types-and-categories}

Med Experience Platform kan ni aktivera data till olika typer av destinationer för att tillgodose era användningsbehov. Målen kan vara allt från API-baserade integreringar till integreringar med mottagningssystem för filer, sökmål för profiler och mycket annat. Mer information om alla tillgängliga destinationer finns i [måltyper och kategorier - översikt](./destination-types.md).

## Destinationer byggda av Adobe och partnerbyggda {#adobe-and-partner-built-destinations}

Vissa av anslutningarna i Experience Platform destinationskatalog byggs och underhålls av Adobe, medan andra byggs och underhålls av partnerföretag som använder [Destination SDK](/help/destinations/destination-sdk/overview.md). En anteckning högst upp på dokumentationssidan för varje partnerbyggd koppling anropar om ett mål skapas och underhålls av partnern. Till exempel [Amazon S3-anslutning](/help/destinations/catalog/cloud-storage/amazon-s3.md) skapas av Adobe, medan [TikTok Connector](/help/destinations/catalog/social/tiktok.md) skapas och underhålls av TikTok team.

För partnerskapade och underhållna anslutningar innebär detta att problem med kopplingen kan behöva lösas av partnerteamet (kontaktmetoden finns i anteckningen på dokumentationssidan). Om du har problem med kontakter som utvecklats och underhålls av Adobe kontaktar du Adobe eller kundtjänst.

## Destinationer och åtkomstkontroller {#access-controls}

Målfunktionerna i Platform fungerar med Adobe Experience Platform åtkomstkontrollsbehörigheter. Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. Information om de enskilda behörigheterna finns på [åtkomstkontroll i Adobe Experience Platform](../access-control/home.md) och rulla ned till tabellen längst ned på sidan.

Följande tabell visar vilka behörigheter och behörighetskombinationer som krävs för att utföra vissa åtgärder på mål.

| Behörighetsnivå | Beskrivning |
| ---- | ---- |
| **[!UICONTROL View Destinations]** | För att få åtkomst till fliken Destinationer i användargränssnittet i Experience Platform måste du ha **[!UICONTROL View Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Manage Destinations]** | Om du vill ansluta till mål behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** | Aktivera målgrupper till destinationer och aktivera [mappningssteg](ui/activate-batch-profile-destinations.md#mapping) i arbetsflödet behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** | Lägga till eller ta bort målgrupper från befintliga dataflöden utan att ha tillgång till [mappningssteg](ui/activate-batch-profile-destinations.md#mapping) i arbetsflödet behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Manage and Activate Dataset Destinations]** | Om du vill exportera datauppsättningar till mål behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage and Activate Dataset Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Identity Graph]** | Exportera *identiteter* till destinationer behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

I diagrammet nedan visas vilka behörigheter du behöver beroende på vilka åtgärder du vill utföra på målen.

![Diagram som visar de behörigheter som krävs för att utföra vissa åtgärder på destinationer.](/help/destinations/assets/overview/permissions-diagram.png)

Mer information om åtkomstkontroller finns i [Användarhandbok för åtkomstkontroll](../access-control/ui/overview.md).

### Attributbaserad åtkomstkontroll för mål {#attribute-based-access}

Med attributbaserad åtkomstkontroll i Adobe Experience Platform kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut.

Med attributbaserad åtkomstkontroll kan du tillämpa mappningskonfigurationer på fält som du har behörighet till. Dessutom kan du inte exportera data till ett mål om du inte har tillgång till alla fält i datauppsättningen.

Mer information om hur destinationer fungerar med attributbaserade åtkomstkontroller finns i [attributbaserad åtkomstkontroll - översikt](../access-control/abac/overview.md#destinations).

## Destinationsövervakning {#destinations-monitoring}

När du har upprättat en anslutning till ett mål och slutfört aktiveringsarbetsflödet kan du övervaka dataexporten till mottagningssystemet. Läs [guide om övervakning av dataflöden till destinationer i användargränssnittet](/help/dataflows/ui/monitor-destinations.md) för mer information.

![Exempel på sida för övervakning av destinationer.](./assets/overview/monitoring-page-example.png)

Du kan också validera om data kommer fram till målet. De flesta måldokumentationssidor i katalogen har en *Avsnittet Validera dataexport*, vilket visar hur du kan kontrollera på målplattformen att data har hämtats in från Experience Platform. Visa ett exempel på det här avsnittet för [Amazon Ads - mål](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Begränsningar för datastyrning när data aktiveras till destinationer {#data-governance}

Datastyrningen används för plattformsdestinationer genom:

* *Marknadsföringsåtgärder* som du kan välja i arbetsflödet för att skapa destinationer,
* *Dataanvändningspolicyer* som begränsar data som innehåller vissa användningsetiketter från att aktiveras till destinationer med vissa marknadsföringsåtgärder.

Mer information om datastyrning i plattformsdokumentationen finns i Datastyrning i plattformsdokumentation [marknadsföringsaktiviteter](../data-governance/policies/overview.md) och [lösa överträdelser av datapolicyer](../data-governance/enforcement/auto-enforcement.md).

Mer information om hur du väljer marknadsföringsåtgärder i arbetsflödet för att skapa mål finns på följande sidor för de olika måltyperna i Platform:

* [Annonsmål - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Annonsmål - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Annonsmål - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Lagringsmål i molnet](./catalog/cloud-storage/overview.md)
* [E-postmarknadsföringsmål](./catalog/email-marketing/overview.md)
* [Social destination](./catalog/social/overview.md)

Mer information om brott mot datapolicyn i arbetsflödet för målgruppsaktivering finns i **[!UICONTROL Review]** steg i följande guider:

* [Aktivera målgruppsdata för att strömma målgrupper och exportera destinationer](./ui/activate-segment-streaming-destinations.md#review)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](./ui/activate-streaming-profile-destinations.md#review)
* [Aktivera målgruppsdata för att batchprofilera exportmål](./ui/activate-batch-profile-destinations.md#review)
