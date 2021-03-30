---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform för 31 mars 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 31 mars 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

Följande uppdateringar av källor finns i mars 2021-utgåvan av Experience Platform:

| Funktion | Beskrivning |
| ------- | ----------- |
| Beta-källor som går över till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-stöd för komprimerad filinläsning | Du kan nu förhandsgranska och importera komprimerade JSON-filer eller avgränsade filer med hjälp av molnlagringskällor. Mer information finns i självstudiekursen om att [samla in molnlagringsdata med API:er](../../sources/tutorials/api/collect/cloud-storage.md). |
| Gränssnittsstöd för rekursiv filöverföring | Du kan nu importera hela mappar rekursivt när du använder en molnlagringskälla. När du importerar en hel mapp måste du se till att dess innehåll delar samma schema. Mer information finns i självstudiekursen om att [konfigurera ett dataflöde för molnlagringskopplingar i gränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Mer information om källor finns i [Källor - översikt](../../sources/home.md).
