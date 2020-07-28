---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över datainmatning i Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---


# Översikt över datainmatning

Adobe Experience Platform sammanför data från olika källor för att hjälpa marknadsförarna att bättre förstå kundernas beteende. Adobe Experience Platform Data Ingestion representerar de olika metoder som [!DNL Platform] inhämtar data från dessa källor, samt hur data bevaras i datasjön för användning av [!DNL Platform] tjänster längre fram i kedjan.

I det här dokumentet introduceras de tre huvudsakliga sätten som data hämtas till, med länkar till respektive översiktsdokumentation för mer detaljerad information. [!DNL Platform]

## Batchförtäring

Genom att lägga in data i grupp kan du importera data [!DNL Experience Platform] som gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. När du har importerat batcharna innehåller de metadata som beskriver antalet poster som har importerats samt eventuella poster som misslyckades och tillhörande felmeddelanden.

Manuellt överförda datafiler som platta CSV-filer (mappade till XDM-scheman) och Parquet-dataramar måste importeras med den här metoden.

Mer information finns i översikten [över](./batch-ingestion/overview.md) gruppinmatning.

## Direktinmatning

Med direktuppspelad inmatning kan ni skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid. [!DNL Platform] stöder användningen av datainmatningar för att strömma inkommande upplevelsedata, som finns kvar i strömningsaktiverade datauppsättningar i Data Lake. Datainmatningar kan konfigureras så att de automatiskt autentiserar de data de samlar in, vilket säkerställer att data kommer från en betrodd källa.

Mer information finns i översikten [över](./streaming-ingestion/overview.md) direktuppspelningsuppläsning.

## Källor

[!DNL Experience Platform] gör att du kan konfigurera källanslutningar till olika dataleverantörer. Dessa anslutningar gör att du kan autentisera mot externa datakällor, ange tider för matningsåtgärder och hantera matningsflöde.

Källanslutningar kan konfigureras för att samla in data från andra Adobe-program (t.ex. Adobe Analytics och Adobe Audience Manager), molnlagringskällor från tredje part (t.ex. [!DNL Azure Blob], S3, FTP-servrar och SFTP-servrar) och CRM-system från tredje part (t.ex. [!DNL Amazon] och [!DNL Microsoft Dynamics] [!DNL Salesforce]).

Mer information finns i [Källöversikt](../sources/home.md) .

## Nästa steg och ytterligare resurser

Detta dokument innehåller en kort introduktion till de olika aspekterna av [!DNL Data Ingestion] i [!DNL Experience Platform]. Fortsätt att läsa översiktsdokumentationen för varje metod för att bekanta dig med deras olika funktioner, användningsfall och bästa metoder. Du kan även understödja din inlärning genom att titta på översiktsvideon nedan. Mer information om hur du [!DNL Experience Platform] spårar metadata för inkapslade poster finns i [Katalogtjänstöversikt](../catalog/home.md).

>[!WARNING]
>
> Termen Enhetlig profil som används i följande video är inaktuell. Termerna [!DNL "Profile"] eller [!DNL "Real-time Customer Profile"] termerna är de korrekta termer som används i [!DNL Experience Platform] dokumentationen. Läs dokumentationen om de senaste funktionerna.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)