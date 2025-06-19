---
title: Versionsinformation för Adobe Experience Platform juni 2025
description: Versionsinformationen för juni 2025 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b39de456b40acda77c67d25ebeba2c8a41c5d3f6
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 49%

---


# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 18 juni 2025**

Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Åtkomstkontroll](#access-control)
- [Hantering av avancerad datalivscykel](#advanced-data-lifecycle-management)
- [Katalogtjänst](#catalog-service)
- [Kontrollpaneler](#dashboards)
- [Dataförvaltning](#data-governance)
- [Mål ](#destinations)
- [Federerad målgruppssammansättning](#fac)
- [Integritetstjänst](#privacy-service)
- [Sandlådor](#sandboxes)
- [Segmentering](#segmentation-service)
- [Källor](#sources)

## Åtkomstkontroll {#access-control}

Experience Platform använder [Adobe Admin Console](https://adminconsole.adobe.com)-produktprofiler för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd olika Experience Platform-funktioner, inklusive datamodellering, profilhantering och sandlådeadministration.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Exportera behörighet för instrumentpanelsdata | Alternativen **[!UICONTROL Download CSV]** och **[!UICONTROL Send as email]** på instrumentpaneler kräver nu behörighet **[!UICONTROL Export Dashboard Data]**. Denna behörighet säkerställer att endast behöriga användare kan exportera insiktsdata i tabellform, vilket ger bättre styrning och regler för dataåtkomstkontroll. Läs avsnittet [behörigheter i åtkomstkontrollguiden](../../access-control/home.md#permissions) om du vill ha mer information. |

Mer information finns i [åtkomstkontrollsöversikten](../../access-control/home.md).

## Hantering av avancerad datalivscykel {#advanced-data-lifecycle-management}

Experience Platform har en rad funktioner för datahygien som gör att du kan hantera lagrade data genom att ta bort konsumentposter och datauppsättningar programmatiskt. Med hjälp av arbetsytan Data Lifecycle i användargränssnittet eller genom anrop till Data Hygiene API kan du hantera dina datalager på ett effektivt sätt. Använd dessa funktioner för att säkerställa att informationen används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationspolicyer anser det nödvändigt.

**Ny dokumentation**

| Ny dokumentation | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för radering av post | Nu kan du ta bort enskilda poster baserat på identitetsfält med hjälp av gränssnittet eller API:t. Den här funktionen hjälper till att minska lagring, framtvinga styrning och förbättra datahygien genom att tillåta borttagningar från en enda datauppsättning eller från alla datauppsättningar. Volymbegränsningar och behörighetskrav gäller. Mer information finns i guiden [Ta bort poster](../../hygiene/ui/record-delete.md). |

Mer information finns i [översikt över livscykelhantering för avancerade data](../../hygiene/home.md).

## Katalogtjänst {#catalog-service}

Catalog Service är det system som registrerar var data finns och hur de härstammar från Adobe Experience Platform. Alla data som tas in i Experience Platform lagras i datasjön som filer och kataloger medan katalogen innehåller metadata och beskrivningar av dessa filer och kataloger för sök- och övervakningsändamål.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrad förhandsgranskning av datauppsättningar: snabbare navigering och tydligare insikter | Granska snabbt datauppsättningsdata, visa underliggande SQL-frågor och utforska upp till 100 rader med förbättrad filtrering och tydligare struktursynlighet - allt i den välbekanta förhandsgranskningen av datauppsättningen. Mer information finns i användarhandboken för [datauppsättningar](../../catalog/datasets/user-guide.md#preview). |

{style="table-layout:auto"}

## Kontrollpaneler {#dashboards}

Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Exportalternativ för Skicka som e-post | Du kan nu exportera upp till 10 000 poster från kontrollpaneler i läget Query Pro genom att välja **[!UICONTROL Send as email]** på menyn **[!UICONTROL View more]**. Det här alternativet skickar säkert en nedladdningslänk till ditt Adobe-relaterade e-postmeddelande för större exporter. Mer information finns i [Visa mer guide](../../dashboards/sql-insights-query-pro-mode/view-more.md#export). |

Läs [översikt över kontrollpaneler](../../dashboards/home.md) för mer information om kontrollpaneler, bland annat hur du beviljar åtkomstbehörigheter och skapar anpassade widgetar.

## Dataförvaltning {#data-governance}

Dataförvaltning i Adobe Experience Platform är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Den spelar en viktig roll inom [!DNL Experience Platform] på olika nivåer, bland annat katalogföring, datahärkomst, märkning av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Azure CMK-aviseringar och konfiguration av IP Tillåtelselista | Du kan nu tillåtslista Adobe statiska IP-adress i Azure Key Vault för att säkerställa fortsatt åtkomst när nätverksbegränsningar är aktiverade. Detta förhindrar störningar i plattformstjänsterna på grund av begränsad nyckelåtkomst. |
| Konfigurationsvarningar och -lösningar för CMK | Experience Platform utlöser nu varningsmeddelanden när Adobe-tjänster förlorar åtkomst till ditt Azure Key Vault (till exempel på grund av borttagna IP tillåtelselista-poster eller inaktiverade nycklar). En ny guide hjälper dig att förstå varje varning och vidta korrigerande åtgärder. |

Mer information finns i [översikten över dataförvaltning](../../data-governance/home.md).

## Mål  {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya destinationer**

| Mål | Beskrivning |
| --- | --- |
| [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md)-anslutning | Använd [!DNL Algolia]-målet för att leverera en konsekvent personalisering över webbplatser från hemsidan till sökningen. Bygg multimediala målgrupper från flera datakällor och dela dem i olika kanaler för bättre målinriktningsstrategier och kampanjpersonalisering. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| [Målgruppsövervakning](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) för direktuppspelningsmål | Övervakning på målgruppsnivå är nu tillgängligt för följande destinationer: <ul><li>[[!DNL (API) Oracle Eloqua] anslutning](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| Stöd för ytterligare identifierare för [Facebook](../../destinations/catalog/social/facebook.md#supported-identities)-mål | Målet [!DNL Facebook] har nu stöd för mappning av nya adressrelaterade fält för förbättrad målinriktning och matchning med profiler på Facebook-egenskaper. Mer information om de nya adressrelaterade fälten finns i avsnittet [identiteter som stöds](../../destinations/catalog/social/facebook.md#supported-identities). <br> ![Plattformsgränssnittsbild som visar ytterligare fält för Facebook.](../2025/assets/june/facebook-destination-fields.png "Plattformsgränssnittsbild som visar ytterligare fält för Facebook."){width="200" align="center" zoomable="yes"} |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) måluppgradering | Från och med 19 juni 2025 kan du se två **[!DNL Braze]**-kort sida vid sida i målkatalogen. Det här beror på en intern uppgradering av måltjänsten. Den befintliga målanslutningen [!DNL Braze] har bytt namn till **[!UICONTROL (Deprecated) Braze]** och du har nu tillgång till ett nytt kort med namnet **[!UICONTROL Braze]**. <br> Använd anslutningen **[!UICONTROL Braze]** i katalogen för nya aktiveringsdataflöden. Om du har aktiva dataflöden till målet **[!UICONTROL (Deprecated) Braze]** uppdateras de automatiskt. Du behöver därför inte göra något. <br> Om du skapar dataflöden via [Flow Service-API:et](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden: <ul><li>Flödesspecifikation-id: `cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>Anslutningsspecifikation-id: `ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

<!-- | [Google Customer Match + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md) general availability | The Google Customer Match + DV360 destination is now available for all Experience Platform users. The documentation now includes detailed guidance for [account linking](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking) between [!DNL Adobe] and [!DNL Google] advertising accounts. | -->

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Federerad målgruppssammansättning {#fac}

Med Federerad målgruppssammansättning kan företag sammanställa data för bättre användning i olika situationer. Med detta nya tillvägagångssätt, som Adobe Real-Time Customer Data Platform- och/eller Adobe Journey Optimizer-användare, kan ni federera datauppsättningar direkt från ert befintliga datalager för att skapa och berika Adobe Experience Platform-målgrupper och attribut i ett och samma system.

| Ny funktion | Beskrivning |
| ----------- | ----------- |
| Allmän tillgänglighet för kunder inom Adobe Healthcare Shield | Federated Audience Composition kommer att vara tillgängligt för kunder som använder Adobe Healthcare Shield för att skapa, berika och berika målgrupper före slutet av juni. Mer information om sekretess- och säkerhetsåtgärder för federerad målgruppskomposition finns i [sekretess- och säkerhetsöversikten för Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security). Mer information om HIPAA-kompatibilitet för Experience Platform-produkter i allmänhet finns i [HIPAA- och Adobe Products and Services-översikt](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Mer information finns i dokumentationen för [Federerad målgruppssammansättning (Federated Audience Composition)](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Flera juridiska och organisatoriska bestämmelser ger användare rätt att på begäran få tillgång till eller radera sina personuppgifter från dina datalager. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service] kan du skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-applikationer, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | ---|
| Stöd för Tennessee och Minnesota Privacy Laws | Privacy Service stöder nu Tennessee Information Protection Act (`tipa_tn_usa`) och Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Du kan bearbeta begäranden om åtkomst och borttagning i enlighet med dessa nya regler på statusnivå. Mer information finns i [Regelöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview). |

Mer information om tjänsten finns i [översikten över Privacy Service](../../privacy-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Migrering av uppdateringar av objektkonfiguration | Du kan nu migrera uppdateringar av konfiguration av iterativa objekt mellan sandlådor efter den inledande replikeringen. Den här förbättringen har stöd för utvecklingsarbetsflöden där konfigurationer behöver uppdateras och spridas över olika miljöer utan att hela sandlådekonfigurationen behöver återskapas. Mer information finns i guiden om [överföring av konfigurationsuppdateringar mellan sandlådor](../../sandboxes/ui/sandbox-tooling.md#move-configs). |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatering av tillgänglighetsinformation för lookalike-insikter | Insikter som liknar lookalike och lookalike-målgrupper inaktiveras automatiskt för miljöer som visar låg användning. Låg användning definieras som att inte visa lookalike-insikter de senaste tre månaderna eller att inte skapa en ny lookalike-målgrupp de senaste sex månaderna. Mer information om den här ändringen finns i [lookalike-målgruppsguiden](../../segmentation/types/lookalike-audiences.md). |

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} UI-stöd för [!DNL Azure Databricks] | Nu kan du ansluta ditt [!DNL Azure Databricks]-konto till Experience Platform med hjälp av källarbetsytan i användargränssnittet. Läs guiden om att [ansluta [!DNL Databricks] till Experience Platform i användargränssnittet](../../sources/connectors/databases/databricks.md) om du vill ha mer information. |
| Stöd för ny autentiseringstyp för [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] stöder nu även autentisering av tjänstens huvudnamn, utöver den befintliga autentiseringen av anslutningssträngen. Mer information finns i [[!DNL Azure Synapse Analytics] autentiseringsöversikten](../../sources/connectors/databases/synapse-analytics.md) |
| [!DNL Salesforce] - borttagning av grundläggande autentisering | Grundläggande autentisering för [Salesforce CRM](../../sources/connectors/crm/salesforce.md) och [Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md) kommer att vara inaktuellt i januari 2026. Kunder måste migrera till OAuth 2.0-autentisering för att kunna upprätthålla anslutningen. Den här ändringen påverkar både källanslutningar och säkerställer förbättrad säkerhet och överensstämmelse med Salesforce autentiseringsstandarder. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).
