---
title: Versionsinformation om Adobe Experience Platform januari 2024
description: Versionsinformationen för Adobe Experience Platform i januari 2024.
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: ht
source-wordcount: '1650'
ht-degree: 100%

---

# Versionsinformation om Adobe Experience Platform

**Releasedatum: 30 januari 2024**

Nya funktioner i Adobe Experience Platform:

- [Use Case Playbooks](#use-case-playbooks)

Uppdateringar av befintliga funktioner i Experience Platform:

- [Attributbaserad åtkomstkontroll](#abac)
- [Dataförberedelse](#data-prep)
- [Kontrollpaneler](#dashboards)
- [Mål ](#destinations)
- [Identitetstjänst](#identity-service)
- [Plattform för kunddata i realtid](#rtcdp)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Use Case Playbooks {#use-case-playbooks}

Funktionen [!UICONTROL Use Case Playbooks] är nu allmänt tillgänglig för alla Real-Time CDP- och Adobe Journey Optimizer-kunder. [!UICONTROL Use Case Playbooks] är utformade för att hjälpa användare att övervinna utmaningar när de börjar med Real-time Customer Data Platform eller Adobe Journey Optimizer. När du är osäker på var du ska börja eller hur du ska skapa rätt material för dina behov kan du få inspiration med Use Case Playbooks och skapa olika resurser så att du kan testa och importera till produktionsmiljöer när du är klar.

Läs följande dokumentationssidor för att komma igång med [!UICONTROL Use Case Playbooks]:

- Läs [översiktssidan](/help/use-case-playbooks/playbooks/overview.md) för att förstå syfte, få tillgänglighetsinformation och för att få en heltäckande demonstration av hur spelböcker fungerar, från identifiering till skapande av instanser, till import av genererade resurser till andra sandlådemiljöer.
- Hämta en lista med alla [tillgängliga spelböcker](/help/use-case-playbooks/playbooks/playbooks-list.md), grupperade efter produkt (Real-Time CDP eller Journey Optimizer)
- Hämta information om alla [nödvändiga behörigheter](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) för att använda spelböcker och de resurser som genereras av spelböckerna.
- Förstå funktionen [för dataidentifiering](/help/use-case-playbooks/playbooks/data-awareness.md) som gör att du kan kopiera genererade resurser till andra sandlådemiljöer
- Få [felsökningstips](/help/use-case-playbooks/playbooks/troubleshooting.md) om du stöter på fel eller problem när du använder Use Case Playbooks.

## Attributbaserad åtkomstkontroll {#abac}

Attributbaserad åtkomstkontroll är en funktion hos Adobe Experience Platform som ger sekretessmedvetna varumärken större flexibilitet att hantera användaråtkomst. Enskilda objekt som schemafält och segment kan tilldelas användarroller. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika plattformsanvändare i organisationen.

Tack vare attributbaserad åtkomstkontroll kan administratören styra användarnas åtkomst till känsliga personuppgifter (SPD), personligt identifierbar information (PII) och andra anpassade typer av data i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

**Ny eller uppdaterad dokumentation**

| Uppdatering av dokumentation | Beskrivning |
| --- | --- |
| Nya API-slutpunkter dokumenteras för attributbaserad åtkomstkontroll | [Referenshandboken för API för åtkomstkontroll](https://developer.adobe.com/experience-platform-apis/references/access-control/) innehåller nu attributbaserade API-roller, principer och produktslutpunkter. De här slutpunkterna kan användas för att hämta relevanta roller, principer och produkter för en användare för angivna resurser i en angiven sandlåda. |

{style="table-layout:auto"}

Mer information om attributbaserad åtkomstkontroll finns i [översikt över attributbaserad åtkomstkontroll](../../access-control/abac/overview.md). En utförlig guide om det attributbaserade arbetsflödet för åtkomstkontroll finns i [heltäckande attributbaserad åtkomstkontroll](../../access-control/abac/end-to-end-guide.md).

## Dataförberedelse {#data-prep}

Med dataförberedelse kan utvecklare mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya mappningsfunktioner | <ul><li>`object_to_map`: Använd funktionen `object_to_map` för att skapa datatyper för mappning. Den här funktionen stöder flera olika syntaxer. Mer information finns i guiden för [funktioner för hierarkier – objekt](../../data-prep/functions.md#objects). </li><li>`to_map`: Använd funktionen `to_map` för att skapa en mappning med angivna fältnamn och värdepar med hjälp av objekt. Mer information finns i guiden för [funktioner för hierarkier – kartor](../../data-prep/functions.md#map). </li><li>`array_to_map`: Använd funktionen `array_to_map` för att skapa en mappning med angivna fältnamn och värdepar med hjälp av objektmatriser. Mer information finns i guiden för [funktioner för hierarkier – kartor](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Mer information om dataförberedelse finns i [översikt över dataförberedelse](../../data-prep/home.md).

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Visa SQL | Du kan nu visa SQL bakom dina profiler, målgrupper, mål och anpassade insikter med hjälp av växlingsknappen Visa SQL och sedan köra frågan på begäran via frågeredigeraren. Genom att komma åt den SQL som driver dina insikter från plattformen för kunddata i realtid kan du förstå logiken bakom analysen av din datamodell. Denna transparens gör Adobes realtids-CDP-data mer tillgängliga, begripliga och effektiva för beslutsfattande.<br>Låt dig inspireras av SQL från över 40 befintliga insikter för att skapa nya frågor som ger unika insikter från plattformsdata baserat på dina affärsbehov. SQL finns också tillgängligt för dina insikter för [profiler](../../dashboards/insights/profiles.md), [målgrupper](../../dashboards/insights/audiences.md) och [mål](../../dashboards/insights/destinations.md) i dokumentationen för Experience League. Dessa dokument belyser de affärsanvändningsfall som kan besvaras med standardinsikterna. Mer information finns i guiden för [visning av SQL-insikter](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Läs [översikt över kontrollpaneler](../../dashboards/home.md) för mer information om kontrollpaneler, bland annat hur du beviljar åtkomstbehörigheter och skapar anpassade widgetar.

## Mål  {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya mål** {#new-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [Pubmatic-anslutning](../../destinations/catalog/advertising/pubmatic.md) | Använd det här målet för att skicka målgruppsdata till [!DNL PubMatic Connect]-plattformen. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Ny autentiseringstyp **antagen roll** för Amazon S3-mål | Använd den nya autentiseringstypen för antagen roll när du ansluter Experience Platform till dina Amazon S3-buckets om du inte vill dela kontonycklar och hemliga nycklar med Experience Platform. Läs mer om den nya autentiseringsmetoden i avsnittet [autentisering](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) i dokumentationen för Amazon S3. |

{style="table-layout:auto"}

För mer allmän information om mål, se [översikt över mål](../../destinations/home.md).

## Identitetstjänst {#identity-service}

Adobe Experience Platforms identitetstjänst ger dig en heltäckande bild av dina kunder och deras beteende genom att koppla samman identiteter mellan enheter och system så att du kan leverera effektiva, personliga digitala upplevelser i realtid.

**Ny eller uppdaterad dokumentation**

| Uppdatering av dokumentation | Beskrivning |
| --- | --- |
| Omstrukturering av dokumentation | Identitetstjänstens dokumentation har omstrukturerats för att förbättra presentationen och tydligheten av begreppen inom identitetstjänsten:<ul><li>Besök [översiktssidan för identitetstjänsten](../../identity-service/home.md) för en utökad terminologiguide, ett exempel på ett användningsfall som beskriver en typisk kundresa, en uppdelning av hur identitetstjänsten kopplar samman identiteter och en sammanfattning av den roll som identitetstjänsten har inom Experience Platforms ekosystem.</li><li>Läs guiden kring att [förstå förhållandet mellan identitetstjänsten och realtids-kundprofilen](../../identity-service/identity-and-profile.md) för en detaljerad sammanfattning av hur de två tjänsterna fungerar tillsammans och skillnaderna mellan deras syften, processer, inputs och outputs.</li><li>Se guiden [länkningslogik för identitetstjänsten](../../identity-service/features/identity-linking-logic.md) för förklaringar och visualiseringar av hur identitetsdiagrammet beter sig i olika scenarier och med olika tidsstämplar.</li></ul> |

{style="table-layout:auto"}

Om du vill veta mer om identitetstjänsten kan du läsa [översikt över identitetstjänsten](../../identity-service/home.md).

## Plattform för kunddata i realtid {#rtcdp}

Plattformen för kunddata i realtid ([!DNL Real-Time CDP]) bygger på Experience Platform och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligenta beslut under hela kundresan. [!DNL Real-Time CDP] kombinerar flera datakällor från företag för att skapa kundprofiler i realtid. Segment som byggs upp utifrån dessa profiler kan sedan skickas till mål i senare led för att ge personliga kundupplevelser i alla kanaler och på alla enheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av [startsidan för Real-Time CDP](https://experience.adobe.com) | <ul><li>**Profilwidget**: Du kan nu använda widgeten Profiler för att navigera till översiktssidan Profiler och visa profilmätvärden för din organisation.</li><li>**Profilmätvärdeskort**: Profilmätvärdeskortet i kontrollpanelen på startsidan visar nu det totala antalet profiler i din organisation, beroende på din respektive sammanfogningspolicy.</li><li>**Schema-widget**: Du kan nu använda schema-widgeten för att navigera till arbetsflödet för schemaskapande i användargränssnittet.</li></ul> |

{style="table-layout:auto"}

**Ny eller uppdaterad dokumentation**

| Uppdatering av dokumentation | Beskrivning |
| --- | --- |
| Ny startsida för dokumentation av Real-Time CDP | Besök den [nya dokumentationsstartsidan för Real-Time CDP](/help/rtcdp/home.md) för att få snabb information om hur du kommer igång med produkten, trösklar, exempel på användningsfall och mycket mer. |
| Översikt över exempel på användningsfall för Real-Time CDP | Besök [sidan med nya exempel på användningsfall](/help/rtcdp/use-case-guides/overview.md) för en samling exempel på användningsfall som din organisation kan uppnå med Real-Time CDP. |

{style="table-layout:auto"}

Läs mer om Real-Time CDP i [översikt över Real-Time CDP](../../rtcdp/overview.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid får du en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online, offline, CRM och data från tredje part. Med profilen kan du konsolidera kunddata till en enhetlig vy som ger en handlingsbar, tidsstämplad redogörelse för varje kundinteraktion.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar av lokaliseringen av profilvisarens standardkort på kontrollpanelen | Standardprofilkorten kommer nu att ha dynamiskt lokaliserade namn. Anpassade profilkort kan även fortsätta ha anpassade namn som kan redigeras. |

{style="table-layout:auto"}

Mer information om kundprofil i realtid finns i [profilöversikt](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Externt genererad målgruppsuppladdning | Det maximala antalet kolumner har ökats till **25**. |
| Segment Builder-uppskattningar | Uppskattningar och kvalificerade profiler visas nu i avsnittet för målgruppsegenskaper. Mer information om den här ändringen finns i [gränssnittsguiden för Segment Builder](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service] finns i [segmenteringsöversikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite]-källor | Använd [!DNL Oracle NetSuite]-integreringarna i källkatalogen för att hämta data från dina [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)- och [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md)-konton till Experience Platform. |
| [!BADGE Beta]{type=Informative} [!DNL Braze Currents]-källa | Använd integreringen [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) i källkatalogen för att hämta data från ditt [!DNL Braze]-konto till Experience Platform. |
| Stöd för autentisering med nyckelpar för gruppkällan [!DNL Snowflake] | Du kan nu använda nyckelpars-autentisering när du skapar ett nytt [!DNL Snowflake]-konto för gruppdata. Mer information finns i guiden om att [skapa ett [!DNL Snowflake] konto med hjälp av API](../../sources/tutorials/api/create/databases/snowflake.md) eller guiden om att [skapa ett [!DNL Snowflake] konto med gränssnittet](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Mer information om källor finns i [översikten över källor](../../sources/home.md).
