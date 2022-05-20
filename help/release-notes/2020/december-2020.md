---
title: Adobe Experience Platform Release Notes december 2020
description: Versionsinformation december 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 december 2020**

Nya funktioner i Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, till identitets- och profiltjänster samt till mål.

**Nyckelfunktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Genomskinlighet för dataflöden | Du kan övervaka dataflöden för källor och mål. Mer information finns i [självstudiekurs om övervakningskällor](../../dataflows/ui/monitor-sources.md) eller [självstudiekurs om övervakning av destinationer](../../dataflows/ui/monitor-destinations.md). |

Läs mer om dataflöden i [dataflödesöversikt](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar.

**Viktiga funktioner**

| Funktion | Beskrivning |
| --- | ---|
| Adobe Experience Platform Intelligence-pakettillägg | Adobe Experience Platform Intelligence-paketet är en uppgradering av en Data Science Workspace som aktiverar ytterligare funktioner som: <li> UI-driven modellexperimenterande och utvärdering.</li><li> Möjlighet att driftsätta och driftsätta modeller med schemalagda utbildnings- och konferensjobb.</li><li> Stöd för djupinlärning i Tensorflow-modeller (GPU Compute).</li><li> Spark-baserad distribuerad beräkning för att träna och poängsätta mot stora datamängder (10 MM + rader).</li><li>Och mer</li> |

Mer information om Adobe Experience Platform Intelligence-paketet finns i dokumentationen om [Åtkomst och funktioner till arbetsytan Data Science](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatera konto- och anslutningsinformation för strömningskällor | Nu kan du uppdatera namn, beskrivningar och autentiseringsuppgifter för befintliga direktuppspelningsanslutningar med [!DNL Flow Service] API och användargränssnittet. Mer information finns i självstudiekursen om [uppdatera anslutningar med API](../../sources/tutorials/api/update.md) och [redigera kontoinformation med användargränssnittet](../../sources/tutorials/ui/monitor.md). |
| Ta bort dataflöden | Strömmande dataflöden som innehåller fel eller har blivit onödiga kan nu tas bort med [!DNL Flow Service] API och användargränssnittet. Mer information finns i självstudiekursen om [ta bort dataflöden med API](../../sources/tutorials/api/delete-dataflows.md) och [ta bort dataflöden med användargränssnittet](../../sources/tutorials/ui/delete.md). |

Mer information om källor finns i [källöversikt](../../sources/home.md).
