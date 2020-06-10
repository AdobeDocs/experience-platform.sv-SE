---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation om Experience Platform 10 juni 2020
doc-type: release notes
last-update: June 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: b6cfdf56c20065bdc3e8a9fedf6007ddd74eaeaa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# Versionsinformation om Adobe Experience Platform

**Releasedatum: 10 juni 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datavetenskapens arbetsyta](#dsw)
- [Källor](#sources)

## Datavetenskapens arbetsyta {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att ge insikter från era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med ert innehåll och era dataresurser över alla Adobes lösningar.

Data Science Workspace har arbetat på nya sätt för att möjliggöra bättre upplevelser och prognoser med hjälp av maskininlärning i realtid. Maskininlärning i realtid ger möjlighet att skapa, testa och driftsätta anpassade eller importerade förutbildade maskininlärningsmodeller i branschstandard-kompatibla modellformat för bedömning/aktivering i realtid via en API-slutpunkt.

Observera att maskininlärning i realtid är alfavärdet och fortfarande utvecklas.

| Funktion | Beskrivning |
|--- | ---|
| JupyterLab Launcher Real-time ML-start | JupyterLab Launcher innehåller nu en startfunktion för en Python-bärbar dator för maskininlärning i realtid (Alpha). |

Mer information om Machine Learning-alfa i realtid finns i [Machine Learning-översikten](../../data-science-workspace/real-time-machine-learning/home.md)i realtid.

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som ni kan strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, programvara från tredje part och ditt CRM-system.

Experience Platform har ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Ytterligare API- och gränssnittsstöd för molnlagringssystem | Ny källanslutning för Apache HDFS |
| Ytterligare API- och gränssnittsstöd för databaser | Ny källanslutning för Couchbase. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
