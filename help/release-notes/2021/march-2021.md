---
title: Versionsinformation om Adobe Experience Platform mars 2021
description: Versionsinformationen för Adobe Experience Platform i mars 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 30%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 31 mars 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

| Funktion | Beskrivning |
| ------- | ----------- |
| Funktionen `add_to_array` | Uppdaterad funktionalitet som stöder arrayer som parametrar. |
| Funktionen `to_array` | Uppdaterad funktionalitet som stöder objekt som parametrar. |

Mer information finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-Time Customer Profile]-data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Experience Platform], vilket gör dem tillgängliga för alla Adobe-program.

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| (Beta) Edge segmentering | Edge segmentering utvärderar segment i realtid, vilket möjliggör användning av samma sida och nästa sida vid personalisering. Mer information om kantsegmentering finns i [Översikt över segmenteringsgränssnittet](../../segmentation/ui/overview.md). |
| (Beta) Inkrementell segmentering | Ökar färskheten för befintliga segmentdefinitioner utvärderade i gruppsegmentering till upp till en timme. |

Mer information om [!DNL Segmentation Service] finns i [segmenteringsöversikten](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

| Funktion | Beskrivning |
| ------- | ----------- |
| Beta-källor som övergår till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-stöd för komprimerad filinläsning | Du kan nu förhandsgranska och importera komprimerade JSON-filer eller avgränsade filer med hjälp av molnlagringskällor. Mer information finns i självstudiekursen [Samla in molnlagringsdata med API:er](../../sources/tutorials/api/collect/cloud-storage.md). |
| Gränssnittsstöd för rekursiv filöverföring | Du kan nu importera hela mappar rekursivt när du använder en molnlagringskälla. När du importerar en hel mapp måste du se till att dess innehåll delar samma schema. Mer information finns i självstudiekursen om att [konfigurera ett dataflöde för molnlagringsanslutningar i användargränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
