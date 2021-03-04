---
keywords: Experience Platform;hem;populära ämnen;datainmatning;dataplatse;dataplats;datahantering;datahantering;linje;rad;grupp;inmatad data
solution: Experience Platform
title: Översikt över dataöverföring
topic: översikt
description: I det här dokumentet introduceras de tre viktigaste sätten att överföra data till plattformen, med länkar till deras respektive översiktsdokumentation för mer detaljerad information.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Översikt över datainmatning

Adobe Experience Platform sammanför data från olika källor för att hjälpa marknadsförarna att bättre förstå kundernas beteende. Adobe Experience Platform datainmatning representerar de olika metoder som [!DNL Platform] använder för att hämta data från dessa källor, samt hur data bevaras i datasjön för användning av underordnade [!DNL Platform]-tjänster.

I det här dokumentet introduceras de tre huvudsakliga sätten att överföra data till [!DNL Platform], med länkar till deras respektive översiktsdokumentation för mer detaljerad information.

## Batchförtäring

Med batchöverföring kan du importera data till [!DNL Experience Platform] som batchfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. När du har importerat batcharna innehåller de metadata som beskriver antalet poster som har importerats samt eventuella poster som misslyckades och tillhörande felmeddelanden.

Manuellt överförda datafiler som platta CSV-filer (mappade till XDM-scheman) och Parquet-dataramar måste importeras med den här metoden.

Mer information finns i översikten [batchöverföring](./batch-ingestion/overview.md).

## Direktinmatning

Med direktuppspelad inmatning kan du skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid. [!DNL Platform] stöder användningen av datainmatningar för att strömma inkommande upplevelsedata, som finns kvar i strömningsaktiverade datauppsättningar i Data Lake. Datainmatningar kan konfigureras så att de automatiskt autentiserar de data de samlar in, vilket säkerställer att data kommer från en betrodd källa.

Mer information finns i [översikten över direktuppspelning](./streaming-ingestion/overview.md).

## Källor

[!DNL Experience Platform] gör att du kan konfigurera källanslutningar till olika dataleverantörer. Dessa anslutningar gör att du kan autentisera mot externa datakällor, ange tider för matningsåtgärder och hantera matningsflöde.

Källanslutningar kan konfigureras för att samla in data från andra Adobe-program (till exempel Adobe Analytics och Adobe Audience Manager), molnlagringskällor från tredje part (till exempel [!DNL Azure Blob], [!DNL Amazon] S3, FTP-servrar och SFTP-servrar) och CRM-system från tredje part (till exempel [!DNL Microsoft Dynamics] och [!DNL Salesforce]).

Mer information finns i [Källöversikt](../sources/home.md).

## Nästa steg och ytterligare resurser

Det här dokumentet innehåller en kort introduktion till de olika aspekterna av [!DNL Data Ingestion] i [!DNL Experience Platform]. Fortsätt att läsa översiktsdokumentationen för varje intagsmetod för att bekanta dig med deras olika funktioner, användningsfall och bästa metoder. Du kan även komplettera din inlärning genom att titta på videon med en översikt över importen nedan. Mer information om hur [!DNL Experience Platform] spårar metadata för kapslade poster finns i [Katalogtjänstöversikt](../catalog/home.md).

>[!WARNING]
>
>Termen Enhetlig profil som används i följande video är inaktuell. Termerna [!DNL "Profile"] eller [!DNL "Real-time Customer Profile"] är de korrekta termer som används i dokumentationen för [!DNL Experience Platform]. Läs dokumentationen om de senaste funktionerna.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)