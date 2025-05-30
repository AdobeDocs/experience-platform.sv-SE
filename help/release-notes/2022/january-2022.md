---
title: Versionsinformation om Adobe Experience Platform januari 2022
description: Versionsinformationen för Adobe Experience Platform i januari 2022.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 25%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 januari 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Aviseringar](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Frågetjänst](#query-service)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika varningsregler via fliken [!UICONTROL Alerts] i Experience Platform användargränssnitt och du kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya varningsregler | Flera nya varningsregler finns nu tillgängliga för arbetsflöden som rör datainhämtning, identiteter, profiler, segmentering och aktivering. I översikten över [varningsregler](../../observability/alerts/rules.md) finns en uppdaterad lista över varningstyper. |
| Aviseringar i sitt sammanhang för källdataflöden | Du kan nu prenumerera för att få varningsmeddelanden om status för dina dataflöden under arbetsflödet för inmatning. Mer information finns i guiden om att [prenumerera på källvarningar i användargränssnittet](../../sources/tutorials/ui/alerts.md). |

Mer information om varningar i Experience Platform finns i [varningsöversikten](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

| Funktion | Beskrivning |
| --- | --- |
| Intelligenta bildtexter | En maskininlärningsalgoritm ger automatiskt insikter om profil- och målgruppsdata och illustrerar mönster och trender under en 30-90-dagars- eller 12-månadersperiod. Bildtexterna innehåller information om <ul><li>Generell form och statistik</li><li>Trender och plötsliga ändringar</li><li>Säsongsmönster</li><li>Oväntade avvikelser</li></ul> Mer information finns i dokumentationen för [profilpanelerna](../../dashboards/guides/profiles.md#profiles-count-trend) och [segmentpanelerna](../../dashboards/guides/audiences.md#audience-size-trend). |
| Instrumentpanelsinventering | Få tillgång till förkonfigurerade rapporter om profiler, segment och målpaneler, inklusive installerade integreringar som PowerBI, på en central plats. Mer information finns i [[!DNL Dashboards] lagerdokumentationen](../../dashboards/inventory.md). |
| PowerBI-rapportmallar | Bygg, anpassa eller utöka mätvärden från profil-, segment- och målrapporteringsdatamodeller med nya PowerBI-diagram. Det automatiserade installationsarbetsflödet gör att ni kan dela med er av era marknadsföringsinsikter i hela organisationen inifrån PowerBI-miljön. Mer information finns i [dokumentationen för PowerBI-rapportmallen](../../dashboards/integrations/power-bi.md). |

Mer information om [!DNL Dashboards] finns i [[!DNL Dashboards] översikten](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Konsoliderad kartläggning | Det nya mappningsgränssnittet i Experience Platform ger en konsekvent mappningsupplevelse så att du kan dra nytta av intelligenta mappningsrekommendationer, manuellt konfigurera mappningsregler och felsöka eventuella fel som inträffar i mappningsuppsättningarna. Mer information finns i [[!DNL Data Prep] gränssnittshandboken](../../data-prep/ui/mapping.md). |

Mer information om [!DNL Data Prep] finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| Personalisering på samma sida och nästa sida | Funktionen [&#128279;](../../destinations/ui/activate-edge-personalization-destinations.md) för anpassning av hela och nästa sida ger en delad, målvänlig vy över användare för program på Edge Network, för enhetlighet mellan marknadsföring och kundkanaler. Den här personaliseringen är möjlig genom [Adobe Target-anslutningen](../../destinations/catalog/personalization/adobe-target-connection.md) och [Anpassad personaliseringsanslutning](../../destinations/catalog/personalization/custom-personalization.md). Mer information om hur du konfigurerar personaliseringskampanjer på samma sida eller nästa sida finns i den [dedikerade självstudiekursen](../../destinations/ui/activate-edge-personalization-destinations.md). |
| Övervakning av batchdestinationer och segmentnivåstatistik | Funktionen för målövervakning har nu utökats från direktuppspelningsdestinationer till att även inkludera batchdestinationer och segmentnivåstatistik för era aktiveringsdata. Mer information finns i [Övervaka målinstrumentpanelen](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [Övervaka segmentjobbkontrollpanelen](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard) och [segmentnivåvyn](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Schemalägg redigering i användargränssnittet för befintliga batchaktiveringsdataflöden | Den här versionen innehåller ett alternativ för att redigera schemat för dina befintliga aktiveringsdataflöden till batchdestinationer. Mer information finns i [Aktivera profildata till gruppprofilsmål](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Förbättringar av Marketo-destinationer | Experience Platform-kunder som använder Marketo Engage kan maximera sin Marketo-databas med den nya möjligheten att överföra nya personposter till Marketo Engage från Experience Platform via [Marketo målanslutning](/help/destinations/catalog/adobe/marketo-engage.md). <br> När du skickar målgruppssegment från Experience Platform till Marketo Engage kan personer i segmentet som inte redan finns i din Marketo Engage-databas automatiskt läggas till i det. Mer information finns i [Push an Adobe Experience Platform Segment to a Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=sv-SE) (step 9 in the tutorial indicates how to push net-new person records into Marketo). |

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [Adobe Target-anslutning](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target är en applikation som innehåller AI-baserad personalisering och experimenterande i realtid i alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera. Adobe Target är en personaliseringsanslutning i Adobe Experience Platform. |
| [Anpassad personaliseringsanslutning](../../destinations/catalog/personalization/custom-personalization.md) | Med den här personaliseringsanslutningen kan du hämta segmentinformation från Adobe Experience Platform till externa personaliseringsplattformar, innehållshanteringssystem, annonsservrar och andra applikationer som körs på kundens webbplatser. |

För mer allmän information om mål, se [Översikt över mål](../../destinations/home.md).

## Frågetjänst {#query-service}

[!DNL Query Service] låter dig använda standard-SQL för att fråga efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla samman alla datauppsättningar från [!DNL Data Lake] och samla in sökresultaten som en ny datauppsättning för användning i rapportering, arbetsytan för datavetenskap eller för inmatning i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Anonymt block | Med den anonyma SQL-blockkonstruktionen kan du dela upp stora datapresentationsjobb i Query Service till mindre uppgifter och sedan återanvända och köra dem i sekvens för inkrementell datainläsning. Mer information finns i [exempelfrågorna för anonym blockdokumentation](../../query-service/key-concepts/anonymous-block.md). |
| Datauppsättningsorganisation | Tillhandahåller en sammanhängande, logisk datastruktur för att organisera dina dataresurser för användning med Query Service när mängden dataresurser i sandlådan växer. Mer information finns i [dokumentationen för att ordna dataresurser](../../query-service/best-practices/organize-data-assets.md). |

Mer information om [!DNL Query Service] finns i [[!DNL Query Service] översikten](../../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda Experience Platform-instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar i användargränssnittet för sandlådor | Sandlådeindikatorn är nu integrerad i huvudet för alla Experience Platform UI-program. Sandlådeindikatorn visar sandlådans namn, region och typ och gör det även möjligt att komma åt en listruta för att växla mellan sandlådor. Mer information finns i användargränssnittsguiden för [sandlådan](../../sandboxes/ui/user-guide.md). |

Mer information om sandlådor finns i översikten över [sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Segmentmatchning | Segmentmatchning är en tjänst för datasamarbete som gör det möjligt för två eller flera Experience Platform-användare att utbyta data, baserat på gemensamma identifierare, på ett säkert, styrt och sekretessvänligt sätt. Segment Match använder Experience Platform sekretessstandarder och personliga identifierare som hash-kodade e-postmeddelanden, hashade telefonnummer och enhetsidentifierare som IDFA och GAID. Mer information finns i översikten [Segmentmatchning](../../segmentation/ui/segment-match/overview.md). |

Mer information om [!DNL Segmentation Service] finns i [segmenteringsöversikten](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

| Funktion | Beskrivning |
| --- | --- |
| Beta-källor som övergår till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] källförbättringar | Källan [!DNL Event Hubs] har nu stöd för SAS-nyckeltyper som inte är rot för autentisering för att ansluta och skapa en källanslutning. Mer information finns i [[!DNL Event Hubs] översikten](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] källförbättringar | Med källan [!DNL SFTP] kan du nu skapa ett angivet antal samtidiga anslutningar som ett dataflöde kan använda för att ansluta till SFTP-servern. Mer information finns i [[!DNL SFTP] översikten](../../sources/connectors/cloud-storage/sftp.md). |
