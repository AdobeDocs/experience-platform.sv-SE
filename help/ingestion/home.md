---
keywords: Experience Platform;hem;populära ämnen;datainmatning;dataplatse;dataplats;datahantering;datahantering;linje;rad;grupp;inmatad data
solution: Experience Platform
title: Översikt över dataöverföring
description: I det här dokumentet presenteras de tre viktigaste sätten att överföra data till Experience Platform, med länkar till respektive översiktsdokumentation för mer detaljerad information.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Översikt över datainmatning

Adobe Experience Platform sammanför data från olika källor för att hjälpa marknadsförarna att bättre förstå kundernas beteende. Adobe Experience Platform datainmatning representerar de olika metoder som Experience Platform använder för att importera data från dessa källor, samt hur data lagras i Data Lake för användning av Experience Platform-tjänster längre fram i kedjan.

I det här dokumentet presenteras de tre viktigaste sätten att överföra data till Experience Platform, med länkar till respektive översiktsdokumentation för mer detaljerad information.

## Batchförtäring

Med batchöverföring kan du importera data till [!DNL Experience Platform] som gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. När du har importerat batcharna innehåller de metadata som beskriver antalet poster som har importerats samt eventuella poster som misslyckades och tillhörande felmeddelanden.

Manuellt överförda datafiler som platta CSV-filer (mappade till XDM-scheman) och Parquet-dataramar måste importeras med den här metoden.

Mer information finns i [översikten över gruppinmatning](./batch-ingestion/overview.md).

>[!TIP]
>
>Använd enkelradig JSON i stället för flerradig JSON som indata för batchförtäring. En-rads JSON ger bättre prestanda eftersom systemet kan dela upp en indatafil i flera segment och bearbeta dem parallellt, medan flerrads-JSON inte kan delas. Detta kan avsevärt minska databehandlingskostnaderna och förbättra tidsfördröjningen för gruppbearbetning.

## Direktinmatning

Med direktuppspelningsinmatning kan du skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid. Experience Platform stöder användningen av datainmatningar för att strömma inkommande upplevelsedata, som finns kvar i strömningsaktiverade datauppsättningar i Data Lake. Datainmatningar kan konfigureras så att de automatiskt autentiserar de data de samlar in, vilket säkerställer att data kommer från en betrodd källa.

Mer information finns i [översikten över direktuppspelning](./streaming-ingestion/overview.md).

## Källor

Med [!DNL Experience Platform] kan du konfigurera källanslutningar till olika dataleverantörer. Dessa anslutningar gör att du kan autentisera mot externa datakällor, ange tider för matningsåtgärder och hantera matningsflöde.

Source-anslutningar kan konfigureras för att samla in data från andra Adobe-program (till exempel Adobe Analytics och Adobe Audience Manager), molnlagringskällor från tredje part (till exempel [!DNL Azure Blob], [!DNL Amazon] S3, FTP-servrar och SFTP-servrar) och CRM-system från tredje part (till exempel [!DNL Microsoft Dynamics] och [!DNL Salesforce]).

Mer information finns i [Källöversikt](../sources/home.md).

### Skapa ML-stödda scheman {#ml-assisted-schema-creation}

För att snabbt integrera nya datakällor kan du nu använda maskininlärningsalgoritmer för att generera ett schema från exempeldata. Den här automatiseringen förenklar framtagningen av korrekta scheman, minskar antalet fel och snabbar upp processen från datainsamling till analys och insikter.

Mer information om det här arbetsflödet finns i guiden [Skapa XML-stödda scheman](../xdm/ui/ml-assisted-schema-creation.md).

## Nästa steg och ytterligare resurser

Det här dokumentet innehåller en kort introduktion till de olika aspekterna av [!DNL Data Ingestion] i [!DNL Experience Platform]. Fortsätt att läsa översiktsdokumentationen för varje intagsmetod för att bekanta dig med deras olika funktioner, användningsfall och bästa metoder. Du kan även komplettera din inlärning genom att titta på videon med en översikt över importen nedan. Mer information om hur [!DNL Experience Platform] spårar metadata för kapslade poster finns i [Katalogtjänstöversikt](../catalog/home.md).

>[!WARNING]
>
>Termen Enhetlig profil som används i följande video är inaktuell. Termerna [!DNL "Profile"] eller [!DNL "Real-Time Customer Profile"] är rätt termer som används i dokumentationen för [!DNL Experience Platform]. Läs dokumentationen om de senaste funktionerna.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
