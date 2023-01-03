---
title: Adobe Experience Platform Release Notes september 2021
description: Versionsinformation för september 2021 för Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '377'
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
| Uppgradera eller korrigera profilposter med hjälp av gruppinmatning | Real-Time Customer Profile tillåter nu uppdateringar av profilattribut i enskilda profilpostdata via batchinmatning. Mer information finns i [Utvecklarhandbok för batchintag](../../ingestion/batch-ingestion/api-overview.md). |

Läs mer om hur du hämtar in data till Platform på [Dokumentation för datainmatning](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för strömmande dataflöden | Nu kan du använda förinställningsfunktioner för data när du skapar ett direktuppspelat dataflöde för [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]och [!DNL Google PubSub]. Se självstudiekursen om [skapa ett direktuppspelat dataflöde för molnlagringskällor](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) för mer information. |

Mer information om [!DNL Data Prep] se [[!DNL Data Prep] översikt](../../data-prep/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Data Landing Zone] | Nu kan du skapa en [!DNL Data Landing Zone] källanslutning med [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) eller [användargränssnitt](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] är en [!DNL Azure Blob] lagringsgränssnittet som tillhandahålls av Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att hämta filer till plattformen. Se [[!DNL Data Landing Zone] översikt](../../sources/connectors/cloud-storage/data-landing-zone.md) för mer information. |
| [!DNL Snowflake] | Nu kan du skapa en [!DNL Snowflake] källanslutning med [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) eller [användargränssnitt](../../sources/tutorials/ui/create/databases/snowflake.md) för att hämta data från [!DNL Snowflake] databas till plattform. Se [[!DNL Snowflake] översikt](../../sources/connectors/databases/snowflake.md) för mer information. |
| [!DNL SFTP] källförbättringar | Du kan ange ett eget portnummer manuellt när du skapar ett [!DNL SFTP] källanslutning. Se [[!DNL SFTP] översikt](../../sources/connectors/cloud-storage/sftp.md) för mer information. |

Mer information om källor finns i [källöversikt](../../sources/home.md).
