---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform för 21 april 2021.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 0c9b60fe0777286819841c520a41007634622578
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 1%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 21 april 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för redigering av mappning för befintliga dataflöden | Du kan nu uppdatera mappningsuppsättningarna för ett befintligt dataflöde. Det går inte att uppdatera mappningsuppsättningar för dataflöden som har schemalagts för engångsbruk. Den här funktionen stöds inte för HTTP API, Adobe Analytics, Adobe Audience Manager och [!DNL Marketo Engage]. Mer information finns i självstudiekursen om att [uppdatera källans dataflöden i användargränssnittet](../../sources/tutorials/ui/update-dataflows.md). |
| Stöd för direktuppspelning | Du kan nu använda förinställningsfunktioner för data när du skapar en direktuppspelad källanslutning. Mer information finns i självstudiekursen om att [skapa en direktuppspelningskällanslutning i användargränssnittet](../../sources/tutorials/ui/create/streaming/http.md). |

Mer information finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## [!DNL Intelligent Services] {#intelligent-services}

Intelligenta tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis.

### Kund-AI

Kundens AI som finns i kunddataplattformen i realtid används för att generera anpassade benägenhetspoäng som bortfall och konvertering för enskilda profiler i stor skala. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, träna eller driftsätta.

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för Adobe Analytics-data | Uppdaterad funktionalitet som stöder Adobe Analytics datauppsättningar via Analytics-källkopplingen utan att era data behöver ETL för att följa CEE-schemat (Consumer Experience Event). |
| Stöd för Adobe Audience Manager-data | Uppdaterad funktionalitet som stöder Adobe Audience Manager datauppsättningar via Audience Manager-källkopplingen utan att dina data behöver ETL för att följa CEE-schemat (Consumer Experience Event). |
| Sammanfattning av modellprestanda | Kund-AI har nu en [modellprestandasammanfattningsflik](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) på sidan med insikter om tjänstinstans. På fliken för modellprestanda visas alla faktiska konverterings- och bortfallstakt. På så sätt kan du dechiffrera och förstå vad som händer i var och en av dina benägenhetsfrågor. |

Mer information om vilka datauppsättningar som stöds finns i [[!DNL Intelligent Services] dokumentationen för dataförberedelser](../../intelligent-services/data-preparation.md).

### Attribution AI

Attribution AI används för att attribuera krediter till kontaktytor som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktyta för marknadsföring över kundresor.

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för Adobe Analytics-data | Uppdaterad funktionalitet som stöder Adobe Analytics datauppsättningar via Analytics-källkopplingen utan att era data behöver ETL för att följa CEE-schemat (Consumer Experience Event). |

Mer information om vilka datauppsättningar som stöds finns i [[!DNL Intelligent Services] dokumentationen för dataförberedelser](../../intelligent-services/data-preparation.md).

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile]-data. Dessa segment konfigureras och underhålls centralt på plattformen, vilket gör dem tillgängliga för alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Ytterligare aggregeringsfunktioner | Räkningsfunktioner har lagts till i Segment Builder. Med räkningsfunktionerna kan du räkna antalet gånger som den angivna händelsen har utförts. Mer information om räkningsfunktionerna finns i avsnittet med räkningsfunktioner i [guiden Skapa segment](../../segmentation/ui/segment-builder.md#count-functions) |

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikt](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Nu kan du skapa en [!DNL Marketo Engage]-källanslutning med användargränssnittet för att hämta B2B-data till plattformen och hålla dessa data uppdaterade med plattformsanslutna program. Mer information finns i [[!DNL Marketo Engage] källanslutningsdokumentationen](../../sources/connectors/adobe-applications/marketo/marketo.md). |

Mer information om källor finns i [Källor - översikt](../../sources/home.md).
