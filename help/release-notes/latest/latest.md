---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation om Experience Platform 8 april 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: dc1c9b7dd9ff4c8b20de96e4ee123d90be4580cc

---


# Versionsinformation om Adobe Experience Platform

## Releasedatum: 8 april 2020

## Experience Data Model (XDM) System

Standardisering och interoperabilitet är viktiga begrepp bakom Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

### Nya funktioner

| Funktion | Beskrivning |
| --- | --- |
| Automatisk alternativ visningsinformation | Schemaregistret tillämpar automatiskt de anpassade titel- och beskrivningsvärden som konfigurerats i `alternateDisplayInfo` beskrivningen. |
| Begränsningar för skalbara fält | Schemaregistret tillåter inte mer än 6 000 skalära fält i ett enda schema. |
| Prestandaöversyn | Schemaregistret har omarbetats för att fungera bättre och uppfylla kraven i Experience Platform. |

**Felkorrigeringar**

* Uppdaterad XDM till XED konverterad för att stödja ett renare XED-format för kapslade URI-fält i standard-XDM.

**Kända fel**

* Känd

## Datastyrning

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll inom Experience Platform på olika nivåer, bland annat i fråga om katalogisering, datalinje, märkning av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

För att komma igång med datastyrning krävs en grundlig förståelse för de regler, avtalsförpliktelser och företagspolicyer som gäller för era kunddata. Därifrån kan data klassificeras med hjälp av lämpliga etiketter för dataanvändning, och användningen av dessa kan styras med hjälp av definitionen av policyer för dataanvändning.

DULE-ramverket förenklar och effektiviserar processen att kategorisera data och skapa dataanvändningsprinciper via Experience Platform-gränssnittet och DULE Policy Service API.

### Nya funktioner

| Funktion | Beskrivning |
| -----------| ---------- |
| Hantera dataanvändningsprinciper i användargränssnittet | Dataanvändningsprinciper kan nu hanteras i arbetsytan _Principer_ i användargränssnittet för Experience Platform. Mer information finns i användarhandboken [för](../../data-governance/policies/user-guide.md) profilen. |

**Kända fel**

* Ingen.

Mer information finns i översikten över [datastyrning](../../data-governance/home.md).


## Mål 

I [Adobes kunddataplattform](../../rtcdp/overview.md)i realtid är destinationer färdigbyggda integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

### Nya destinationer

Adobe CDP stöder nu dataaktivering i realtid i över femtio Experience Cloud Launch-tillägg, vilket möjliggör analyser, personalisering och andra användningsfall. Mer information finns nedan:

| Dokumentation | Beskrivning |
|--- | ---|
| [Måltyper och -kategorier](/help/rtcdp/destinations/destination-types.md) | I den här artikeln förklaras skillnaden mellan anslutningar och tillägg i Adobe-gränssnittet för CDP i realtid och en rekommendation om när var och en av dessa destinationer ska användas. |
| [Experience Platform Launch-tillägg](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | På den här sidan förklaras vad Launch-tillägg är, används exempel på dem och länkar till dokumentation för varje Launch-tillägg i Adobe Real-time CDP. |

Mer information finns i Översikt över [destinationer](/help/rtcdp/destinations/destinations-overview.md).

## Intelligenta tjänster

Intelligenta tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis. Dessutom kan marknadsförare aktivera prognoser i Adobe Experience Cloud, Adobe Experience Platform och tredjepartsprogram.

**Viktiga funktioner**

| Funktion | Beskrivning |
|---|---|
| Kund-AI | Kunds-AI ger marknadsförarna möjlighet att generera kundprognoser på individnivå med förklaringar. Med hjälp av inflytelserika faktorer kan kundens AI tala om för er vad en kund kan tänkas göra och varför. Dessutom kan marknadsförarna dra nytta av kundernas AI-prognoser och insikter för att personalisera kundupplevelser genom att leverera de lämpligaste erbjudandena och budskapen. |
| Attribution AI | Attribution AI är en flerkanals algoritmisk attribueringstjänst som beräknar påverkan och inkrementell påverkan av kundinteraktioner mot angivna resultat. Med Attribution AI kan marknadsförarna mäta och optimera marknadsförings- och annonskostnader genom att förstå effekten av varje enskild kundinteraktion under varje fas av kundresan. |

**Kända fel**

* Inga kända problem.

Mer information om intelligenta tjänster och vad de har att erbjuda finns i [Intelligent Services - översikt](../../intelligent-services/home.md).

## Integritetstjänst

Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Integritetstjänsten för Adobe Experience Platform tillhandahåller ett RESTful API och användargränssnitt som hjälper er att hantera dessa dataförfrågningar från era kunder. Med Integritetstjänsten kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | Begäran om skydd av personuppgifter kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När du gör sekretessförfrågningar i API:t accepterar arrayen värdet &quot;pdpa_tha&quot;. `regulation` |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i Sekretessgränssnittet. Mer information finns i [användarhandboken](../../privacy-service/ui/user-guide.md) . |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

Kända fel

* Ingen

Mer information om sekretesstjänsten finns i översikten över [sekretesstjänsten](../../privacy-service/home.md).

## Källor

Adobe Experience Platform kan importera data från externa källor samtidigt som ni kan strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, programvara från tredje part och ditt CRM-system.

Experience Platform har ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

### Nya funktioner

| Funktion | Beskrivning |
| ------- | ----------- |
| API- och gränssnittsstöd för databaser | Nya källanslutningar för Apache Spark (på HDInsights), Azure Synapse Analytics, Azure Table Storage, Hive (på HDInsights) och Phoenix. |
| API- och gränssnittsstöd för betalningsbaserade program | Nya källanslutningar för PayPal. |
| API- och gränssnittsstöd för protokollbaserade program | Nya källkopplingar för allmänna OData. |

### Kända fel

* Ingen

Mer information om källor finns i [Källöversikt](../../source-connectors/home.md).