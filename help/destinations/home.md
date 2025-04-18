---
title: Översikt över destinationer
description: Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda Destinationer i Adobe Experience Platform för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 3%

---

# [!DNL Destinations] översikt {#overview}

![Målöversiktsbanderoll.](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinationer och källor {#destinations-and-sources}

En av de viktigaste funktionerna i Experience Platform är att inhämta era egna data och aktivera dem för era affärsbehov. Använd [källor](../sources/home.md) för att importera data till Experience Platform och mål för att exportera data från Experience Platform.

## Destinationssteg {#steps}

* Välj från en [självbetjäningskatalog](./catalog/overview.md) för alla mål som är tillgängliga i Experience Platform.
* Använd destinationer för att skicka målgrupper eller datauppsättningar till automatiserade marknadsföringsplattformar, digitala annonsnätverk med mera.
* Schemalägg dataexport till dina önskade destinationer vid regelbundna tidpunkter.

## Kontroller {#controls}

Med kontrollerna på [målarbetsytan](./ui/destinations-workspace.md) kan du:

* Bläddra i katalogen med destinationsplattformar där du kan aktivera dina data;
* Skapa, redigera, aktivera och inaktivera dataflöden till destinationerna i katalogen,
* Skapa ett konto på en lagringsplats eller länka Experience Platform till kontot på målplattformen.
* Välj vilka målgrupper eller datamängder som ska aktiveras för destinationer,
* Välj vilka [XDM-fält (Experience Data Model)](../xdm/home.md) som ska exporteras när målgrupper aktiveras till vissa mål, som e-postmarknadsföringsmål, CRM-plattformar, molnlagringsplatser och mycket mer.
* Aktivera olika typer av profiler och målgrupper för destinationer - personer, konton och potentiella kunder.

## Måltyper och -kategorier {#types-and-categories}

Med Experience Platform kan ni aktivera data till olika typer av destinationer för att tillgodose era användningsbehov. Målen kan vara allt från API-baserade integreringar till integreringar med mottagningssystem för filer, sökmål för profiler och mycket annat. Mer information om alla tillgängliga destinationer finns i översikten över [måltyper och kategorier](./destination-types.md).

## Adobe-byggda och partnerbyggda destinationer {#adobe-and-partner-built-destinations}

Vissa av anslutningarna i Experience Platform målkatalog byggs och underhålls av Adobe, medan andra byggs och underhålls av partnerföretag som använder [Destination SDK](/help/destinations/destination-sdk/overview.md). En anteckning högst upp på dokumentationssidan för varje partnerbyggd koppling anropar om ett mål skapas och underhålls av partnern. Till exempel skapas [Amazon S3-anslutningen](/help/destinations/catalog/cloud-storage/amazon-s3.md) av Adobe medan [TikTok-anslutningen](/help/destinations/catalog/social/tiktok.md) skapas och underhålls av TikTok-teamet.

För partnerskapade och underhållna anslutningar innebär detta att problem med kopplingen kan behöva lösas av partnerteamet (kontaktmetoden finns i anteckningen på dokumentationssidan). Kontakta Adobe eller kundtjänst om du har problem med kontakter som skapats och underhålls av Adobe.

## Destinationer och åtkomstkontroller {#access-controls}

Målfunktionerna i Experience Platform fungerar med Adobe Experience Platform åtkomstkontrollsbehörigheter. Beroende på din användares behörighetsnivå kan du visa, hantera och aktivera mål. Om du vill ha information om de enskilda behörigheterna går du till [åtkomstkontrollen i Adobe Experience Platform](../access-control/home.md) och rullar ned till tabellen längst ned på sidan.

Följande tabell visar vilka behörigheter och behörighetskombinationer som krävs för att utföra vissa åtgärder på mål.

| Behörighetsnivå | Beskrivning |
| ---- | ---- |
| **[!UICONTROL View Destinations]** | Om du vill få åtkomst till målfliken i Experience Platform-gränssnittet behöver du **[!UICONTROL View Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Manage Destinations]** | Om du vill ansluta till mål behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** | Om du vill aktivera målgrupper till mål och aktivera [mappningssteget](ui/activate-batch-profile-destinations.md#mapping) i arbetsflödet behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** | Om du vill lägga till eller ta bort målgrupper från befintliga dataflöden utan att ha tillgång till [mappningssteget](ui/activate-batch-profile-destinations.md#mapping) i arbetsflödet behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Destinations]**, **[!UICONTROL Manage and Activate Dataset Destinations]** | Om du vill exportera datauppsättningar till mål behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage and Activate Dataset Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). |
| **[!UICONTROL View Identity Graph]** | Om du vill exportera *identiteter* till mål måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

I diagrammet nedan visas vilka behörigheter du behöver beroende på vilka åtgärder du vill utföra på målen.

![Diagram som visar de behörigheter som krävs för att utföra vissa åtgärder på mål.](/help/destinations/assets/overview/permissions-diagram.png)

Mer information om åtkomstkontroller finns i användarhandboken för [Åtkomstkontroll](../access-control/ui/overview.md).

### Attributbaserad åtkomstkontroll för mål {#attribute-based-access}

Med attributbaserad åtkomstkontroll i Adobe Experience Platform kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut.

Med attributbaserad åtkomstkontroll kan du tillämpa mappningskonfigurationer på fält som du har behörighet till. Dessutom kan du inte exportera data till ett mål om du inte har tillgång till alla fält i datauppsättningen.

Mer information om hur mål fungerar med attributbaserade åtkomstkontroller finns i [attributbaserad åtkomstkontroll](../access-control/abac/overview.md#destinations).

## Profilborttagning från mål {#profile-removal}

När en profil tas bort från en målgrupp som har aktiverats till ett mål tas även den profilen bort från motsvarande målgrupp på målplattformen. Om en profil tas bort från en målgrupp som tidigare aktiverats för LinkedIn, tas den profilen bort från den associerade [!UICONTROL LinkedIn Matched Audience].

Borttagning av profiler från destinationer - som också kallas osegmentering - sker på samma avstånd som segmentering. Så snart en profil har tagits bort från en målgrupp i Experience Platform återspeglas ändringen i nästa schemalagda dataflöde och profilen tas bort från målgruppen.

Den faktiska hastighet med vilken profilborttagningen börjar gälla på målplattformen kan variera beroende på målets beteende vid förtäring och bearbetning.

## Destinationsövervakning {#destinations-monitoring}

När du har upprättat en anslutning till ett mål och slutfört aktiveringsarbetsflödet kan du övervaka dataexporten till mottagningssystemet. Läs [guiden om övervakning av dataflöden till mål i användargränssnittet](/help/dataflows/ui/monitor-destinations.md) om du vill ha mer information.

![Exempel på målövervakningssida.](./assets/overview/monitoring-page-example.png)

Du kan också validera om data kommer fram till målet. De flesta måldokumentationssidor i katalogen har *avsnittet Validera dataexport*, som anger hur du kan kontrollera på målplattformen att data hämtas från Experience Platform. Visa ett exempel på det här avsnittet för [Amazon Ads-målet](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Begränsningar för datastyrning när data aktiveras till destinationer {#data-governance}

Datastyrning tillämpas för Experience Platform-destinationer genom:

* *Marknadsföringsåtgärder* som du kan välja i arbetsflödet för att skapa mål;
* *Dataanvändningsprinciper* som begränsar data som innehåller vissa användningsetiketter från att aktiveras till mål med vissa marknadsföringsåtgärder.

Mer information om [marknadsföringsåtgärder](../data-governance/policies/overview.md) och [att lösa datapolicyöverträdelser](../data-governance/enforcement/auto-enforcement.md) finns i Datastyrning i Experience Platform-dokumentationen.

Mer information om hur du väljer marknadsföringsåtgärder i arbetsflödet för att skapa mål finns på följande sidor för de olika måltyperna i Experience Platform:

* [Advertising-destinationer - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Advertising-destinationer - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Advertising-mål - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Lagringsmål i molnet](./catalog/cloud-storage/overview.md)
* [E-postmarknadsföringsmål](./catalog/email-marketing/overview.md)
* [Social destination](./catalog/social/overview.md)

Mer information om brott mot datapolicyer i arbetsflödet för målgruppsaktivering finns i **[!UICONTROL Review]**-steget i följande guider:

* [Aktivera målgruppsdata för att strömma målgrupper och exportera destinationer](./ui/activate-segment-streaming-destinations.md#review)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](./ui/activate-streaming-profile-destinations.md#review)
* [Aktivera målgruppsdata för att batchprofilera exportmål](./ui/activate-batch-profile-destinations.md#review)

## Villkor {#terms-and-conditions}

Genom att använda något av de destinationer som är märkta som betaversioner (&quot;Beta&quot;) bekräftar du härmed att Beta tillhandahålls ***i befintligt skick utan garanti av något slag***.

Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, modifiera eller på annat sätt stödja Beta. Du rekommenderas att använda Informativ och inte på något sätt förlita dig på att sådana Beta och/eller medföljande material fungerar korrekt eller fungerar korrekt. Beta betraktas som Konfidentiell information om Adobe.

All &quot;Feedback&quot; (information om Beta, inklusive men inte begränsad till problem eller defekter som du stöter på när du använder Beta, förslag, förbättringar och rekommendationer) som du ger Adobe tilldelas härmed till Adobe, inklusive alla rättigheter, titlar och intressen i och för sådan feedback.

Skicka Öppna feedback eller skapa en supportanmälan för att dela dina förslag eller rapportera ett fel, sök efter en funktionsförbättring.