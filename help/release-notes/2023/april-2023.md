---
title: Versionsinformation om Adobe Experience Platform april 2023
description: Versionsinformation från april 2023 för Adobe Experience Platform.
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 april 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Dataförberedelse](#data-prep)
- [Källor](#sources)

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av bakåtfyllnadsperiod för Adobe Analytics i icke-produktionssandlådor | Förifyllningsperioden för Adobe Analytics i icke-produktionssandlådor har reducerats till tre månader. Backfill för produktionssandlådor är desamma vid 13 månader. Den här ändringen gäller endast för nya flöden och påverkar inte befintliga flöden. Mer information finns i [Adobe Analytics - översikt](../../sources/connectors/adobe-applications/analytics.md). |
| Ny mappningsfunktion som konverterar FPID-strängar till ECID | Använd `fpid_to_ecid` funktion för att konvertera FPID-strängar till ECID för användning i Experience Platform och Experience Cloud. Mer information finns i [Handbok för dataprefixfunktioner](../../data-prep/functions.md). |

{style="table-layout:auto"}

Mer information om Data Prep finns i [Översikt över datapreflight](../../data-prep/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| API-stöd för filtrering av radnivådata för Microsoft Dynamics, Salesforce CRM och Salesforce Marketing Cloud | Använd logiska operatorer och jämförelseoperatorer för att filtrera radnivådata för källorna i Microsoft Dynamics, Salesforce CRM och Salesforce Marketing Cloud. Läs guiden på [filtrera data för en källa med API](../../sources/tutorials/api/filter.md) för mer information. |
| Betaversion av Shopify Streaming | The [Förminska strömningskälla](../../sources/connectors/ecommerce/shopify-streaming.md) finns nu i betaversion. Använd Shopify Streaming-källan för att strömma data från ditt Shopify-partnerkonto till Experience Platform. |
| Allmän tillgänglighet för OneTrust-integrering | The [OneTrust Integration-källa](../../sources/connectors/consent-and-preferences/onetrust.md) är nu GA. Använd OneTrust Integration-källan för att skicka data om samtycke och inställningar från OneTrust Integration-kontot till Experience Platform. |
| Allmän tillgänglighet för Oracle Service Cloud | The [Oracle Service Cloud-källa](../../sources/connectors/customer-success/oracle-service-cloud.md) är nu GA. Använd Oraclets Service Cloud-källa för att skicka Oracle Service Cloud-data till Experience Platform. |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).
