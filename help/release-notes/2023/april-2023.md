---
title: Versionsinformation om Adobe Experience Platform april 2023
description: Versionsinformation från april 2023 för Adobe Experience Platform.
source-git-commit: 938b4ba7affadc7ad0eca086d7cc2c9ce1a54a83
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 april 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Dataförberedelse](#data-prep)
- [Experience Data Model](#xdm)
- [Kundprofil i realtid](#profile)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner** {#dashboards-new-updated-features}

| Funktion | Beskrivning |
| --- | --- |
| Användardefinierade kontrollpaneler | Nu kan du **filtrera historiska data** utifrån widgetens insikter och använd antingen senaste data eller en anpassad analysperiod.<br>Du kan också göra det nu **duplicera dina befintliga widgetar**. Genom att anpassa en dubblett och redigera deras attribut kan du undvika att starta om från början när du skapar en ny, unik widget. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikt över instrumentpaneler](../../dashboards/home.md).

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av bakåtfyllnadsperiod för Adobe Analytics i icke-produktionssandlådor | Förifyllningsperioden för Adobe Analytics i icke-produktionssandlådor har reducerats till tre månader. Backfill för produktionssandlådor är desamma vid 13 månader. Den här ändringen gäller endast för nya flöden och påverkar inte befintliga flöden. Mer information finns i [Adobe Analytics - översikt](../../sources/connectors/adobe-applications/analytics.md). |
| Ny mappningsfunktion som konverterar FPID-strängar till ECID | Använd `fpid_to_ecid` funktion för att konvertera FPID-strängar till ECID för användning i Experience Platform och Experience Cloud. Mer information finns i [Handbok för dataprefixfunktioner](../../data-prep/functions.md). |

{style="table-layout:auto"}

Mer information om Data Prep finns i [Översikt över datapreflight](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Växla visningsnamn | Schemaredigeraren har nu en funktion för att växla mellan de ursprungliga fältnamnen och de mer läsbara visningsnamnen. Tack vare den här flexibiliteten blir det enklare att hitta och redigera dina scheman. Visningsnamnen för standardfältgrupper genereras av systemet men kan vid behov anpassas via användargränssnittet. |

{style="table-layout:auto"}

Mer information om XDM in Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förfallodatum för pseudonyma profiler | Nu kan pseudonyma profildata förfalla. Den här versionen tar kontinuerligt bort inaktuella pseudonyma profiler från din Experience Platform-instans när den har aktiverats. Läs mer om den här funktionen och pseudonyma profiler i [Förfalloguide för pseudonyma profildata](../../profile/pseudonymous-profiles.md). |

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
