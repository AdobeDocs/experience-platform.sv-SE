---
title: Adobe Experience Platform Release Notes januari 2024
description: Versionsinformationen för Adobe Experience Platform i januari 2024.
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 30 januari 2024**

Nya funktioner i Adobe Experience Platform:

- [Spelböcker med användningsexempel](#use-case-playbooks)

Uppdateringar av befintliga funktioner i Experience Platform:

- [Attributbaserad åtkomstkontroll](#abac)
- [Dataförberedelse](#data-prep)
- [Kontrollpaneler](#dashboards)
- [Mål ](#destinations)
- [Identitetstjänst](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Spelböcker med användningsexempel {#use-case-playbooks}

Funktionen [!UICONTROL Use Case Playbooks] är nu allmänt tillgänglig för alla Real-Time CDP- och Adobe Journey Optimizer-kunder. [!UICONTROL Use Case Playbooks] är utformade för att hjälpa användare att övervinna utmaningar när de börjar med Real-time Customer Data Platform eller Adobe Journey Optimizer. När du är osäker på var du ska börja eller hur du ska skapa rätt material för dina behov kan du få inspiration med Use Case Playbooks och skapa olika resurser så att du kan testa och importera till produktionsmiljöer när du är klar.

Läs följande dokumentationssidor för att komma igång med [!UICONTROL Use Case Playbooks]:

- Läs [översiktssidan](/help/use-case-playbooks/playbooks/overview.md) för att förstå syfte, tillgänglighetsinformation och för att få en heltäckande demonstration av hur spelböcker fungerar, från identifiering till skapande av instanser, till import av genererade resurser till andra sandlådemiljöer.
- Hämta en lista med alla [tillgängliga spelningsböcker](/help/use-case-playbooks/playbooks/playbooks-list.md), grupperade efter produkt (Real-Time CDP eller Journey Optimizer)
- Hämta information om alla [nödvändiga behörigheter](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) för att använda spelböcker och de resurser som genereras av spelböckerna.
- Förstå funktionen [för dataidentifiering](/help/use-case-playbooks/playbooks/data-awareness.md) som gör att du kan kopiera genererade resurser till andra sandlådemiljöer
- Få [felsökningstips](/help/use-case-playbooks/playbooks/troubleshooting.md) om du stöter på fel eller problem när du använder Använd fallspelningsböcker.

## Attributbaserad åtkomstkontroll {#abac}

Attributbaserad åtkomstkontroll är en funktion hos Adobe Experience Platform som ger sekretessmedvetna varumärken större flexibilitet att hantera användaråtkomst. Enskilda objekt som schemafält och segment kan tilldelas användarroller. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika plattformsanvändare i organisationen.

Tack vare attributbaserad åtkomstkontroll kan administratören styra användarnas åtkomst till, känsliga personuppgifter (SPD), personligt identifierbar information (PII) och andra anpassade typer av data i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

**Ny eller uppdaterad dokumentation**

| Dokumentation - uppdatering | Beskrivning |
| --- | --- |
| Nya API-slutpunkter dokumenteras för attributbaserad åtkomstkontroll | Referenshandboken för [API:t för åtkomstkontroll](https://developer.adobe.com/experience-platform-apis/references/access-control/) innehåller nu attributbaserade API-roller, principer och produktslutpunkter. De här slutpunkterna kan användas för att hämta relevanta roller, principer och produkter för en användare för angivna resurser i en angiven sandlåda. |

{style="table-layout:auto"}

Mer information om attributbaserad åtkomstkontroll finns i [Översikt över attributbaserad åtkomstkontroll](../../access-control/abac/overview.md). En utförlig guide om det attributbaserade arbetsflödet för åtkomstkontroll finns i [attributbaserad åtkomstkontroll från början till slut](../../access-control/abac/end-to-end-guide.md).

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya mappningsfunktioner | <ul><li>`object_to_map`: Använd funktionen `object_to_map` för att skapa mappningsdatatyper. Den här funktionen stöder flera olika syntaxer. Mer information finns i handboken om [funktioner för hierarkier - objekt](../../data-prep/functions.md#objects). </li><li>`to_map`: Använd funktionen `to_map` för att skapa en karta med angivna fältnamn och värdepar med hjälp av objekt. Mer information finns i handboken om [funktioner för hierarkier - kartor](../../data-prep/functions.md#map). </li><li>`array_to_map`: Använd funktionen `array_to_map` för att skapa en karta med angivna fältnamn och värdepar med hjälp av objektarrayer. Mer information finns i handboken om [funktioner för hierarkier - kartor](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Mer information om Prep av data finns i [Översikt över Prep av data](../../data-prep/home.md).

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Visa SQL | Nu kan du visa SQL bakom dina profiler, målgrupper, destinationer och anpassade insikter med växlingsknappen Visa SQL och sedan köra frågan på begäran via Frågeredigeraren. Genom att få tillgång till den SQL som ligger till grund för dina Real-time Customer Data Platform-insikter kan du förstå logiken bakom analysen av din datamodell. Denna transparens gör CDP-data i realtid i Adobe mer tillgängliga, begripliga och slagkraftiga för beslutsfattande.<br>Hämta inspiration från SQL av över 40 befintliga insikter för att skapa nya frågor som härleder unika insikter från plattformsdata baserat på dina affärsbehov. SQL är också tillgängligt för dina [profiler](../../dashboards/insights/profiles.md), [målgrupper](../../dashboards/insights/audiences.md) och [måladresser](../../dashboards/insights/destinations.md) i Experience League-dokumentationen. Dokumenten belyser de användningsfall som kan besvaras med standardinsikter. Mer information finns i guiden om att [visa insikter i SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikten för kontrollpaneler](../../dashboards/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya mål** {#new-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [Publicerad anslutning](../../destinations/catalog/advertising/pubmatic.md) | Använd det här målet för att skicka målgruppsdata till plattformen [!DNL PubMatic Connect]. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Ny **antagen roll**-autentiseringstyp för Amazon S3-mål | Använd den nya rollautentiseringstypen när du ansluter Experience Platform till dina Amazon S3-bucket om du inte vill dela kontonycklar och hemliga nycklar med Experience Platform. Läs mer om den nya autentiseringsmetoden i [autentiseringsavsnittet](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) i Amazon S3-dokumentationen. |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Identitetstjänst {#identity-service}

Adobe Experience Platform identitetstjänst ger er en heltäckande bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Ny eller uppdaterad dokumentation**

| Dokumentation - uppdatering | Beskrivning |
| --- | --- |
| Omstrukturering av dokumentation | Identitetstjänstens dokumentation har omstrukturerats för att förbättra presentationen och tydligheten i begrepp inom identitetstjänsten:<ul><li>Besök [Översiktssidan för identitetstjänsten](../../identity-service/home.md) om du vill ha en utökad terminologiguide, ett exempel med en typisk kundresa, en beskrivning av hur identitetstjänsten länkar samman identiteter och en sammanfattning av den roll som identitetstjänsten har i Experience Platform-ekosystemet.</li><li>Läs guiden [Förstå relationen mellan identitetstjänsten och kundprofilen i realtid](../../identity-service/identity-and-profile.md) för en detaljerad sammanfattning av hur de två tjänsterna samverkar och skillnaderna mellan deras syften, processer, indata och utdata.</li><li>I guiden [Identitetstjänstens länkningslogik](../../identity-service/features/identity-linking-logic.md) finns förklaringar och visualiseringar av hur identitetsdiagrammet beter sig utifrån olika scenarier och tidsstämplar.</li></ul> |

{style="table-layout:auto"}

Läs [Översikt över identitetstjänsten](../../identity-service/home.md) om du vill veta mer om identitetstjänsten.

## Real-Time Customer Data Platform {#rtcdp}

Real-time Customer Data Platform ([!DNL Real-Time CDP]) bygger på Experience Platform och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. [!DNL Real-Time CDP] kombinerar flera företagsdatakällor för att skapa kundprofiler i realtid. Segment som byggts utifrån dessa profiler kan sedan skickas till efterföljande destinationer för att tillhandahålla personliga kundupplevelser i alla kanaler och enheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av [Real-Time CDP hemsida](https://experience.adobe.com) | <ul><li>**Profilwidget**: Nu kan du använda profilwidgeten för att navigera till sidan Profiler - översikt och visa profilmått för din organisation.</li><li>**Profilmätningskort**: Profilmätningskortet på kontrollpanelen för startsidan visar nu det totala antalet profiler i organisationen, beroende på din respektive sammanfogningsprincip.</li><li>**Widget för scheman**: Nu kan du använda schemwidgeten för att navigera till arbetsflödet för att skapa scheman i användargränssnittet.</li></ul> |

{style="table-layout:auto"}

**Ny eller uppdaterad dokumentation**

| Dokumentation - uppdatering | Beskrivning |
| --- | --- |
| Ny startsida för Real-Time CDP-dokumentation | Besök den [nya Real-Time CDP-dokumentationssidan](/help/rtcdp/home.md) om du snabbt vill ha information om hur du kommer igång med produkten, skyddsutkast, exempel på användning och mycket annat. |
| Exempel på Real-Time CDP användningsexempel - översikt | Besök [översiktssidan ](/help/rtcdp/use-case-guides/overview.md) med exempel på hur din organisation kan använda Real-Time CDP. |

{style="table-layout:auto"}

Läs [Real-Time CDP-översikten](../../rtcdp/overview.md) om du vill veta mer om Real-Time CDP.

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar av lokalisering av profilvisningsprogrammets standardinstrumentpanelskort | Standardprofilkorten har nu dynamiskt lokaliserade namn. Anpassade profilkort kan även fortsättningsvis ha egna namn som kan redigeras. |

{style="table-layout:auto"}

Läs [Profilöversikt](../../profile/home.md) om du vill veta mer om kundprofilen i realtid.

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss delmängd av profiler genom att beskriva kriterierna som särskiljer en marknadsföringsbar grupp av personer inom din kundbas. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Externt genererad målgruppsuppladdning | Det maximala antalet kolumner har ökats till **25**. |
| Uppskattningar av segmentbyggaren | Uppskattningar och kvalificerade profiler visas nu i avsnittet för målgruppsegenskaper. Mer information om den här ändringen finns i [gränssnittsguiden för segmentbyggaren](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikt](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite]-källor | Använd [!DNL Oracle NetSuite]-integreringarna i källkatalogen för att hämta data från dina [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)- och [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md)-konton till Experience Platform. |
| [!BADGE Beta]{type=Informative} [!DNL Braze Currents] källa | Använd integreringen [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) i källkatalogen för att hämta data från ditt [!DNL Braze]-konto till Experience Platform. |
| Stöd för autentisering med nyckelpar för batchkällan [!DNL Snowflake] | Du kan nu använda nyckelpars-autentisering när du skapar ett nytt [!DNL Snowflake]-konto för batchdata. Mer information finns i guiden om att [skapa ett [!DNL Snowflake] konto med API:t](../../sources/tutorials/api/create/databases/snowflake.md) eller i guiden om att [skapa ett [!DNL Snowflake] konto med användargränssnittet](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Läs [Källöversikten](../../sources/home.md) om du vill veta mer om källor.
