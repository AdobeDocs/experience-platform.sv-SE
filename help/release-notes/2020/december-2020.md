---
title: Adobe Experience Platform Release Notes december 2020
description: Versionsinformation december 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 10%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 december 2020**

Nya funktioner i Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Dataflöden är en representation av datajobb som flyttar data mellan Experience Platform. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, till identitets- och profiltjänster samt till mål.

**Nyckelfunktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Genomskinlighet för dataflöden | Du kan övervaka dataflöden för källor och mål. Mer information finns i [självstudiekursen om övervakning av källor](../../dataflows/ui/monitor-sources.md) eller [självstudiekursen om övervakning av mål](../../dataflows/ui/monitor-destinations.md). |

Mer information om dataflöden finns i [dataflödesöversikten](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era datatillgångar i alla Adobe lösningar.

**Viktiga funktioner**

| Funktion | Beskrivning |
| --- | ---|
| Adobe Experience Platform Intelligence-pakettillägg | Adobe Experience Platform Intelligence-paketet är en uppgradering av Data Science Workspace som ger tillgång till ytterligare funktioner som: <li> UI-driven modellexperimenterande och utvärdering.</li><li> Möjlighet att driftsätta och driftsätta modeller med schemalagda utbildnings- och konferensjobb.</li><li> Stöd för djuplärande i Tensorflow-modeller (GPU Compute).</li><li> Spark-baserad distribuerad beräkning för att träna och poängsätta mot stora datamängder (10 MM + rader).</li><li>Och mer</li> |

Mer information om Adobe Experience Platform Intelligence-pakettillägget finns i dokumentationen om [Data Science Workspace-åtkomst och -funktioner](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som du kan strukturera, etikettera och förbättra data med hjälp av [!DNL Experience Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatera konto- och anslutningsinformation för strömningskällor | Nu kan du uppdatera namn, beskrivningar och autentiseringsuppgifter för befintliga direktuppspelningsanslutningar med API:t [!DNL Flow Service] och gränssnittet. Mer information finns i självstudiekursen om att [uppdatera anslutningar med API](../../sources/tutorials/api/update.md) och [redigera kontoinformation med gränssnittet](../../sources/tutorials/ui/monitor.md). |
| Ta bort dataflöden | Strömmande dataflöden som innehåller fel eller har blivit onödiga kan nu tas bort med API:t [!DNL Flow Service] och gränssnittet. Mer information finns i självstudiekursen om att [ta bort dataflöden med API:t ](../../sources/tutorials/api/delete-dataflows.md) och [ta bort dataflöden med användargränssnittet](../../sources/tutorials/ui/delete.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
