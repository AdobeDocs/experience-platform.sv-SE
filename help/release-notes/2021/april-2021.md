---
title: Versionsinformation om Adobe Experience Platform april 2021
description: Versionsinformation från april 2021 för Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 21 april 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för redigering av mappning för befintliga dataflöden | Du kan nu uppdatera mappningsuppsättningarna för ett befintligt dataflöde. Det går inte att uppdatera mappningsuppsättningar för dataflöden som har schemalagts för engångsbruk. Den här funktionen stöds inte för HTTP API, Adobe Analytics, Adobe Audience Manager och [!DNL Marketo Engage]. Mer information finns i självstudiekursen om [uppdatera källornas dataflöden i användargränssnittet](../../sources/tutorials/ui/update-dataflows.md). |
| Stöd för direktuppspelning | Du kan nu använda förinställningsfunktioner för data när du skapar en direktuppspelad källanslutning. Mer information finns i självstudiekursen om [skapa en direktuppspelningskällanslutning i användargränssnittet](../../sources/tutorials/ui/create/streaming/http.md). |

Mer information finns i [[!DNL Data Prep] översikt](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) är en öppen källkodsspecifikation som är utformad för att förbättra kraften i digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

| Funktion | Beskrivning |
| --- | --- |
| Schemarekommendationer efter bransch | När du väljer klasser och schemafältgrupper i schemaläggningsgränssnittet kan du använda ett nytt filter för att visa rekommenderade standardkomponenter baserat på din bransch. Läs dokumentationen om [branschdatamodeller](https://www.adobe.com/go/xdm-industry-erds-en) om du vill ha mer information om hur dessa komponenter hänger ihop för olika användningsområden i branschen. |

## [!DNL Intelligent Services] {#intelligent-services}

Intelligenta tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis.

### Kund-AI

Customer AI available in Real-time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, träna eller driftsätta.

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för Adobe Analytics-data | Uppdaterad funktionalitet som stöder Adobe Analytics datauppsättningar via Analytics-källkopplingen utan att era data behöver ETL för att följa CEE-schemat (Consumer Experience Event). |
| Stöd för Adobe Audience Manager-data | Uppdaterad funktionalitet som stöder Adobe Audience Manager datauppsättningar via Audience Manager-källkopplingen utan att dina data behöver ETL för att följa CEE-schemat (Consumer Experience Event). |
| Sammanfattning av modellprestanda | Kundens AI har nu en [sammanfattningsflik för modellprestanda](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) på sidan med insikter om tjänstinstans. På fliken för modellprestanda visas alla faktiska konverterings- och bortfallstakt. På så sätt kan du dechiffrera och förstå vad som händer i var och en av dina benägenhetsfrågor. |

Mer information om datauppsättningar som stöds finns i [[!DNL Intelligent Services] dokumentation om dataförberedelser](../../intelligent-services/data-preparation.md).

### Attribution AI

Attribution AI används för att attribuera krediter till kontaktytor som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktyta för marknadsföring över kundresor.

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för Adobe Analytics-data | Uppdaterad funktionalitet som stöder Adobe Analytics datauppsättningar via Analytics-källkopplingen utan att era data behöver ETL för att följa CEE-schemat (Consumer Experience Event). |

Mer information om datauppsättningar som stöds finns i [[!DNL Intelligent Services] dokumentation om dataförberedelser](../../intelligent-services/data-preparation.md).

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform Segmentation Service har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper från din [!DNL Real-Time Customer Profile] data. Dessa segment konfigureras och underhålls centralt på plattformen, vilket gör dem tillgängliga för alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Ytterligare aggregeringsfunktioner | Räkningsfunktioner har lagts till i Segment Builder. Med räkningsfunktionerna kan du räkna antalet gånger som den angivna händelsen har utförts. Mer information om räkningsfunktionerna finns i avsnittet med räkningsfunktioner i [Segment Builder Guide](../../segmentation/ui/segment-builder.md#count-functions) |

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Nu kan du skapa en [!DNL Marketo Engage] källanslutning med användargränssnittet för att ta med B2B-data till plattformen och hålla dessa data uppdaterade med plattformsanslutna program. Mer information finns i [[!DNL Marketo Engage] dokumentation för källanslutning](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Beta-källor som går över till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Mer information om källor finns i [källöversikt](../../sources/home.md).
