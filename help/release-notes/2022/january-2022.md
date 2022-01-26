---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
source-git-commit: 9cd9307d54d0950d4f67d5d8cee9c6412a558275
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 januari 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Larm {#alerts}](#alerts-alerts)
- [[!DNL Data Prep] {#data-prep}](#dnl-data-prep-data-prep)
- [[!DNL Dashboards] {#dashboards}](#dnl-dashboards-dashboards)
- [Frågetjänst {#query-service}](#query-service-query-service)
- [Sandlådor {#sandboxes}](#sandboxes-sandboxes)
- [Segmenteringstjänst {#segmentation}](#segmentation-service-segmentation)

## Larm {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika plattformsaktiviteter. Du kan prenumerera på olika varningsregler via [!UICONTROL Alerts] -fliken i användargränssnittet för plattformen och kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya varningsregler | Flera nya varningsregler finns nu tillgängliga för arbetsflöden som rör datainhämtning, identiteter, profiler, segmentering och aktivering. Se översikten på [varningsregler](../../observability/alerts/rules.md) för den uppdaterade listan över varningstyper. |

Mer information om varningar i Platform finns i [varningsöversikt](../../observability/alerts/overview.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Konsoliderad kartläggning | Det nya mappningsgränssnittet i plattformsgränssnittet ger en konsekvent mappningsupplevelse så att du kan dra nytta av intelligenta mappningsrekommendationer, manuellt konfigurera mappningsregler och felsöka eventuella fel som inträffar i mappningsuppsättningarna. Mer information finns i [[!DNL Data Prep] Användargränssnittsguide](../../data-prep/home.md). |

Mer information om [!DNL Data Prep], se [[!DNL Data Prep] översikt](../../data-prep/home.md).

## [!DNL Dashboards] {#dashboards}

[!DNL Dashboards] gör vackra saker.

| Funktion | Beskrivning |
|---------|-------------|
| Intelligenta bildtexter | En maskininlärningsalgoritm ger automatiskt insikter om profil- och målgruppsdata och illustrerar mönster och trender under en 30-90-dagars- eller 12-månadersperiod. Bildtexterna innehåller information om <ul><li>Generell form och statistik</li><li>Trender och plötsliga ändringar</li><li>Säsongsmönster</li><li>Oväntade avvikelser</li></ul> Mer information finns på [profiler dashboards](../../dashboards/guides/profiles.md#profiles-count-trend) och [instrumentpaneler för segment](../../dashboards/guides/segments.md#audience-size-trend) dokumentation. |
| Instrumentpanelsinventering | Få tillgång till förkonfigurerade rapporter om profiler, segment och målpaneler, inklusive installerade integreringar som PowerBI, på en central plats. Mer information finns i [[!DNL Dashboards] översikt](../../dashboards/home.md). |
| PowerBI-rapportmallar | Bygg, anpassa eller utöka mätvärden från profil-, segment- och målrapporteringsdatamodeller med nya PowerBI-diagram. Det automatiserade installationsarbetsflödet gör att ni kan dela med er av era marknadsföringsinsikter i hela organisationen inifrån PowerBI-miljön. Mer information finns i [[!DNL Dashboards] översikt](../../dashboards/home.md). |

Mer information om [!DNL Dashboards], se [[!DNL Dashboards] översikt](../../dashboards/home.md).

## Frågetjänst {#query-service}

[!DNL Query Service] låter dig använda standard-SQL för att fråga efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, datavetenskapen eller för förtäring i kundprofilen i realtid.

| Funktion | Beskrivning |
|----------------------|-----------------------|
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

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Segmentmatchning | Segmentmatchning är en tjänst för datasamarbete som gör det möjligt för två eller flera plattformsanvändare att utbyta data, baserat på gemensamma identifierare, på ett säkert, styrt och sekretessvänligt sätt. Mer information finns i [Översikt över segmentmatchning](../../segmentation/ui/segment-match/overview.md). |

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md).
