---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation januari 2024 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 7b694ad1b064279fcc0dd09bd1e8761e734e7556
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 30 januari 2024**

Nya funktioner i Adobe Experience Platform:

- [Använd fallspelningsböcker](#use-case-playbooks)

Uppdateringar av befintliga funktioner i Experience Platform:

- [Attributbaserad åtkomstkontroll](#abac)
- [Dataförberedelse](#data-prep)
- [Kontrollpaneler](#dashboards)
- [Mål ](#destinations)
- [Identitetstjänst](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Kundprofil i realtid](#profile)
- [Källor](#sources)

## Använd fallspelningsböcker {#use-case-playbooks}

The [!UICONTROL Use Case Playbooks] är nu allmänt tillgängliga för alla kunder som har Real-Time CDP och Adobe Journey Optimizer. [!UICONTROL Use Case Playbooks] är utformade för att hjälpa användare att klara utmaningar när de börjar med Real-time Customer Data Platform eller Adobe Journey Optimizer. När du är osäker på var du ska börja eller hur du ska skapa rätt material för dina behov kan du få inspiration med Use Case Playbooks och skapa olika resurser så att du kan testa och importera till produktionsmiljöer när du är klar.

Så här kommer du igång med [!UICONTROL Use Case Playbooks]kan du läsa följande dokumentationssidor:

- Läs [översiktssida](/help/use-case-playbooks/playbooks/overview.md) för att förstå syfte, tillgänglighetsinformation och få en heltäckande demonstration av hur spelböcker fungerar, från identifiering till skapande av instanser, till import av genererade resurser till andra sandlådemiljöer.
- Få en lista över alla [tillgängliga spelböcker](/help/use-case-playbooks/playbooks/playbooks-list.md), grupperade efter produkt (Real-Time CDP eller Journey Optimizer)
- Hämta information om alla [nödvändiga behörigheter](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) om du vill använda spelböcker och de resurser som spelböckerna genererar.
- Förstå [funktioner för datainlärning](/help/use-case-playbooks/playbooks/data-awareness.md) som gör att du kan kopiera genererade resurser till andra sandlådemiljöer
- Hämta [felsökningstips](/help/use-case-playbooks/playbooks/troubleshooting.md) om du stöter på fel eller problem när du använder Använd fallspelningsböcker.

## Attributbaserad åtkomstkontroll {#abac}

Attributbaserad åtkomstkontroll är en funktion hos Adobe Experience Platform som ger sekretessmedvetna varumärken större flexibilitet att hantera användaråtkomst. Enskilda objekt som schemafält och segment kan tilldelas användarroller. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika plattformsanvändare i organisationen.

Tack vare attributbaserad åtkomstkontroll kan administratören styra användarnas åtkomst till, känsliga personuppgifter (SPD), personligt identifierbar information (PII) och andra anpassade typer av data i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

**Ny eller uppdaterad dokumentation**

| Dokumentation - uppdatering | Beskrivning |
| --- | --- |
| Nya API-slutpunkter dokumenteras för attributbaserad åtkomstkontroll | The [API-referensdokumentation för åtkomstkontroll](https://developer.adobe.com/experience-platform-apis/references/access-control/) innehåller nu attributbaserade API-roller, principer och produktslutpunkter för åtkomstkontroll. De här slutpunkterna kan användas för att hämta relevanta roller, principer och produkter för en användare för angivna resurser i en angiven sandlåda. |

{style="table-layout:auto"}

Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontroll - översikt](../../access-control/abac/overview.md). En omfattande guide om det attributbaserade arbetsflödet för åtkomstkontroll finns i [attribueringsbaserad åtkomstkontroll från början till slut](../../access-control/abac/end-to-end-guide.md).

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya mappningsfunktioner | <ul><li>`object_to_map`: Använd `object_to_map` funktion för att skapa mappningsdatatyper. Den här funktionen stöder flera olika syntaxer. Mer information finns i guiden [funktioner för hierarkier - objekt](../../data-prep/functions.md#objects). </li><li>`to_map`: Använd `to_map` om du vill skapa en karta med angivna fältnamn och värdepar med hjälp av objekt. Mer information finns i guiden [funktioner för hierarkier - kartor](../../data-prep/functions.md#map). </li><li>`array_to_map`: Använd `array_to_map` om du vill skapa en karta med angivna fältnamn och värdepar med hjälp av objektarrayer. Mer information finns i guiden [funktioner för hierarkier - kartor](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Mer information om Data Prep finns i [Översikt över datapreflight](../../data-prep/home.md).

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Visa SQL | Nu kan du visa SQL bakom dina profiler, målgrupper, destinationer och anpassade insikter med växlingsknappen Visa SQL och sedan köra frågan på begäran via Frågeredigeraren. Genom att få tillgång till den SQL som ligger till grund för dina Real-time Customer Data Platform-insikter kan du förstå logiken bakom analysen av din datamodell. Denna transparens gör CDP-data i realtid i Adobe mer tillgängliga, begripliga och slagkraftiga för beslutsfattande.<br>Hämta inspiration från SQL av över 40 befintliga insikter för att skapa nya frågor som bygger på unika insikter från plattformsdata baserat på era affärsbehov. SQL är också tillgängligt för [Profiler](../../dashboards/insights/profiles.md), [Målgrupper](../../dashboards/insights/audiences.md)och [Destinationer](../../dashboards/insights/destinations.md) insikter i dokumentationen för Experience League. Dokumenten belyser de användningsfall som kan besvaras med standardinsikter. Mer information finns i guiden [visa insikter i SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikt över instrumentpaneler](../../dashboards/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer** {#new-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [Allmän anslutning](../../destinations/catalog/advertising/pubmatic.md) | Använd det här målet för att skicka målgruppsdata till [!DNL PubMatic Connect] plattform. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Nytt **antagen roll** autentiseringstyp för Amazon S3-mål | Använd den nya rollautentiseringstypen när du ansluter Experience Platform till dina Amazon S3-bucket om du inte vill dela kontonycklar och hemliga nycklar med Experience Platform. Läs mer om den nya autentiseringsmetoden i [autentiseringssektion](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) av Amazon S3-dokumentationen. |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Identitetstjänst {#identity-service}

Adobe Experience Platform identitetstjänst ger er en heltäckande bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Ny eller uppdaterad dokumentation**

| Dokumentation - uppdatering | Beskrivning |
| --- | --- |
| Omstrukturering av dokumentation | Identitetstjänstens dokumentation har omstrukturerats för att förbättra presentationen och tydligheten i begrepp inom identitetstjänsten:<ul><li>Besök [Översikt över identitetstjänsten](../../identity-service/home.md) om du vill ha en utökad terminologisk guide, ett exempel med exempel på ett typiskt kundresa, en beskrivning av hur identitetstjänsten länkar samman identiteter och en sammanfattning av den roll som identitetstjänsten har i Experience Platform-ekosystemet.</li><li>Läs guiden på [förstå relationen mellan identitetstjänsten och kundprofilen i realtid](../../identity-service/identity-and-profile.md) för en detaljerad sammanfattning av hur de två tjänsterna fungerar tillsammans och skillnaderna mellan deras syften, processer, indata och utdata.</li><li>Se [Logikguide för länkning av identitetstjänst](../../identity-service/features/identity-linking-logic.md) för förklaringar och visualiseringar av hur identitetsdiagrammet beter sig utifrån olika scenarier och tidsstämplar.</li></ul> |

{style="table-layout:auto"}

Läs mer om identitetstjänsten i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Built on Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. [!DNL Real-Time CDP] kombinerar flera datakällor för företag för att skapa kundprofiler i realtid. Segment som byggts utifrån dessa profiler kan sedan skickas till efterföljande destinationer för att tillhandahålla personliga kundupplevelser i alla kanaler och enheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av [Real-Time CDP hemsida](https://experience.adobe.com) | <ul><li>**Profiler, widget**: Du kan nu använda profilwidgeten för att navigera till sidan Profiler - översikt och visa profilmått för din organisation.</li><li>**Profilmätningskort**: Profilmätningskortet på kontrollpanelen för hemsidor visar nu det totala antalet profiler i organisationen, beroende på din respektive sammanfogningspolicy.</li><li>**Widgeten Scheman**: Du kan nu använda schemwidgeten för att navigera till arbetsflödet för att skapa scheman i användargränssnittet.</li></ul> |

{style="table-layout:auto"}

**Ny eller uppdaterad dokumentation**

| Dokumentation - uppdatering | Beskrivning |
| --- | --- |
| Ny startsida för Real-Time CDP-dokumentation | Besök [ny startsida för Real-Time CDP-dokumentation](/help/rtcdp/home.md) om du vill ha snabb information om hur du kommer igång med produkten, skyddsritningar, exempel på hur du använder exempelfiler och mycket annat. |
| Exempel på Real-Time CDP användningsexempel - översikt | Besök [ny sida med översikt över exempel](/help/rtcdp/use-case-guides/overview.md) för en samling exempel på användningsområden som din organisation kan uppnå med Real-Time CDP. |

{style="table-layout:auto"}

Läs mer om Real-Time CDP i [Real-Time CDP - översikt](../../rtcdp/overview.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar av lokalisering av profilvisningsprogrammets standardinstrumentpanelskort | Standardprofilkorten har nu dynamiskt lokaliserade namn. Anpassade profilkort kan även fortsättningsvis ha egna namn som kan redigeras. |

{style="table-layout:auto"}

Läs mer om kundprofilen i realtid i [Profilöversikt](../../profile/home.md)

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL Oracle NetSuite] källor | Använd [!DNL Oracle NetSuite] integreringar i källkatalogen för att hämta data från [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) och [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) konton hos Experience Platform. |
| [!BADGE Beta]{type=Informative}[!DNL Braze Currents] källa | Använd [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) integrering i källkatalogen för att hämta data från [!DNL Braze] konto till Experience Platform. |
| Stöd för autentisering med nyckelpar för [!DNL Snowflake] batchkälla | Nu kan du använda nyckelpars-autentisering när du skapar en ny [!DNL Snowflake] konto för batchdata. Mer information finns i guiden [skapa [!DNL Snowflake] konto med API](../../sources/tutorials/api/create/databases/snowflake.md) eller guiden på [skapa [!DNL Snowflake] konto med användargränssnittet](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).