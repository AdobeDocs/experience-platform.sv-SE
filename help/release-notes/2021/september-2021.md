---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 4959b5227f777a2c8cab1317d67795678d1a6eea
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 29 september 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Dataintag](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Källor](#sources)

## Dataintag {#ingestion}

Adobe Experience Platform datainmatning representerar de olika metoder som används för att importera data från olika källor och hur data lagras i datasjön för användning av plattformstjänster längre fram i kedjan.

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Uppgradera eller korrigera profilposter med hjälp av gruppinmatning | Realtidskundprofil tillåter nu uppdateringar av profilattribut i enskilda profilpostdata via batchinmatning. Mer information finns i [Utvecklarhandboken för gruppfrågor](../../ingestion/batch-ingestion/api-overview.md). |

Mer information om hur du hämtar data till Platform finns i [dokumentationen för datainmatning](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för strömmande dataflöden | Du kan nu använda dataprep-funktioner när du skapar ett direktuppspelat dataflöde för [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] och [!DNL Google PubSub]. Mer information finns i självstudiekursen om att [skapa ett direktuppspelat dataflöde för molnlagringskällor](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md). |

Mer information om [!DNL Data Prep] finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Data Landing Zone] | Nu kan du skapa en [!DNL Data Landing Zone]-källanslutning med hjälp av [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) eller [användargränssnittet](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] är ett  [!DNL Azure Blob] lagringsgränssnitt som tillhandahålls av Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att importera och hämta filer in och ut ur plattformen. Mer information finns i [[!DNL Data Landing Zone] översikten](../../sources/connectors/cloud-storage/data-landing-zone.md). |
| [!DNL Snowflake] | Nu kan du skapa en [!DNL Snowflake]-källanslutning med hjälp av [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) eller [användargränssnittet](../../sources/tutorials/ui/create/databases/snowflake.md) för att hämta data från din [!DNL Snowflake]-databas till plattformen. Mer information finns i [[!DNL Snowflake] översikten](../../sources/connectors/databases/snowflake.md). |
| [!DNL SFTP] källförbättringar | Du kan ange ett eget portnummer manuellt när du skapar en [!DNL SFTP]-källanslutning. Mer information finns i [[!DNL SFTP] översikten](../../sources/connectors/cloud-storage/sftp.md). |

Mer information om källor finns i [Källor - översikt](../../sources/home.md).
