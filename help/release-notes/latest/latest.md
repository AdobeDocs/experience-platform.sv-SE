---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform för 28 juli 2021.
doc-type: release notes
last-update: July 28, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 28 juli 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datavetenskapens arbetsyta](#dsw)
- [Dataflöden](#destinations)
- [Mål ](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Frågetjänst](#query)
- [Källor](#sources)

## Datavetenskapens arbetsyta {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar för bibliotek och operativsystem | Data Science Workspace har gjort betydande biblioteks- och operativsystemsuppdateringar för att förbättra funktionaliteten och användbarheten. Detta inkluderar JupyterLab 1.2.20, Python 3.7, Pandor 1.2.4, Tensorflow 2.4.1 med stöd för CUDA 11 och CUDNN 8 med mera. Om du vill lära dig hur du visar tillgängliga bibliotek i JupyterLab går du till avsnittet [bibliotek som stöds](../../data-science-workspace/jupyterlab/overview.md#supported-libraries) i översiktsdokumentationen för JupyterLab-anteckningsböcker. |

Mer allmän information om arbetsytan Datavetenskap finns i [Översikt över arbetsytan Datavetenskap](../../data-science-workspace/home.md).

## Dataflöden {#dataflows}

I Platform hämtas data från många olika källor, analyseras i systemet och aktiveras till en mängd olika destinationer. Plattformen gör processen att spåra detta potentiellt icke-linjära dataflöde enklare genom att tillhandahålla genomskinlighet med dataflöden.

Dataflöden är en representation av jobb som flyttar data över plattformen. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, där de sedan används av identitetstjänsten och kundprofilen i realtid innan de aktiveras för destinationerna.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Kontrollpanel för destinationer | Du kan nu använda kontrollpanelen för övervakning för att övervaka dataflöden för mål. Om du vill veta mer kan du läsa självstudiekursen om [övervakningsmål i användargränssnittet](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard) |

Mer allmän information om dataflöden finns i [översikten över dataflöden](../../dataflows/home.md). Mer information om destinationer finns i [målöversikten](../../destinations/home.md).

## Mål  {#destinations}

Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Snabbare export av inkrementella filer](../../destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) | Du kan nu schemalägga inkrementell filexport för filbaserade mål var 3, 6, 8 och 12:e timme. Det finns för närvarande inget stöd för att ändra filexportschemat för segment som redan har sparats. Om du vill återexportera segment med ett annat schema måste du skapa en ny destinationsinstans. Detta är en begränsning som kommer att tas upp i framtida versioner. |
| [Stöd för dedupliceringsnycklar](../../destinations/ui/activate-batch-profile-destinations.md#deduplication-keys) | Eliminera flera poster med samma profil i exportfilerna genom att välja en dedupliceringsnyckel. Du kan välja ett enstaka namnutrymme eller upp till två XDM-schemaattribut som en dedupliceringsnyckel. |

## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) är en öppen källkodsspecifikation som är utformad för att förbättra kraften i digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för data i form av scheman, som gör att alla program kan kommunicera med plattformstjänster.

| Funktion | Beskrivning |
| --- | --- |
| Telekommunikationsfilter | När du lägger till fältgrupper i ett schema i användargränssnittet kan du nu filtrera efter telekombranschen. Se [Egenrelationsdiagram (ERD)](../../xdm/schema/industries/telecom.md) för telekombranschen för att se en rekommenderad datamodell för användning inom telekom. |

Mer allmän information om XDM i Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Frågetjänst {#query}

Med frågetjänsten kan du använda standard-SQL för att fråga data i Adobe Experience Platform, vilket stöder en mängd olika användningsfall för analys och datahantering. Det är ett serverlöst verktyg som gör att du kan koppla ihop datauppsättningar från datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas i rapporter, Data Science Workspace eller för att lägga in dem i kundprofilen i realtid.

Du kan använda frågetjänsten för att bygga dataanalysekosystem och skapa en bild av kunderna över deras olika interaktionskanaler. De här kanalerna kan omfatta butiks-, webb-, mobil- eller CRM-system.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Schemalagda frågor | Du kan nu schemalägga frågor i plattformen med hjälp av Frågeredigeraren. Mer information finns i dokumentationen för [Frågeredigeraren](../../query-service/ui/user-guide.md#scheduled-queries). |

Mer information finns i [dokumentationen för frågetjänsten](../../query-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| ------- | ----------- |
| Beta-källor som går över till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL Amazon Redshift]](../../sources/connectors/databases/redshift.md)</li><li>[[!DNL Azure Table Storage]](../../sources/connectors/databases/ats.md)</li><li>[[!DNL PayPal]](../../sources/connectors/payments/paypal.md)</li></ul> |
| [!DNL Salesforce Marketing Cloud] (Beta) | Nu kan du ansluta [!DNL Salesforce Marketing Cloud] till Experience Platform med hjälp av API:t [!DNL Flow Service] eller gränssnittet. Mer information finns i [[!DNL Salesforce Marketing Cloud] anslutningsöversikten](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). |

Mer information om källor finns i [Källor - översikt](../../sources/home.md).
