---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 9 december 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: a411ac92d946080abd7b22b9d57c7154d263a30a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 december 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar.

### Viktiga funktioner

| Funktion | Beskrivning |
|--- | ---|
| Adobe Experience Platform Intelligence-pakettillägg | Adobe Experience Platform Intelligence-paketet är en uppgradering av en Data Science Workspace som aktiverar ytterligare funktioner som: <li> UI-driven modellexperimenterande och utvärdering.</li><li> Möjlighet att driftsätta och driftsätta modeller med schemalagda utbildnings- och konferensjobb.</li><li> Stöd för djupinlärning i Tensorflow-modeller (GPU Compute).</li><li> Spark-baserad distribuerad beräkning för att träna och poängsätta mot stora datamängder (10 MM + rader).</li><li>Och mer</li> |

Mer information om Adobe Experience Platform Intelligence-pakettillägget finns i dokumentationen om [Data Science Workspace-åtkomst och -funktioner](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatera konto- och anslutningsinformation för strömningskällor | Nu kan du uppdatera namn, beskrivningar och autentiseringsuppgifter för befintliga direktuppspelningsanslutningar med API:t och gränssnittet [!DNL Flow Service] . Mer information finns i självstudiekursen om hur du [uppdaterar anslutningar med API:t](../../sources/tutorials/api/update.md) och [redigerar kontoinformation med användargränssnittet](../../sources/tutorials/ui/monitor.md). |
| Ta bort dataflöden | Strömmande dataflöden som innehåller fel eller har blivit onödiga kan nu tas bort med API:t och gränssnittet [!DNL Flow Service] . Mer information finns i självstudiekursen om hur du [tar bort dataflöden med API:t](../../sources/tutorials/api/delete-dataflows.md) och [tar bort dataflöden med gränssnittet](../../sources/tutorials/ui/delete.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).

