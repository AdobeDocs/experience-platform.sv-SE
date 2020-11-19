---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 8 april 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 8 april 2020**

Nya funktioner i Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Uppdateringar av befintliga funktioner:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [[!DNL Data Governance]](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis. Dessutom kan marknadsförare aktivera prognoser i Adobe Experience Cloud, Adobe Experience Platform och tredjepartsprogram.

**Viktiga funktioner**

| Funktion | Beskrivning |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] ger marknadsförarna möjlighet att generera kundprognoser på individnivå med förklaringar. Med hjälp av inflytelserika faktorer kan [!DNL Customer AI] ni tala om för er vad en kund kan göra och varför. Dessutom kan marknadsförarna dra nytta av [!DNL Customer AI] prognoser och insikter för att personalisera kundupplevelser genom att leverera de lämpligaste erbjudandena och budskapen. |
| [!DNL Attribution AI] | [!DNL Attribution AI] är en flerkanalig, algoritmisk attribueringstjänst som beräknar påverkan och inkrementell påverkan av kundinteraktioner mot angivna resultat. Med [!DNL Attribution AI]kan marknadsförarna mäta och optimera marknadsförings- och annonsutgifterna genom att förstå effekten av varje enskild kundinteraktion i varje fas av kundresan. |

**Kända fel**

* Inga kända problem.

Mer information om [!DNL Intelligent Services] och vad det har att erbjuda finns i [Intelligent Services - översikt](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardisering och interoperabilitet är viktiga koncept som ligger bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Automatisk alternativ visningsinformation | De anpassade titel- och beskrivningsvärdena som konfigurerats i [!DNL Schema Registry] `alternateDisplayInfo` beskrivningen används automatiskt. |
| Begränsningar för skalbara fält | Det går [!DNL Schema Registry] inte att använda fler än 6 000 skalära fält i ett enda schema. |
| Prestandaöversyn | Programmet [!DNL Schema Registry] har omarbetats för att kunna prestera och uppfylla kraven på [!DNL Experience Platform] bättre. |

**Felkorrigeringar**

* Uppdaterad XDM till XED konverterad för att stödja ett renare XED-format för kapslade URI-fält i standard-XDM.

**Kända fel**

* Känd

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och regler som gäller för dataanvändning följs. Det spelar en viktig roll på [!DNL Experience Platform] olika nivåer, bland annat i fråga om katalogisering, datalinje, etikettering av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

För att komma igång med datastyrning krävs en grundlig förståelse för de regler, avtalsförpliktelser och företagspolicyer som gäller för era kunddata. Därifrån kan data klassificeras med hjälp av lämpliga etiketter för dataanvändning, och användningen av dessa kan styras med hjälp av definitionen av policyer för dataanvändning.

Ramverket [!DNL Data Governance] förenklar och effektiviserar processen att kategorisera data och skapa dataanvändningsprinciper via [!DNL Experience Platform] användargränssnittet och [!DNL Policy Service] API.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Hantera dataanvändningsprinciper i användargränssnittet | Dataanvändningsprinciper kan nu hanteras inom arbetsytan **Profiler** i [!DNL Experience Platform] gränssnittet. Mer information finns i användarhandboken [för](../../data-governance/policies/user-guide.md) profilen. |

**Kända fel**

* Ingen.

Mer information finns i översikten över [datastyrning](../../data-governance/home.md).


## Mål {#destinations}

I kunddataplattformen [i](../../rtcdp/overview.md)realtid är mål färdiga integreringar med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

Adobe CDP i realtid har nu stöd för dataaktivering i över femtio [!DNL Experience Cloud Launch] tillägg, vilket möjliggör analyser, personalisering och andra användningsfall. Mer information finns nedan:

| Dokumentation | Beskrivning |
|--- | ---|
| [Måltyper och -kategorier](/help/rtcdp/destinations/destination-types.md) | I den här artikeln förklaras skillnaden mellan anslutningar och tillägg i CDP-gränssnittet i realtid för Adobe och en rekommendation om när var och en av dessa destinationer ska användas. |
| [Experience Platform Launch-tillägg](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | På den här sidan förklaras vad [!DNL Launch] tillägg är, en lista över användningsfall för dem och länkar till dokumentation för varje [!DNL Launch] tillägg i Adobe Real-time CDP. |

Mer information finns i Översikt över [destinationer](/help/rtcdp/destinations/destinations-overview.md).

## [!DNL Privacy Service] {#privacy}

Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Adobe Experience Platform [!DNL Privacy Service] tillhandahåller ett RESTful API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service]kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | Begäran om skydd av personuppgifter kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När du gör sekretessförfrågningar i API:t accepterar arrayen värdet &quot;pdpa_tha&quot;. `regulation` |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i [!DNL Privacy Service] användargränssnittet. Mer information finns i [användarhandboken](../../privacy-service/ui/user-guide.md) . |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

Kända fel

* Ingen

Mer information [!DNL Privacy Service]finns i [Privacy Servicen](../../privacy-service/home.md).

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| API- och gränssnittsstöd för databaser | Nya källkontakter för [!DNL Apache Spark] (HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage][!DNL Hive] (HDInsights) och [!DNL Phoenix]. |
| API- och gränssnittsstöd för betalningsbaserade program | Nya källkopplingar för [!DNL PayPal]. |
| API- och gränssnittsstöd för protokollbaserade program | Nya källkopplingar för [!DNL Generic OData]. |

**Kända fel**

* Ingen

Mer information om källor finns i [Källöversikt](../../sources/home.md).
