---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 27 januari 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: cf70b21f3a8c02b25e5acd3be8c8feaa3f52a5e3
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 27 januari 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Funktioner för reguljära uttryck | [!DNL Data Prep] Mapper har nu stöd för att matcha och extrahera delar av indatafältet baserat på reguljära uttryck. |

Mer information finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av Adobe Audience Manager källanslutning | Nu kan du filtrera och välja enskilda förstahandssegment från Audience Manager till att importera till Platform, samt filtrera bort förstahandsegenskaper. Mer information finns i självstudiekursen om att [skapa en Audience Manager-källkoppling](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| [!DNL Google BigQuery] förbättringar av källkopplingen | Du kan nu importera filer som är större än 10 GB i en flödeskörning med hjälp av [!DNL BigQuery]-källkopplingen. Mer information finns i [[!DNL BigQuery] översikten över källkopplingen](../../sources/connectors/databases/bigquery.md). |
| Stöd för komplexa datatyper för molnlagring | Du kan nu importera komplexa datatyper, till exempel arrayer i JSON-filer, när du använder en anslutning till en molnlagringskälla. Självstudiekurserna om hur du skapar ett molnlagringsdataflöde [i gränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) eller [med API [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) innehåller mer information. |
| Stöd för huvudnyckelbaserad autentisering för [!DNL Microsoft Dynamics]-källa | Du kan nu autentisera ditt [!DNL Dynamics]-konto med en tjänsthuvudnyckel som ett alternativ till lösenordsbaserad autentisering. Mer information finns i [[!DNL Dynamics] översikten över källkopplingen](../../sources/connectors/crm/ms-dynamics.md). |

Mer information om källor finns i [Källor - översikt](../../sources/home.md).
