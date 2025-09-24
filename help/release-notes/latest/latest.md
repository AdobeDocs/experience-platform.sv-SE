---
title: Versionsinformation om Adobe Experience Platform för augusti 2025
description: Versionsinformation för augusti 2025 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e21381f2683070fdbf24c473fa6794b89160864b
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 43%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 23 september 2025**

Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Aviseringar](#alerts)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator är det nya agakta lagret i Adobe Experience Platform.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator är det nya agakta lagret i Adobe Experience Platform. Experience Platform Agent Orchestrator är utformat för att utnyttja plattformens omfattande data och kundupplevelser och driver intelligens och resonemang bakom specialbyggda Adobe Experience Platform-agenter som gör det möjligt för dem att fatta komplexa beslut och lösa problem snabbt och i stor skala - allt med mänsklig tillsyn. När du ställer frågor eller begär hjälp via ett naturligt språk i ett konversationsgränssnitt som AI Assistant, uppmanar Agent Orchestrator automatiskt våra specialistrepresentanter att ge dig rätt svar. Agent Orchestrator kommer ihåg er konversationshistorik, vilket gör att ni kan bygga vidare på tidigare frågor på ett naturligt sätt utan att behöva upprepa sammanhanget, och kombinerar insikter från olika agenter för att ge er tydliga, enhetliga svar. Mer information finns i [Agent Orchestrator-dokumentationen](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). |
| Audience Agent | Med Audience Agent kan ni visa insikter om målgrupper, inklusive att identifiera betydande förändringar av målgruppsstorlek, identifiera duplicerade målgrupper, utforska ert målgruppslager och ta fram era målgruppers storlek. Mer information finns i [Audience Agent-dokumentationen](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Mer information finns i [Agent Orchestrator-dokumentationen](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/home).

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aviseringar om inhämtning av strömmande profiler | Du kan nu prenumerera på två nya aviseringar för direktuppspelning på en dataflödesnivå: <ul><li>Felfrekvens för direktuppspelningsinmatning överskreds</li><li>Överhoppad frekvens för direktuppspelningsinmatning överskreds</li></ul> Varningar på plattformen eller via e-post meddelar dig när tröskelvärdena överskrids för standardtröskelvärdet, eller när du anger ett anpassat tröskelvärde. Mer information finns i guiden [Profilaviseringar](../../observability/alerts/rules.md#profile). |

{style="table-layout:auto"}

Mer information om aviseringar finns i avsnittet [[!DNL Observability Insights] översikt](../../observability/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md)-anslutning | En ny [!DNL Snowflake Batch]-anslutning är nu tillgänglig som ett alternativ till direktuppspelningsanslutaren för specifika användningsfall. |
| Krypteringsstöd för [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Nu kan du bifoga RSA-formaterade offentliga nycklar för att kryptera dina exporterade filer, vilket ger dig samma säkerhetsnivå som andra molnlagringsplatser tillhandahåller för din känsliga information. |
| Information om förfallodatum för autentisering för [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) mål | Information om förfallotid för autentisering för [!DNL Pinterest]-destinationer visas nu direkt i Experience Platform-gränssnittet, så du kan se när din autentisering kommer att upphöra och förnya den innan den orsakar eventuella avbrott i dataflödena. Du kan övervaka förfallotiden för dina tokens från kolumnen **[!UICONTROL Account expiration date]** på flikarna **[[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts)** eller **[[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrade funktioner för destinationshantering i Experience Platform UI | Förbättra arbetsflödet för målhantering med nya sorteringsfunktioner på flikarna [[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse) och [[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts). Nu kan du även se en visuell indikator när din kontoautentisering håller på att gå ut. <br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| Inställningar för beständig kolumnbredd | Inställningarna för kolumnbredd behålls nu när du navigerar bort från en sida och återgår till den. Om du till exempel justerar en kolumnbredd på fliken [[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse) ändras inte den anpassade kolumnbredden när du navigerar bort och återgår till den fliken. |

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Modellbaserade scheman | Förenkla datamodelleringen med modellbaserade scheman. Nu kan du lättare skapa scheman tack vare många exempel och guider. Den här funktionen är för närvarande tillgänglig för innehavare av Campaign Orchestration-licenser och kommer att utvidgas till att omfatta Data Distiller-kunder på GA, vilket gör datamodelleringen mer tillgänglig och effektiv. Funktionen har stöd för tidsseriedata och funktioner för datainhämtning vid ändring. |

Mer information finns i [XDM-översikten](../../xdm/home.md).
<!--

| Data Mirror | Ingest row-level changes from cloud data warehouses (e.g., Snowflake, Databricks, BigQuery) into Adobe Experience Platform using model-based schemas. Data Mirror eliminates upstream ETL and preserves relationships, versioning, and deletions by mirroring existing database structures directly into the data lake. Time-series and record event schema behavior with change data capture capabilities are all supported. This feature is currently available for Campaign Orchestration license holders and will expand through this limited release, also including Customer Journey Analytics customers. See the [Data Mirror documentation](../../xdm/data-mirror/overview.md) for more details. Contact your Adobe representative for access. |
-->

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid får du en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online, offline, CRM och data från tredje part. Med profilen kan du konsolidera kunddata till en enhetlig vy som ger en handlingsbar, tidsstämplad redogörelse för varje kundinteraktion.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av profilvisningsprogram | Septemberversionen 2025 innehåller följande förbättringar av profilvisningsprogrammet. <ul><li>**Kombinerad vy**: Attribut, händelser och insikter har kombinerats till en enda vy.</li><li>**AI-genererade insikter**: Sidan med profilinformation visar nu AI-genererade insikter, som visar information som genererats från din profil. Dessa insikter kan innehålla information som benägenhetspoäng och trendanalyser.</li><li>**Formatuppdatering**: Sidan med profilinformation har uppdaterats visuellt.</li><li>**Bläddra**: Nu kan du utforska dina profiler via en interaktiv kortbaserad karusell med sökning och anpassning.</li></ul> |

Mer information finns i [Översikt över kundprofilen i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Kontomålgrupper med borttagning av upplevelsehändelser | Efter uppgraderingen av B2B-arkitekturen stöds inte längre kontomålgrupper med upplevelsehändelser. Använd i stället den nya segmentmetoden: skapa en publik med Experience Events och hänvisa sedan till den målgruppen när du skapar en Account Audience. Detta ger en mer flexibel och underhållande metod för att skapa B2B-målgrupper. |

**Viktiga uppdateringar**

| Uppdatering | Beskrivning |
| ------- | ----------- |
| Målgruppsuppskattningar återställer automatiskt | Förbättringen av den automatiska uppdateringen för målgruppsuppskattningar har återställts. Målgruppsuppskattningar kommer även i fortsättningen att genereras i Segment Builder, men funktionen för automatisk uppdatering har tagits bort. |
| Extern publik | Från och med den 30 september hämtas externa målgrupper via Unified Search i Segment Builder. Om du använder segmentmatchning kan du aktivera den gamla funktionen i Segment Builder. |

Mer information finns i [[!DNL Segmentation Service] översikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya källor i allmän tillgänglighet | Följande källor är nu allmänt tillgängliga: Flera källanslutningar har uppdaterats från Beta till GA: <ul><li>[Acxiom-datainmatning](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acxiom Prospect Data Inghit](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. De här källorna stöds nu fullt ut och är klara för produktion. |
| [!DNL Snowflake] autentiseringsstöd för nyckelpar | Förbättrad säkerhet för Snowflake-anslutningar med stöd för autentisering med nyckelpar. Grundläggande autentisering (användarnamn/lösenord) kommer att vara inaktuellt i november 2025, så kunder uppmuntras att migrera till nyckelpars autentisering för att få bättre säkerhet. Mer information finns i [[!DNL Snowflake] dokumentationen](../../sources/connectors/databases/snowflake.md). |
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | Använd [[!DNL Capillary Streaming Events] source](../../sources/connectors/loyalty/capillary.md) för att strömma bonusdata från ditt [!DNL Capillary]-konto till Experience Platform. |
| Allmän tillgänglighet för stöd för privata länkar i källor | Du kan nu använda **privata länkar** för en vald grupp källor. Använd den här funktionen för att skapa en privat slutpunkt som källan kan ansluta till. Med privata slutpunkter kan du skapa anslutningar och dataflöden som kringgår det offentliga Internet, vilket ger förbättrad säkerhet och nätverksisolering för dina känsliga data. Stöd för privata länkar finns för följande källor: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>. Mer information finns i handböckerna om hur du skapar privata länkar [ i API:t ](../../sources/tutorials/api/private-link.md) och [ i gränssnittet](../../sources/tutorials/ui/private-link.md). |

Mer information finns i [översikten över källor](../../sources/home.md).
