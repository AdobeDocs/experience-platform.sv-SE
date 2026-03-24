---
title: Versionsinformation om Adobe Experience Platform mars 2026
description: Versionsinformationen för Adobe Experience Platform i mars 2026.
source-git-commit: d7415a9deefac55b8583eb52a7c1f18caf5f3334
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 35%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/latest)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 24 mars 2026**

Nya funktioner och uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Hantering av avancerad datalivscykel](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Källor](#sources)

## Hantering av avancerad datalivscykel {#advanced-data-lifecycle-management}

Experience Platform har en rad funktioner för datahygien som gör att du kan hantera lagrade data genom att ta bort konsumentposter och datauppsättningar programmatiskt. Du kan hantera dina datalager effektivt med hjälp av arbetsytan Datalängd i användargränssnittet eller anrop till API:t för datahygien. Använd dessa funktioner för att säkerställa att informationen används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationspolicyer anser det nödvändigt.

| Funktion | Beskrivning |
| --- | --- |
| Borttagning av post för flera datauppsättningar och endast profiler (endast API) | Du kan skicka ett enstaka datauppsättnings-ID, en kommaavgränsad lista med datauppsättnings-ID:n eller literalen `ALL` i `datasetId` för att ta bort identiteter i en, flera eller alla datauppsättningar. Du kan även begränsa borttagning till profilrelaterade tjänster genom att ange `targetServices` till `["identity","profile","ajo"]`, vilket lämnar datalagret oförändrat. Den här funktionen är bara tillgänglig via API:t för datahygien. Mer information finns i guiden [Ta bort arbetsorder](../../hygiene/api/workorder.md). |

{style="table-layout:auto"}

Mer information finns i [översikt över livscykelhantering för avancerade data](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Med Agent Orchestrator kan ni bygga och driftsätta AI-baserade agenter som kan automatisera arbetsflöden och interagera med kunder över flera kanaler.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Adobe Marketing Agent för [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent för [!DNL Microsoft 365 Copilot] är din inbäddade agent som samlar Adobe marknadsföringsinformation direkt i vanliga verktyg som [!DNL Teams], [!DNL Word], [!DNL PowerPoint] och andra [!DNL Microsoft 365]-appar. Du kan använda den här agenten för att hämta in betrodda kampanjinsikter från Adobe-program medan du planerar kampanjer, granskar målgrupper, samarbetar med kollegor för att besvara kundfrågor och fatta dataorienterade beslut utan att lämna ditt [!DNL Microsoft 365]-arbetsflöde. |

{style="table-layout:auto"}

Mer information finns i [dokumentationen om Agent Orchestrator](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md)-anslutning | Den nya Adobe Advertising DSP-anslutningen har samma funktionalitet som den gamla anslutningen plus stöd för ytterligare identiteter. Med den nya kopplingen kan du också exportera cookie-baserade identiteter till Adobe Advertising DSP. |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md)-anslutning | Skicka [!DNL Real-Time CDP] målgrupper till FreeWheel som dagliga batchfiler så att du kan rikta in dem i FreeWheel-erbjudanden och -kampanjer för CTV, video och displayen. Kontakta ditt Adobe-kontoteam för att få åtkomst. |
| Stöd för externa målgrupper för [Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) och [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Du kan nu aktivera målgrupper från ursprungsland till inte bara segmenteringstjänsten, till Trade Desk CRM, Criteo och Pinterest, inklusive anpassade uppladdningsmålgrupper (som importerats från CSV), lookalike-målgrupper, federerade målgrupper och målgrupper som skapats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer]. Uppdateringen lanseras i slutet av mars. Mer information finns i avsnittet [målgrupper](../../destinations/catalog/advertising/criteo.md#supported-audiences) som stöds på katalogsidan för varje mål. |
| Ökad gräns för anpassad uppladdning av mottagare | Du kan nu aktivera upp till 20 anpassade uppladdningsmålgrupper per målinstans. Tidigare var gränsen 10. Mer information finns i [målskyddsjournalerna](../../destinations/guardrails.md#batch-file-based-activation). |
| [Exportera filen nu](../../destinations/ui/export-file-now.md) och [API för ad hoc-aktivering](../../destinations/api/ad-hoc-activation-api.md) har stöd för externa målgrupper | Nu kan du använda Export file now (UI) och ad hoc-aktiverings-API:t med externa målgrupper (som anpassad överföring, lookalike, federerad och målgrupper från andra Experience Platform-program) när du aktiverar batchfilbaserade mål. Uppdateringen lanseras i slutet av mars. |

{style="table-layout:auto"}

**Korrigeringar och förbättringar**

| Korrigera | Beskrivning |
| --- | --- |
| Telefonnummer för [TikTok](../../destinations/catalog/social/tiktok.md)-anslutning visas | Ett problem har korrigerats där en felkonfiguration på målkortet innebar att identiteter som är avaktiverade av telefonnummer inte aktiverades för TikTok. Om du vill använda den här korrigeringen skapar du ett nytt aktiveringsflöde eller tar bort telefonnummermappningen från ditt befintliga flöde, sparar den och lägger sedan tillbaka den igen. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

| Funktion | Beskrivning |
| --- | --- |
| XDM-entitetsåtgärder och borttagningsstöd | Få åtkomst till åtgärder för scheman, klasser, fältgrupper och datatyper direkt från inline-tabellmenyer och rubrikmenyer för detaljsidor. Om du har de behörigheter som krävs kan du även ta bort organisationens enheter när de inte används av datauppsättningar och inte är aktiverade för profil. Mer information finns i [gränssnittshandboken för XDM](../../xdm/ui/explore.md). |

Mer information finns i [XDM-översikten](../../xdm/home.md).

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## Källor

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| [!DNL Talon.One] | Nu kan du ansluta Experience Platform till [!DNL Talon.One] med de nya källorna [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) och [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md). Använd de nya källorna för att importera data om lojalitetsprofiler samt transaktioner- och lojalitetshändelser till Experience Platform. |
| Nya IP-adresser att tillåtslista | Nya IP-adresser för GBR9: Storbritannien har lagts till i listan med adresser som du måste tillåtslista för att batchkällanslutningarna till Experience Platform på Azure ska lyckas. Visa listan i guiden [IP-adress till tillåtelselista](../../sources/ip-address-allow-list.md#gbr9-united-kingdom) om du vill ha mer information. |
| Förbättrat stöd för registrering av ändringsdata | Du kan nu använda registrering av ändringsdata med källorna [!DNL Marketo Engage], [!DNL Microsoft Dynamics] och [!DNL Salesforce CRM]. |
| Förbättrad autentiseringsguide för [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | Autentiseringsguiden för källan [!DNL Google BigQuery] har utökats med följande information: <ul><li>De scope som krävs för uppdateringstoken.</li><li>IAM-rollerna som krävs för identiteten [!DNL Google].</li><li>Ytterligare vägledning om hur du använder `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->