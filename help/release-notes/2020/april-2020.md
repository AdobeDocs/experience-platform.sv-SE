---
title: Versionsinformation om Adobe Experience Platform april 2020
description: Versionsinformationen för Adobe Experience Platform från april 2020.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: Versionsinformation.
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 104db777446b19fa9e3ea7538ae1dda6f51a00b1
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 26%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 8 april 2020**

Nya funktioner i Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Uppdateringar av befintliga funktioner:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Dataförvaltning](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja kraften i artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskap. Dessutom kan marknadsförare aktivera prognoser i Adobe Experience Cloud, Adobe Experience Platform och tredjepartsprogram.

**Viktiga funktioner**

| Funktion | Beskrivning |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] ger marknadsförarna möjlighet att generera kundprognoser på individnivå med förklaringar. Med hjälp av inflytelserika faktorer kan [!DNL Customer AI] tala om för dig vad en kund är trolig att göra och varför. Dessutom kan marknadsförarna dra nytta av [!DNL Customer AI]-prognoser och insikter för att personalisera kundupplevelser genom att leverera de lämpligaste erbjudandena och meddelandena. |
| [!DNL Attribution AI] | [!DNL Attribution AI] är en algoritmisk attribueringstjänst med flera kanaler som beräknar påverkan och inkrementell påverkan av kundinteraktioner mot angivna utfall. Med [!DNL Attribution AI] kan marknadsförarna mäta och optimera marknadsförings- och annonsutgifterna genom att förstå effekten av varje enskild kundinteraktion under varje fas av kundresan. |

**Kända fel**

* Inga kända problem.

Mer information om [!DNL Intelligent Services] och vad den har att erbjuda finns i [Översikt över intelligenta tjänster](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM) system {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Automatisk alternativ visningsinformation | [!DNL Schema Registry] tillämpar automatiskt de anpassade titel- och beskrivningsvärden som konfigurerats i `alternateDisplayInfo`-beskrivningen. |
| Begränsningar för skalbara fält | [!DNL Schema Registry] tillåter inte mer än 6 000 skalära fält i ett enda schema. |
| Prestandaöversyn | [!DNL Schema Registry] har omarbetats för att kunna utföra och bättre uppfylla kraven för [!DNL Experience Platform]. |

**Felkorrigeringar**

* Uppdaterad XDM till XED konverterad för att stödja ett renare XED-format för kapslade URI-fält i standard-XDM.

**Kända fel**

* Känd

## Dataförvaltning {#governance}

Dataförvaltning i Adobe Experience Platform är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Den spelar en viktig roll inom [!DNL Experience Platform] på olika nivåer, bland annat katalogföring, datahärkomst, märkning av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

För att komma igång med datastyrning krävs en grundlig förståelse för de regler, avtalsförpliktelser och företagspolicyer som gäller för era kunddata. Därifrån kan data klassificeras med hjälp av lämpliga etiketter för dataanvändning, och användningen av dessa kan styras med hjälp av definitionen av policyer för dataanvändning.

Datastyrningsramverket förenklar och effektiviserar processen att kategorisera data och skapa dataanvändningsprinciper via användargränssnittet [!DNL Experience Platform] och API:t [!DNL Policy Service].

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Hantera dataanvändningsprinciper i användargränssnittet | Dataanvändningsprinciper kan nu hanteras inom arbetsytan **Profiler** i användargränssnittet i [!DNL Experience Platform]. Mer information finns i användarhandboken för [principen](../../data-governance/policies/user-guide.md). |

**Kända fel**

* Ingen.

Mer information finns i [Översikt över datastyrning](../../data-governance/home.md).


## Mål {#destinations}

I [Real-Time Customer Data Platform](../../rtcdp/overview.md) är mål färdiga integreringar med målplattformar som aktiverar data till dessa partner på ett smidigt sätt.

**Nya destinationer**

Real-Time CDP har nu stöd för dataaktivering till över femtio [!DNL Experience Cloud Launch]-tillägg, vilket möjliggör analyser, personalisering och andra användningsfall. Mer information finns nedan:

| Dokumentation | Beskrivning |
|--- | ---|
| [Måltyper och -kategorier](../../destinations/destination-types.md) | I den här artikeln förklaras skillnaden mellan anslutningar och tillägg i Real-Time CDP-gränssnittet och en rekommendation om när var och en av dessa destinationer ska användas. |
| [Experience Platform Launch-tillägg](../../destinations/catalog/launch-extensions/overview.md) | Den här sidan förklarar vad [!DNL Launch] tillägg är, visar användningsfall för dem och länkar till dokumentation för varje [!DNL Launch]-tillägg i Real-Time CDP. |

Mer information finns i [Målöversikt](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service] kan du skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-applikationer, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | Begäran om skydd av personuppgifter kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När du gör sekretessförfrågningar i API:et accepterar `regulation`-matrisen värdet ”pdpa_tha”. |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnrymdstyper i Request Builder i användargränssnittet för [!DNL Privacy Service]. Mer information finns i [användarhandboken](../../privacy-service/ui/user-guide.md). |
| Borttagning av gammal slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

Kända fel

* Ingen

Mer information om [!DNL Privacy Service] får du genom att läsa [Privacy Service-översikten](../../privacy-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som du kan strukturera, etikettera och förbättra data med hjälp av [!DNL Experience Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| API- och gränssnittsstöd för databaser | Nya källanslutningar för [!DNL Apache Spark] (på HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage] och [!DNL Hive]. |
| API- och gränssnittsstöd för protokollbaserade program | Nya källanslutningar för [!DNL Generic OData]. |

**Kända fel**

* Ingen

Mer information om källor finns i [Källöversikt](../../sources/home.md).
