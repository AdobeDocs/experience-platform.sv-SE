---
title: Experience Platform Pre-Release Notes
description: En förhandsgranskning av den senaste versionsinformationen för Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5cbf63cc0a149d54de63e3e1797cae4098498fe8
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 29%

---

# Information om förhandsversionen av Adobe Experience Platform

>[!IMPORTANT]
>
>Det här dokumentet är avsett som en **förhandsgranskning** av versionsinformationen för den aktuella månaden. Utgivningsobjekt kan ändras och kan läggas till eller tas bort i den slutliga versionen.

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/latest)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: mars 2026**

Nya funktioner och uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Hantering av avancerad datalivscykel](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Mål &#x200B;](#destinations)
- [Frågetjänst](#query-service)
- [Kundprofil i realtid](#profile)
- [Kör och använd](#run-and-operate)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Hantering av avancerad datalivscykel {#advanced-data-lifecycle-management}

Experience Platform har en rad funktioner för datahygien som gör att du kan hantera lagrade data genom att ta bort konsumentposter och datauppsättningar programmatiskt. Med hjälp av arbetsytan Data Lifecycle i användargränssnittet eller genom anrop till Data Hygiene API kan du hantera dina datalager på ett effektivt sätt. Använd dessa funktioner för att säkerställa att informationen används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationspolicyer anser det nödvändigt.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ta bort post för flera datauppsättningar och endast profiler (endast API) | Du kan skicka ett enstaka datauppsättnings-ID, en kommaavgränsad lista med datauppsättnings-ID:n eller literalen `ALL` i `datasetId` för att ta bort identiteter i en, flera eller alla datauppsättningar. Du kan även begränsa borttagningen till profiltjänster genom att ange `targetServices` till `["identity","profile","ajo"]`, vilket gör att data inte ändras. Mer information finns i guiden [Ta bort arbetsorder](../hygiene/api/workorder.md). |

{style="table-layout:auto"}

Mer information finns i [översikt över livscykelhantering för avancerade data](../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Med Agent Orchestrator kan ni bygga och driftsätta AI-baserade agenter som kan automatisera arbetsflöden och interagera med kunder över flera kanaler.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Adobe Marketing Agent för [!DNL Microsoft 365 Copilot] | Adobe Marketing Agent för [!DNL Microsoft 365 Copilot] är din inbäddade agent som samlar Adobe marknadsföringsinformation direkt i vanliga verktyg som [!DNL Teams], [!DNL Word], [!DNL PowerPoint] och andra [!DNL Microsoft 365]-appar. Du kan använda den här agenten för att hämta in betrodda kampanjinsikter från Adobe-program när du planerar kampanjer, granskar målgrupper eller samarbetar med kollegor, besvarar kundfrågor och fattar dataorienterade beslut utan att lämna ditt [!DNL Microsoft 365]-arbetsflöde. |

{style="table-layout:auto"}

Mer information finns i [Agent Orchestrator-dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [Snowflake Batch](../destinations/catalog/warehouses/snowflake-batch.md) - regionväljare | Nu är det enklare att hitta regionen med den nya sökbara listrutan som kombinerar sök- och listruta i en enda kontroll. |
| Exportera målgruppsmetadata till [Snowflake Batch](../destinations/catalog/warehouses/snowflake-batch.md)-mål | Filerna som exporteras till det här målet innehåller nu målgruppsmetadata. Den nya tabellstrukturen gäller för alla nya målanslutningar som ställs in framåt. Den gamla tabellstrukturen behålls i ytterligare tre månader innan den tas bort. |
| [!DNL Adobe Advertising Cloud DSP]-anslutning | Den nya Adobe Advertising DSP-anslutningen har samma funktionalitet som den gamla anslutningen plus stöd för ytterligare identiteter. |
| Externt målgruppsstöd för [Trade Desk CRM](../destinations/catalog/advertising/tradedesk-emails.md), [Villkor](../destinations/catalog/advertising/criteo.md) och [Pinterest](../destinations/catalog/advertising/pinterest.md) | Nu kan du aktivera målgrupper utanför segmenteringen för segmenteringstjänster för Trade Desk CRM, Criteo och Pinterest, inklusive anpassade uppladdningsmålgrupper (importerade från CSV), lookalike-målgrupper, federerade målgrupper och målgrupper skapade i andra Experience Platform-appar som Adobe Journey Optimizer. Mer information finns i avsnittet [målgrupper](../destinations/catalog/advertising/criteo.md#supported-audiences) som stöds på katalogsidan för varje mål. |
| Större gräns för anpassad överföring av målgrupper | Du kan nu aktivera upp till 20 anpassade uppladdningsmålgrupper per målinstans. Tidigare var gränsen 10. |
| [Exportera filen nu](../destinations/ui/export-file-now.md) och [API för ad hoc-aktivering](../destinations/api/ad-hoc-activation-api.md) har stöd för externa målgrupper | Nu kan du använda Export file now (UI) och ad hoc-aktiverings-API:t med externa målgrupper (som anpassad överföring, lookalike, federerad och målgrupper från andra Experience Platform-program) när du aktiverar batchfilbaserade mål. |
| HTTP API-mål med OAuth 2 och mTLS | Nu kan du skapa och autentisera HTTP API-mål som använder OAuth 2 när autentiseringsslutpunkten kräver gemensam TLS (mTLS). Token retrieval under målkonfigurationen har nu stöd för mTLS. |
| ZoomInfo-kontodestination | Nu kan du skicka kontomaterial till ZoomInfo från Real-Time Customer Data Platform (B2B). |

{style="table-layout:auto"}

**Korrigeringar och förbättringar**

| Korrigera | Beskrivning |
| --- | --- |
| [Verifiering av konto-ID för Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) | En validerare för reguljära uttryck har lagts till i steget för konto-ID. När du anger ditt ID valideras det nu för att säkerställa att organisations-ID och konto-ID har rätt format (avgränsat med en punkt). |
| Telefonnummer för [TikTok](../destinations/catalog/social/tiktok.md)-anslutning visas | Ett problem har korrigerats där en felkonfiguration på målkortet innebar att identiteter som är avaktiverade av telefonnummer inte aktiverades för TikTok. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../destinations/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tidsväljare för profilhändelser | Du kan nu ange ett tidsfönster på fliken Profilhändelser för att visa och analysera händelser inom det intervallet. Du kan ange tidsfönstret till upp till 30 dagar. Som standard visas händelser under de senaste 48 timmarna. |

{style="table-layout:auto"}

Mer information finns i [Översikten över kundprofil i realtid](../profile/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard SQL för att söka efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla samman alla datauppsättningar från [!DNL Data Lake] och samla in sökresultaten som en ny datauppsättning för användning i rapportering, arbetsytan för datavetenskap eller för inmatning i kundprofilen i realtid.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Data Distiller Accelerators | Du kan nu välja en accelerator på fliken Acceleratorer, ange de parametrar som krävs och köra eller schemalägga den genererade SQL-filen utan att behöva skriva den själv. Klona acceleratorn i en anpassad mall för att redigera den. |

{style="table-layout:auto"}

Mer information finns i [Översikt över frågetjänsten](../query-service/home.md).

## Kör och använd {#run-and-operate}

Inspektera, felsök och optimera era era Experience Platform-implementeringar med verktygen Kör och Kör. Få synlighet i schemalagda batchaktiveringar, identifiera konfigurationsproblem och förbättra systemets tillförlitlighet.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Jobbscheman](../run-and-operate/job-schedules.md) - allmän tillgänglighet | [!DNL Job Schedules] ger en enhetlig vy över alla schemalagda batchbearbetningsjobb i hela dataredjan, från inmatning till målaktivering. Kontrollera körningsstatus, identifiera schemaläggningskonflikter och diagnostisera konfigurationsproblem innan de påverkar din affärsverksamhet. |
| Allmän tillgänglighet för hälsokontroller | Dåliga schema- och identitetskonfigurationer leder till betydande problem längre fram i kedjan, bland annat felaktigt skapande av profiler, misslyckade segmentkvalificeringar och felaktig aktivering. <br>Hälsokontroller förändrar ditt tillvägagångssätt från reaktiv felsökning till proaktivt, förebyggande underhåll. Hälsokontroller är alltid inskannade av dina scheman och identiteter som används i din sandlåda och ger en sammanfattning av problem som du kan använda för att utforska och felsöka. |

{style="table-layout:auto"}

Mer information finns i översikten [Kör och använd](../run-and-operate/overview.md), [Granska jobbscheman](../run-and-operate/job-schedules.md) och [Plattformens gränssnittsguide](../landing/ui-guide.md).

## Segmenteringstjänst {#segmentation}

Med Experience Platform kan ni skapa målgruppssegment utifrån era kunddata, och ni får en komplett livscykelhantering för dessa målgrupper.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Inmatningskälla i Audience Builder | Nu kan du se om varje attribut kommer från en grupp, direktuppspelning eller edge-källa i Audience Builder för att undvika att skapa ogiltiga eller ineffektiva direktuppspelande målgrupper. |
| Visa endast fält med data i Audience Builder | Nu kan du filtrera så att bara attribut som innehåller data visas när du skapar kontomålgrupper. |

{style="table-layout:auto"}

Mer information finns i [Publiköversikt](../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| Förbättrat stöd för registrering av ändringsdata | Du kan nu använda registrering av ändringsdata med källorna [!DNL Marketo Engage], [!DNL Microsoft Dynamics] och [!DNL Salesforce CRM]. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../sources/home.md).

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) multiregion support | The Snowflake Streaming connector is now available to customers beyond the US VA7 region. Use the region dropdown selector to select which Snowflake region your account is in. The documentation has been updated with the expected data structure for Snowflake streaming tables. |
| Audience filtering in activation workflow | You can now find and filter audiences in the **[!UICONTROL Select audiences]** step with the same experience as the Audiences page; for example, you can filter on audience origin to easily find the audience you are looking for. |

-->