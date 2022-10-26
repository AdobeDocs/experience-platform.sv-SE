---
title: Versionsinformation om Adobe Experience Platform april 2020
description: Versionsinformation från april 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: Versionsinformation.
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 8 april 2020**

Nya funktioner i Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Uppdateringar av befintliga funktioner:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Datastyrning](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis. Dessutom kan marknadsförare aktivera prognoser i Adobe Experience Cloud, Adobe Experience Platform och tredjepartsprogram.

**Viktiga funktioner**

| Funktion | Beskrivning |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] ger marknadsförarna möjlighet att generera kundprognoser på individnivå med förklaringar. Med hjälp av inflytelserika faktorer [!DNL Customer AI] kan tala om för er vad en kund sannolikt kommer att göra och varför. Dessutom kan marknadsförarna dra nytta av [!DNL Customer AI] prognoser och insikter för att personalisera kundupplevelser genom att leverera de lämpligaste erbjudandena och budskapen. |
| [!DNL Attribution AI] | [!DNL Attribution AI] är en flerkanalig, algoritmisk attribueringstjänst som beräknar påverkan och inkrementell påverkan av kundinteraktioner mot angivna resultat. Med [!DNL Attribution AI]kan marknadsförarna mäta och optimera marknadsförings- och annonsutgifterna genom att förstå effekten av varje enskild kundinteraktion i varje fas av kundresan. |

**Kända fel**

* Inga kända problem.

Mer information om [!DNL Intelligent Services] och vad den har att erbjuda finns i [Intelligent Services - översikt](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Automatisk alternativ visningsinformation | The [!DNL Schema Registry] använder automatiskt de anpassade titel- och beskrivningsvärden som konfigurerats i `alternateDisplayInfo` beskrivning. |
| Begränsningar för skalbara fält | The [!DNL Schema Registry] tillåter inte mer än 6000 skalära fält i ett enda schema. |
| Prestandaöversyn | The [!DNL Schema Registry] har omarbetats för att kunna utföra och uppfylla kraven i [!DNL Experience Platform] bättre. |

**Felkorrigeringar**

* Uppdaterad XDM till XED konverterad för att stödja ett renare XED-format för kapslade URI-fält i standard-XDM.

**Kända fel**

* Känd

## Datastyrning {#governance}

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Det spelar en nyckelroll inom [!DNL Experience Platform] på olika nivåer, inklusive katalogisering, datalinje, märkning av dataanvändning, dataåtkomstregler och åtkomstkontroll av data för marknadsföringsåtgärder.

För att komma igång med datastyrning krävs en grundlig förståelse för de regler, avtalsförpliktelser och företagspolicyer som gäller för era kunddata. Därifrån kan data klassificeras med hjälp av lämpliga etiketter för dataanvändning, och användningen av dessa kan styras med hjälp av definitionen av policyer för dataanvändning.

Datastyrningsramverket förenklar och effektiviserar processen att kategorisera data och skapa dataanvändningspolicyer via [!DNL Experience Platform] användargränssnitt och [!DNL Policy Service] API.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Hantera dataanvändningsprinciper i användargränssnittet | Dataanvändningsprinciper kan nu hanteras i **Profiler** arbetsytan i [!DNL Experience Platform] Gränssnitt. Se [principanvändarhandbok](../../data-governance/policies/user-guide.md) för mer information. |

**Kända fel**

* Ingen.

Mer information finns i [Datastyrning - översikt](../../data-governance/home.md).


## Mål  {#destinations}

I [Real-time Customer Data Platform](../../rtcdp/overview.md)är destinationer färdiga integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

Real-Time CDP har nu stöd för dataaktivering till över femtio [!DNL Experience Cloud Launch] tillägg som möjliggör analyser, personalisering och andra användningsfall. Mer information finns nedan:

| Dokumentation | Beskrivning |
|--- | ---|
| [Måltyper och -kategorier](../../destinations/destination-types.md) | I den här artikeln förklaras skillnaden mellan anslutningar och tillägg i Real-Time CDP-gränssnittet och en rekommendation om när var och en av dessa destinationer ska användas. |
| [Experience Platform Launch-tillägg](../../destinations/catalog/launch-extensions/overview.md) | Den här sidan förklarar vad [!DNL Launch] är, visar användningsexempel för dem och länkar till dokumentation för [!DNL Launch] i Real-Time CDP. |

Mer information finns i [Översikt över destinationer](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful-API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service]kan du skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessregler.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | Begäran om skydd av personuppgifter kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När sekretessförfrågningar görs i API:t `regulation` arrayen accepterar värdet &quot;pdpa_tha&quot;. |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i [!DNL Privacy Service] Gränssnitt. Se [användarhandbok](../../privacy-service/ui/user-guide.md) för mer information. |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

Kända fel

* Ingen

Mer information om [!DNL Privacy Service], kan du börja med att läsa [Översikt över Privacy Servicen](../../privacy-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| API- och gränssnittsstöd för databaser | Nya källkopplingar för [!DNL Apache Spark] (på HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (på HDInsights), och [!DNL Phoenix]. |
| API- och gränssnittsstöd för betalningsbaserade program | Nya källkopplingar för [!DNL PayPal]. |
| API- och gränssnittsstöd för protokollbaserade program | Nya källkopplingar för [!DNL Generic OData]. |

**Kända fel**

* Ingen

Mer information om källor finns i [källöversikt](../../sources/home.md).
