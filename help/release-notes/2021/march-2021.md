---
title: Versionsinformation om Adobe Experience Platform mars 2021
description: Versionsinformation mars 2021 för Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 31 mars 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

| Funktion | Beskrivning |
| ------- | ----------- |
| `add_to_array` funktion | Uppdaterad funktionalitet som stöder arrayer som parametrar. |
| `to_array` funktion | Uppdaterad funktionalitet som stöder objekt som parametrar. |

Mer information finns i [[!DNL Data Prep] översikt](../../data-prep/home.md).

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform Segmentation Service har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper från din [!DNL Real-Time Customer Profile] data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform], så att de är lättillgängliga i alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| (Beta) Kantsegmentering | Kantsegmentering utvärderar segment i realtid, vilket möjliggör användning av samma sida och nästa sida vid personalisering. Mer information om kantsegmentering finns i [Översikt över segmenteringsgränssnittet](../../segmentation/ui/overview.md). |
| (Beta) Inkrementell segmentering | Ökar färskheten för befintliga segmentdefinitioner utvärderade i gruppsegmentering till upp till en timme. |

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| ------- | ----------- |
| Beta-källor som går över till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-stöd för komprimerad filinläsning | Du kan nu förhandsgranska och importera komprimerade JSON-filer eller avgränsade filer med hjälp av molnlagringskällor. Mer information finns i självstudiekursen om [samla in molnlagringsdata med API:er](../../sources/tutorials/api/collect/cloud-storage.md). |
| Gränssnittsstöd för rekursiv filöverföring | Du kan nu importera hela mappar rekursivt när du använder en molnlagringskälla. När du importerar en hel mapp måste du se till att dess innehåll delar samma schema. Mer information finns i självstudiekursen om [konfigurera ett dataflöde för molnlagringsanslutningar i användargränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Mer information om källor finns i [källöversikt](../../sources/home.md).
