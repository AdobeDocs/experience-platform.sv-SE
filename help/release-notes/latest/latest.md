---
title: Versionsinformation om Adobe Experience Platform mars 2026
description: Versionsinformationen för Adobe Experience Platform i mars 2026.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4f4761024a658d284f3eacdc2230e868c6ee53fb
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 20%

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
- [Dataströmmar](#datastreams)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Kundprofil i realtid](#real-time-customer-profile)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Hantering av avancerad datalivscykel {#advanced-data-lifecycle-management}

Experience Platform har en rad olika funktioner för datahygien som hjälper dig att hantera lagrade data genom att programmatiskt ta bort konsumentposter och datauppsättningar. Du kan hantera dina datalager effektivt med hjälp av arbetsytan Datalängd i användargränssnittet eller anrop till API:t för datahygien. Använd dessa funktioner för att säkerställa att informationen används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationspolicyer anser det nödvändigt.

| Funktion | Beskrivning |
| --- | --- |
| Borttagning av post för flera datauppsättningar och endast profiler (endast API) | Du kan skicka ett enstaka datauppsättnings-ID, en kommaavgränsad lista med datauppsättnings-ID:n eller literalen `ALL` i `datasetId` för att ta bort identiteter i en, flera eller alla datauppsättningar. Du kan även begränsa borttagning till profilrelaterade tjänster genom att ange `targetServices` till `["identity","profile","ajo"]`, vilket lämnar datalagret oförändrat. Den här funktionen är bara tillgänglig via API:t för datahygien. Mer information finns i guiden [Ta bort arbetsorder](../../hygiene/api/workorder.md). |

{style="table-layout:auto"}

Mer information finns i [översikt över livscykelhantering för avancerade data](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Använd Agent Orchestrator för att bygga och driftsätta AI-baserade agenter som automatiserar arbetsflöden och interagerar med kunder i flera kanaler.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Adobe Marketing Agent för [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent för [!DNL Microsoft 365 Copilot] är din inbäddade agent som samlar Adobe marknadsföringsinformation direkt i vanliga verktyg som [!DNL Teams], [!DNL Word], [!DNL PowerPoint] och andra [!DNL Microsoft 365]-appar. Du kan använda den här agenten för att hämta in betrodda kampanjinsikter från Adobe-program medan du planerar kampanjer, granskar målgrupper, samarbetar med kollegor för att besvara kundfrågor och fatta dataorienterade beslut utan att lämna ditt [!DNL Microsoft 365]-arbetsflöde. |

{style="table-layout:auto"}

Mer information finns i [dokumentationen om Agent Orchestrator](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Dataströmmar {#datastreams}

En datastream representerar konfigurationen på serversidan när Adobe Experience Platform Web och Mobile SDK implementeras och Adobe Experience Platform Edge Network Server API. Datastream-konfigurationskommandot i SDK:n hanterar alla tjänster som en klient interagerar med.

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för dynamiska datastream-konfigurationer | Dynamiska datastream-konfigurationer är nu allmänt tillgängliga. Med dynamiska datastream-konfigurationer kan du definiera användarkonfigurerbara regeluppsättningar för varje tjänst som är aktiverad för din datastream, som avgör vilken Experience Cloud-lösning som ska ta emot varje typ av data. Mer information finns i [guiden för dynamiska datastream-konfigurationer](../../datastreams/configure-dynamic-datastream.md). |

{style="table-layout:auto"}

Mer information finns i [datastreams-översikten](../../datastreams/overview.md).

## Mål {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar. Använd destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) - regionväljare | Nu är det enklare att hitta regionen med den nya sökbara listrutan som kombinerar sök- och listruta i en enda kontroll. Uppdateringen lanseras i slutet av mars. |
| Ny tabellstruktur för [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md)-mål | Tabeller som delas med ditt Snowflake-konto har nu en ny struktur som innehåller separata kolumner för målgruppsnamn och målgruppernas ursprung. Den nya tabellstrukturen gäller för alla nya målanslutningar som ställs in framåt. För nya anslutningar som du skapar skapas båda tabellstrukturerna: den nya strukturen har prefixet V2 och den gamla strukturen behålls till slutet av juni 2026, varefter den kommer att bli inaktuell. Läs mer i avsnittet [Exporterade data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) i dokumentationen för Snowflake Batch. Uppdateringen lanseras i slutet av mars. |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md)-anslutning | Den nya Adobe Advertising DSP-anslutningen har samma funktionalitet som den gamla anslutningen plus stöd för ytterligare identiteter. Med den nya kopplingen kan du också exportera cookie-baserade identiteter till Adobe Advertising DSP. |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md)-anslutning | Skicka [!DNL Real-Time CDP] målgrupper till FreeWheel som dagliga batchfiler så att du kan rikta in dem i FreeWheel-erbjudanden och -kampanjer för CTV, video och displayen. Kontakta ditt Adobe-kontoteam för att få åtkomst. |
| Stöd för externa målgrupper för [Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) och [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Du kan nu aktivera målgrupper från ursprungsland till inte bara segmenteringstjänsten, till Trade Desk CRM, Criteo och Pinterest, inklusive anpassade uppladdningsmålgrupper (som importerats från CSV), lookalike-målgrupper, federerade målgrupper och målgrupper som skapats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer]. Uppdateringen lanseras i slutet av mars. Mer information finns i avsnittet [målgrupper](../../destinations/catalog/advertising/criteo.md#supported-audiences) som stöds på katalogsidan för varje mål. |
| Ökad gräns för anpassad uppladdning av mottagare | Du kan nu aktivera upp till 20 anpassade uppladdningsmålgrupper per målinstans. Tidigare var gränsen 10. Mer information finns i [målskyddsjournalerna](../../destinations/guardrails.md#batch-file-based-activation). |
| [Exportera filen nu](../../destinations/ui/export-file-now.md) och [API för ad hoc-aktivering](../../destinations/api/ad-hoc-activation-api.md) har stöd för externa målgrupper | Nu kan du använda Export file now (UI) och ad hoc-aktiverings-API:t med externa målgrupper (som anpassad överföring, lookalike, federerad och målgrupper från andra Experience Platform-program) när du aktiverar batchfilbaserade mål. Uppdateringen lanseras i slutet av mars. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) -mål med OAuth 2 och mTLS | Nu kan du skapa och autentisera HTTP API-mål som använder OAuth 2 när autentiseringsslutpunkten kräver gemensam TLS (mTLS). Token retrieval under målkonfigurationen har nu stöd för mTLS. Uppdateringen lanseras i slutet av mars. |

{style="table-layout:auto"}

**Korrigeringar och förbättringar**

| Korrigera | Beskrivning |
| --- | --- |
| Telefonnummer för [TikTok](../../destinations/catalog/social/tiktok.md)-anslutning visas | Ett problem har korrigerats där en felkonfiguration på målkortet innebar att identiteter som är avaktiverade av telefonnummer inte aktiverades för TikTok. Om du vill använda den här korrigeringen skapar du ett nytt aktiveringsflöde eller tar bort telefonnummermappningen från ditt befintliga flöde, sparar den och lägger sedan tillbaka den igen. |
| [Verifiering av konto-ID för Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) och [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) | En validerare för reguljära uttryck har lagts till i steget för konto-ID. När du anger ditt ID valideras det nu för att säkerställa att organisations-ID och konto-ID har rätt format (avgränsat med en punkt). Uppdateringen lanseras i slutet av mars. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

| Funktion | Beskrivning |
| --- | --- |
| XDM-entitetsåtgärder och borttagningsstöd | Få åtkomst till åtgärder för scheman, klasser, fältgrupper och datatyper direkt från inline-tabellmenyer och rubrikmenyer för detaljsidor. Om du har de behörigheter som krävs kan du även ta bort organisationens enheter när de inte används av datauppsättningar och inte är aktiverade för profil. Mer information finns i [gränssnittshandboken för XDM](../../xdm/ui/explore.md). |

Mer information finns i [XDM-översikten](../../xdm/home.md).

## Kundprofil i realtid {#real-time-customer-profile}

Med kundprofilen i realtid får ni en fullständig bild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Använd Profil för att konsolidera era kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Händelser | Du kan nu ange uppslagsperiod för händelser när du bläddrar bland dina profiler. Detta gör att du kan se de händelser som profilen är kopplad till under den angivna tidsperioden. Mer information finns i [Användargränssnittsguiden för profil](../../profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Mer information finns i [[!DNL Real-Time Customer Profile] översikten](../../profile/home.md).

## Kör och använd {#run-and-operate}

Inspektera, felsök och optimera era era Experience Platform-implementeringar med verktygen Kör och Kör. Få synlighet i schemalagda batchaktiveringar, identifiera konfigurationsproblem och förbättra systemets tillförlitlighet.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Jobbscheman](../../run-and-operate/job-schedules.md) - allmän tillgänglighet | [!DNL Job Schedules] ger en enhetlig vy över alla schemalagda batchbearbetningsjobb i hela dataredjan, från inmatning till målaktivering. Kontrollera körningsstatus, identifiera schemaläggningskonflikter och diagnostisera konfigurationsproblem innan de påverkar din affärsverksamhet. |
| [Hälsokontroller](../../run-and-operate/health-checks.md) allmän tillgänglighet | Dåliga schema- och identitetskonfigurationer leder till betydande problem längre fram i kedjan, bland annat felaktigt skapande av profiler, misslyckade segmentkvalificeringar och felaktig aktivering. <br>Hälsokontroller förändrar ditt tillvägagångssätt från reaktiv felsökning till proaktivt, förebyggande underhåll. Hälsokontroller är alltid inskannade av dina scheman och identiteter som används i din sandlåda och ger en sammanfattning av problem som du kan använda för att utforska och felsöka. |

{style="table-layout:auto"}

Mer information finns i översikten [Kör och använd](../../run-and-operate/overview.md), [Granska jobbscheman](../../run-and-operate/job-schedules.md) och [Plattformens gränssnittsguide](../../landing/ui-guide.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Inmatningstyp | Nu kan du visa attributens insatstyp. På så sätt kan ni känna till informationens ursprung, så att ni kan skapa bättre målgrupper. Mer information om den här funktionen finns i [guiden för segmentbyggaren](../../segmentation/ui/segment-builder.md). |
| Sammanfattningsdata | Nu kan du visa sammanfattningsdata för dina attribut för konto- och personbaserade målgrupper. Mer information om den här funktionen finns i [Audience Builder-handboken](../../rtcdp/segmentation/audience-builder.md) för kontot. Mer information om den här funktionen hos personbaserade målgrupper finns i [guiden för segmentbyggaren](../../segmentation/ui/segment-builder.md). |

Mer information finns i [[!DNL Segmentation Service] översikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Använd de här källanslutningarna för att autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tidpunkter för intag och hantera dataöverföringshastighet.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| [!DNL Talon.One] | Nu kan du ansluta Experience Platform till [!DNL Talon.One] med de nya källorna [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) och [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md). Använd de nya källorna för att importera data om lojalitetsprofiler samt transaktioner- och lojalitetshändelser till Experience Platform. |
| Nya IP-adresser att tillåtslista | Nya IP-adresser för GBR9: Storbritannien har lagts till i listan med adresser som du måste tillåtslista för att batchkällanslutningarna till Experience Platform på Azure ska lyckas. Visa listan i guiden [IP-adress till tillåtelselista](../../sources/ip-address-allow-list.md#gbr9-united-kingdom) om du vill ha mer information. |
| Förbättrat stöd för registrering av ändringsdata | Du kan nu använda registrering av ändringsdata med källorna [!DNL Marketo Engage], [!DNL Microsoft Dynamics] och [!DNL Salesforce CRM]. |
| Förbättrad autentiseringsguide för [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | Autentiseringsguiden för källan [!DNL Google BigQuery] har utökats med följande information: <ul><li>De scope som krävs för uppdateringstoken.</li><li>IAM-rollerna som krävs för identiteten [!DNL Google].</li><li>Ytterligare vägledning om hur du använder `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).
