---
keywords: Experience Platform;hem;populära ämnen;datainmatning;dataplatse;dataplats;datahantering;datahantering;linje;rad;grupp;inmatad data
solution: Experience Platform
title: Översikt över dataöverföring
description: I det här dokumentet introduceras de tre viktigaste sätten att överföra data till plattformen, med länkar till deras respektive översiktsdokumentation för mer detaljerad information.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Översikt över datainmatning

Adobe Experience Platform sammanför data från olika källor för att hjälpa marknadsförarna att bättre förstå kundernas beteende. Adobe Experience Platform datainmatning representerar de olika metoder som [!DNL Platform] inhämtar data från dessa källor samt hur dessa data bevaras inom datasjön för användning i senare led [!DNL Platform] tjänster.

I det här dokumentet beskrivs de tre huvudsakliga sätten att överföra data till [!DNL Platform], med länkar till deras respektive översiktsdokumentation för mer detaljerad information.

## Batchförtäring

Genom att lägga till data i grupp kan du importera data till [!DNL Experience Platform] som gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. När du har importerat batcharna innehåller de metadata som beskriver antalet poster som har importerats samt eventuella poster som misslyckades och tillhörande felmeddelanden.

Manuellt överförda datafiler som platta CSV-filer (mappade till XDM-scheman) och Parquet-dataramar måste importeras med den här metoden.

Se [batchvis hantering - översikt](./batch-ingestion/overview.md) för mer information.

## Direktinmatning

Med direktuppspelning kan du skicka data från klient- och serverenheter till [!DNL Experience Platform] i realtid. [!DNL Platform] stöder användningen av datainmatningar för att strömma inkommande upplevelsedata, som finns kvar i strömningsaktiverade datauppsättningar i Data Lake. Datainmatningar kan konfigureras så att de automatiskt autentiserar de data de samlar in, vilket säkerställer att data kommer från en betrodd källa.

Se [översikt över direktuppspelning](./streaming-ingestion/overview.md) för mer information.

## Källor

[!DNL Experience Platform] gör att du kan konfigurera källanslutningar till olika dataleverantörer. Dessa anslutningar gör att du kan autentisera mot externa datakällor, ange tider för matningsåtgärder och hantera matningsflöde.

Källanslutningar kan konfigureras för att samla in data från andra Adobe-program (till exempel Adobe Analytics och Adobe Audience Manager), molnlagringskällor från tredje part (till exempel [!DNL Azure Blob], [!DNL Amazon] S3-, FTP-servrar och SFTP-servrar) och CRM-system från tredje part (till exempel [!DNL Microsoft Dynamics] och [!DNL Salesforce]).

Se [Översikt över källor](../sources/home.md) för mer information.

## Nästa steg och ytterligare resurser

Detta dokument innehåller en kort introduktion till de olika aspekterna av [!DNL Data Ingestion] in [!DNL Experience Platform]. Fortsätt att läsa översiktsdokumentationen för varje intagsmetod för att bekanta dig med deras olika funktioner, användningsfall och bästa metoder. Du kan även komplettera din inlärning genom att titta på videon med en översikt över importen nedan. Information om hur [!DNL Experience Platform] spårar metadata för kapslade poster, se [Katalogtjänst - översikt](../catalog/home.md).

>[!WARNING]
>
>Termen Enhetlig profil som används i följande video är inaktuell. Villkoren [!DNL "Profile"] eller [!DNL "Real-Time Customer Profile"] är rätt termer som används i [!DNL Experience Platform] dokumentation. Läs dokumentationen om de senaste funktionerna.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
