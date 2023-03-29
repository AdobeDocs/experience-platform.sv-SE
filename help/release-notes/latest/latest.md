---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation mars 2023 för Adobe Experience Platform.
source-git-commit: 38c3461f1d84fca83fd04eef57aae28de4744e17
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 29 mars 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainsamling](#data-collection)
- [Dataförberedelse](#data-prep)
- [Mål ](#destinations)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nytt snabbstartarbetsflöde för Meta Conversions API (beta) | Kom åt nya snabbstartarbetsflöden via&quot;Komma igång&quot; från startskärmen för datainsamling! The [snabbstartsarbetsflöde för Meta Conversion API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) gör det möjligt för kunderna att snabbt samla in och vidarebefordra händelsedata, från serversidan till Meta för annonskonverteringar med bara några få enkla steg. |
| [!DNL Braze] tillägg för händelsevidarebefordran | The [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) tillägg för händelsevidarebefordran gör att du kan utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Braze] i form av händelser på serversidan med [!DNL Braze] API:er för användarspårning. |
| [!DNL Mixpanel] tillägg för händelsevidarebefordran | The [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Med hjälp av tillägget kan kunder utnyttja händelsevidarebefordran för att hämta händelseinformation i Adobe Experience Platform Edge Network och skicka den till Mixpanel med API:t för spårningshändelser. |

{style="table-layout:auto"}

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya funktioner för kodning och avkodning av URL-strängar | <ul><li>The `get_url_encoded` funktionen tar en URL som indata och ersätter eller kodar specialtecken med ASCII-tecken.</li><li>The `get_url_decoded` funktionen tar en URL som indata och avkodar ASCII-tecken till specialtecken.</li></ul> Mer information finns i [Handbok för dataprefixfunktioner](../../data-prep/functions.md). En omfattande lista över reserverade tecken och motsvarande kodade tecken finns i guiden [specialtecken](../../data-prep/functions.md#special-characters). |

Mer information om Data Prep finns i [Översikt över datapreflight](../../data-prep/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer** {#new-destinations}

| Destination | Beskrivning |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] anslutning GA](../../destinations/catalog/personalization/adobe-commerce.md) | The [!DNL Adobe Commerce] målanslutning (nu allmänt tillgänglig) låter dig välja en eller flera Real-Time CDP-målgrupper att aktivera för [!DNL Adobe Commerce] för att leverera en dynamisk personaliserad upplevelse till era kunder. |
| [[!DNL Snap Inc] anslutning GA](../../destinations/catalog/advertising/snap-inc.md) | The [!DNL Snap Inc] destinationsanslutning (nu allmänt tillgänglig) tillåter marknadsförare att importera användarsegment som skapats i Experience Platform till [!DNL Snapchat Ads] och använda dem för att rikta in sina annonser. |
| [(API) Oraclena Eloqua-anslutning](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Använd den API-baserade anslutningen för att [!DNL Oracle Eloqua] att planera och genomföra kampanjer samtidigt som ni levererar en personaliserad kundupplevelse för sina presumtiva kunder i [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] anslutning](../../destinations/catalog/advertising/amazon-ads.md) | The [!DNL Amazon Ads] integrering med Adobe Experience Platform ger nyckelfärdig integrering med [!DNL Amazon Ads] produkter, inklusive [!DNL Amazon DSP (ADSP)]. Använda [!DNL Amazon Ads] i Adobe Experience Platform kan man definiera målgrupper för annonser för målinriktning och aktivering på [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] anslutning](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (tidigare Bizible) ger marknadsförarna insikt i vilka marknadsföringssatsningar som är mest effektiva när det gäller att öka intäkterna och maximera avkastningen på investeringen för deras företag. Målet möjliggör dataflöden från företag till företag (B2B) från Adobe Experience Platform till [!DNL Marketo Measure]. Kortet är bara tillgängligt för [!DNL Marketo Measure Ultimate] kunder. |
| [TikTok-anslutning](../../destinations/catalog/social/tiktok.md) | Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. |
| [Zendesk-anslutning](../../destinations/catalog/crm/zendesk.md) | Använd det här målet för att skapa och uppdatera identiteter inom ett segment som kontakter inom [!DNL Zendesk]. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Ny åtkomstkontrollbehörighet för mål: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | Den nya behörigheten ger användarna möjlighet att aktivera segment för befintliga destinationer, utan att visa [mappningssteg](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Användare kan lägga till och ta bort segment i aktiveringsarbetsflöden, men kan inte lägga till eller ta bort mappade attribut eller identiteter. |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

Vi släpper en felkorrigering för PGP/GPG-kryptering i filbaserade mål för CDP i realtid. Den här ändringen innebär att befintliga filbaserade mål som använder kryptering genererar ett filnamn med ett annat filtillägg än tidigare.

- Aktuellt tillägg när kryptering används: `filename.csv`
- Framtida tillägg när kryptering används: `filename.csv.gpg`

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Profilmått | För att ni ska få en mer korrekt återgivning av profilmätvärden kombineras uppdelning efter medlemskap och omsättningsstatistik och beräknas nu över en 24-timmarsperiod. Mer information finns i [Användargränssnittsguide för segmentering](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tillgänglighet för betaversion av [!DNL Chatlio] | The [!DNL Chatlio] finns nu i betaversionen. Använd [!DNL Chatlio] strömma [!DNL Chatlio] händelsedata till Experience Platform. Mer information finns i [[!DNL Chatlio] översikt](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Tillgänglighet för betaversion av [!DNL Customer.io] | The [!DNL Customer.io] finns nu i betaversionen. Använd [!DNL Customer.io] för att strömma era kundhändelsedata till Experience Platform. Mer information finns i [[!DNL Customer.io] översikt](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Tillgänglighet för betaversion av [!DNL Pendo] | The [!DNL Pendo] finns nu i betaversionen. Använd [!DNL Pendo] för att strömma era produktanalysdata till Experience Platform. Mer information finns i [[!DNL Pendo] översikt](../../sources/connectors/analytics/pendo-webhook.md). |
| Stöd för dataflöden | Du kan nu använda API:t för Flow Service för att ställa in dataflödena till ett utkasttillstånd. Ritade dataflöden kan senare uppdateras och publiceras med ny information. Mer information finns i guiden [ange källans dataflöden som utkast](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).
