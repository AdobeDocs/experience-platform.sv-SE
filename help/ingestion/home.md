---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över datainmatning i Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Översikt över datainmatning

Adobe Experience Platform samlar data från flera olika källor för att hjälpa marknadsförarna att bättre förstå kundernas beteende. Adobe Experience Platforms datainmatning representerar de olika metoder som Platform använder för att hämta data från dessa källor samt hur dessa data lagras i Data Lake för användning av plattformstjänster längre fram i kedjan.

I det här dokumentet introduceras de tre viktigaste sätten att överföra data till plattformen, med länkar till deras respektive översiktsdokumentation för mer detaljerad information.

## Batchförtäring

Med batchöverföring kan ni importera data till Experience Platform som batchfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. När du har importerat batcharna innehåller de metadata som beskriver antalet poster som har importerats samt eventuella poster som misslyckades och tillhörande felmeddelanden.

Manuellt överförda datafiler som platta CSV-filer (mappade till XDM-scheman) och Parquet-dataramar måste importeras med den här metoden.

Mer information finns i översikten [över](./batch-ingestion/overview.md) gruppinmatning.

## Direktinmatning

Med direktuppspelad inmatning kan ni skicka data från klient- och serverenheter till Experience Platform i realtid. Plattformen stöder användningen av datainmatningar för att strömma inkommande upplevelsedata, som finns kvar i strömningsaktiverade datauppsättningar i Data Lake. Datainmatningar kan konfigureras så att de automatiskt autentiserar de data de samlar in, vilket säkerställer att data kommer från en betrodd källa.

Mer information finns i översikten [över](./streaming-ingestion/overview.md) direktuppspelningsuppläsning.

## Källor

Med Experience Platform kan ni skapa källanslutningar till olika dataleverantörer. Dessa anslutningar gör att du kan autentisera mot externa datakällor, ange tider för matningsåtgärder och hantera matningsflöde.

Källanslutningar kan konfigureras för att samla in data från andra Adobe-program (till exempel Adobe Analytics och Adobe Audience Manager), molnlagringskällor från tredje part (till exempel Azure Blob, Amazon S3, FTP-servrar och SFTP-servrar) och CRM-system från tredje part (till exempel Microsoft Dynamics och Salesforce).

Mer information finns i [Källöversikt](../source-connectors/home.md) .

## Nästa steg

Detta dokument innehåller en kort introduktion till de olika aspekterna av datainmatning i Experience Platform. Fortsätt att läsa översiktsdokumentationen för varje metod för att bekanta dig med deras olika funktioner, användningsfall och bästa metoder. Mer information om hur Experience Platform spårar metadata för inkapslade poster finns i [Katalogtjänstöversikten](../catalog/home.md).