---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
exl-id: bcd52989-ef62-4ab9-866e-1d9e57b76a0c
source-git-commit: 8a26a69e6a244fc8a0d347e2814f0406713b1c9b
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 januari 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Larm](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Destinations]](#destinations)
- [Frågetjänst](#query-service)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Larm {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika plattformsaktiviteter. Du kan prenumerera på olika varningsregler via [!UICONTROL Alerts] -fliken i användargränssnittet för plattformen och kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya varningsregler | Flera nya varningsregler finns nu tillgängliga för arbetsflöden som rör datainhämtning, identiteter, profiler, segmentering och aktivering. Se översikten på [varningsregler](../../observability/alerts/rules.md) för den uppdaterade listan över varningstyper. |
| Aviseringar i sitt sammanhang för källdataflöden | Du kan nu prenumerera för att få varningsmeddelanden om status för dina dataflöden under arbetsflödet för inmatning. Mer information finns i handboken på [prenumerera på källvarningar i användargränssnittet](../../sources/tutorials/ui/alerts.md). |

Mer information om varningar i Platform finns i [varningsöversikt](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform har flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har tagits med vid dagliga ögonblicksbilder.

| Funktion | Beskrivning |
| --- | --- |
| Intelligenta bildtexter | En maskininlärningsalgoritm ger automatiskt insikter om profil- och målgruppsdata och illustrerar mönster och trender under en 30-90-dagars- eller 12-månadersperiod. Bildtexterna innehåller information om <ul><li>Generell form och statistik</li><li>Trender och plötsliga ändringar</li><li>Säsongsmönster</li><li>Oväntade avvikelser</li></ul> Mer information finns på [profiler dashboards](../../dashboards/guides/profiles.md#profiles-count-trend) och [instrumentpaneler för segment](../../dashboards/guides/segments.md#audience-size-trend) dokumentation. |
| Instrumentpanelsinventering | Få tillgång till förkonfigurerade rapporter om profiler, segment och målpaneler, inklusive installerade integreringar som PowerBI, på en central plats. Mer information finns i [[!DNL Dashboards] översikt](../../dashboards/home.md). |
| PowerBI-rapportmallar | Bygg, anpassa eller utöka mätvärden från profil-, segment- och målrapporteringsdatamodeller med nya PowerBI-diagram. Det automatiserade installationsarbetsflödet gör att ni kan dela med er av era marknadsföringsinsikter i hela organisationen inifrån PowerBI-miljön. Mer information finns i [[!DNL Dashboards] översikt](../../dashboards/home.md). |

Mer information om [!DNL Dashboards], se [[!DNL Dashboards] översikt](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Konsoliderad kartläggning | Det nya mappningsgränssnittet i plattformsgränssnittet ger en konsekvent mappningsupplevelse så att du kan dra nytta av intelligenta mappningsrekommendationer, manuellt konfigurera mappningsregler och felsöka eventuella fel som inträffar i mappningsuppsättningarna. Mer information finns i [[!DNL Data Prep] Användargränssnittsguide](../../data-prep/ui/mapping.md). |

Mer information om [!DNL Data Prep], se [[!DNL Data Prep] översikt](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| Personalisering på samma sida och nästa sida | Personaliseringsfunktionen på samma sida och nästa sida ger en delad, målinriktad vy över användare för program på Experience Edge, för enhetlighet mellan marknadsföring och kundkanaler. Den här personaliseringen är möjlig genom [Adobe Target-anslutning](../../destinations/catalog/personalization/adobe-target-connection.md) och [Anpassad personaliseringsanslutning](../../destinations/catalog/personalization/custom-personalization.md). Information om hur du konfigurerar personaliseringskampanjer på samma sida eller nästa sida finns i [dedikerad självstudiekurs](../../destinations/ui/configure-personalization-destinations.md). |
| Förbättringar av Marketo-destinationer | Experience Platform-kunder som använder Marketo Engage kan maximera sin Marketo-databas med den nya möjligheten att föra över nya personposter till Marketo Engage från Experience Platform via [Marketo destinationskontakt](/help/destinations/catalog/adobe/marketo-engage.md). När du skickar målgruppssegment från Experience Platform till Marketo Engage kan personer i segmentet som inte redan finns i Marketo Engage-databasen automatiskt läggas till i det. Mer information finns i [Överför ett Adobe Experience Platform-segment till en Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (steg 9 i självstudiekursen visar hur du överför nya personposter till Marketo). |

<!--

| Feature | Description |
| ----------- | ----------- |
| Batch destination monitoring and segment-level metrics | The destination monitoring functionality is now expanded from streaming destinations to also include batch destinations and segment-level metrics for your activation dataflows. For more information, read monitoring destinations dashboard, monitoring segment jobs dashboard, and segment-level view. |
| Schedule editing in the UI for existing batch activation dataflows | This release introduces the option to edit the schedule of your existing activation dataflows to batch destinations. For more information, read [activate profile data to batch profile destinations](/help/destinations/ui/activate-batch-profile-destinations.md).  |

-->

**Nya destinationer**

| Destination | Beskrivning |
| ----------- | ----------- |
| [Adobe Target-anslutning](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target är en applikation som innehåller AI-baserad personalisering och experimenterande i realtid i alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera. Adobe Target är en personaliseringsanslutning i Adobe Experience Platform. |
| [Anpassad personaliseringsanslutning](../../destinations/catalog/personalization/custom-personalization.md) | Med den här personaliseringsanslutningen kan du hämta segmentinformation från Adobe Experience Platform till externa personaliseringsplattformar, innehållshanteringssystem, annonsservrar och andra applikationer som körs på kundens webbplatser. |

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Frågetjänst {#query-service}

[!DNL Query Service] låter dig använda standard-SQL för att fråga efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, datavetenskapen eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Anonymt block | Med den anonyma SQL-blockkonstruktionen kan du dela upp stora datapresentationsjobb i Query Service till mindre uppgifter och sedan återanvända och köra dem i sekvens för inkrementell datainläsning. Mer information finns i [Översikt över frågetjänsten](../../query-service/home.md). |
| Datauppsättningsorganisation | Tillhandahåller en sammanhängande, logisk datastruktur för att organisera dina dataresurser för användning med Query Service när mängden dataresurser i sandlådan växer. Mer information finns i [Översikt över frågetjänsten](../../query-service/home.md). |

Mer information om [!DNL Query Service], se [[!DNL Query Service] översikt](../../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar i användargränssnittet för sandlådor | Sandlådeindikatorn är nu integrerad i huvudet för alla plattformsgränssnittsprogram. Sandlådeindikatorn visar sandlådans namn, region och typ och gör det även möjligt att komma åt en listruta för att växla mellan sandlådor. Mer information finns i [gränssnittshandbok för sandlådor](../../sandboxes/ui/user-guide.md). |

Mer information om sandlådor finns i [översikt över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Segmentmatchning | Segmentmatchning är en tjänst för datasamarbete som gör det möjligt för två eller flera plattformsanvändare att utbyta data, baserat på gemensamma identifierare, på ett säkert, styrt och sekretessvänligt sätt. Segment Match använder sekretessstandarder för Platform och personliga identifierare som hash-kodade e-postmeddelanden, hashade telefonnummer och enhetsidentifierare som IDFA och GAID. Mer information finns i [Översikt över segmentmatchning](../../segmentation/ui/segment-match/overview.md). |

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| Beta-källor som går över till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] källförbättringar | The [!DNL Event Hubs] source har nu stöd för SAS-nyckeltyper som inte är rot för autentisering för att ansluta och skapa källanslutning. Mer information finns i [[!DNL Event Hubs] översikt](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] källförbättringar | The [!DNL SFTP] kan du nu skapa ett angivet antal samtidiga anslutningar som ett dataflöde kan använda för att ansluta till SFTP-servern. Mer information finns i [[!DNL SFTP] översikt](../../sources/connectors/cloud-storage/sftp.md). |
