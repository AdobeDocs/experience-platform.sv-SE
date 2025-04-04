---
title: Versionsinformation om Adobe Experience Platform september 2021
description: Versionsinformationen för Adobe Experience Platform från september 2021.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 22%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 29 september 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainmatning](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Källor](#sources)

## Datainmatning {#ingestion}

Adobe Experience Platform datainmatning representerar de olika metoder som Experience Platform använder för att importera data från olika källor, samt hur data lagras i Data Lake för användning i Experience Platform-tjänster längre fram i kedjan.

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Uppgradera eller korrigera profilposter med hjälp av gruppinmatning | Real-Time Customer Profile tillåter nu uppdateringar av profilattribut i enskilda profilpostdata via batchinmatning. Mer information finns i [Utvecklarhandboken för gruppintagning](../../ingestion/batch-ingestion/api-overview.md). |

Mer information om hur du importerar data till Experience Platform finns i [dokumentationen för datainmatning](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för strömmande dataflöden | Du kan nu använda dataprep-funktioner när du skapar ett direktuppspelat dataflöde för [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] och [!DNL Google PubSub]. Mer information finns i självstudiekursen [Skapa ett direktuppspelat dataflöde för molnlagringskällor](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md). |

Mer information om [!DNL Data Prep] finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Data Landing Zone] | Du kan nu skapa en [!DNL Data Landing Zone]-källanslutning med [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) eller [användargränssnittet](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] är ett [!DNL Azure Blob]-lagringsgränssnitt som tillhandahålls av Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att hämta filer till Experience Platform. Mer information finns i [[!DNL Data Landing Zone] översikten](../../sources/connectors/cloud-storage/data-landing-zone.md). |
| [!DNL Snowflake] | Du kan nu skapa en [!DNL Snowflake]-källanslutning med [[!DNL Flow Service]  API ](../../sources/tutorials/api/create/databases/snowflake.md) eller [användargränssnittet](../../sources/tutorials/ui/create/databases/snowflake.md) för att hämta data från din [!DNL Snowflake]-databas till Experience Platform. Mer information finns i [[!DNL Snowflake] översikten](../../sources/connectors/databases/snowflake.md). |
| [!DNL SFTP] källförbättringar | Du kan ange ett eget portnummer manuellt när du skapar en [!DNL SFTP]-källanslutning. Mer information finns i [[!DNL SFTP] översikten](../../sources/connectors/cloud-storage/sftp.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
