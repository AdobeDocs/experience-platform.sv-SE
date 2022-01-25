---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
source-git-commit: 641fcab89b849d91a075fa5058421950bc7fecd7
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 januari 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Larm](#alerts)
- [Dataprep](#data-prep)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)

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
