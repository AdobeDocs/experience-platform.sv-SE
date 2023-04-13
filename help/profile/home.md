---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;enhetlig profil;enhetlig;profil;rtcp;XDM-diagram
title: Kundprofilöversikt i realtid
description: Kundprofilen i realtid sammanfogar data från olika källor och ger åtkomst till dessa data i form av enskilda kundprofiler och relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] översikt

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-Time Customer Profile]kan ni få en helhetsbild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online, offline, CRM och tredje part. [!DNL Profile] gör att ni kan sammanställa era kunddata i en enhetlig vy som ger en användbar, tidsstämplad bild av varje kundinteraktion. Den här översikten hjälper dig att förstå vilken roll du har och hur du använder [!DNL Real-Time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] i Experience Platform

Förhållandet mellan kundprofilen i realtid och andra tjänster inom Experience Platform framgår av följande diagram:

![Förhållandet mellan kundprofilen i realtid och andra tjänster i Adobe Experience Platform. Bilden visar att Profil är en av huvudkomponenterna i Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Förstå profiler

[!DNL Real-Time Customer Profile] sammanfogar data från olika affärssystem och ger sedan tillgång till dessa data i form av kundprofiler med relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler. I följande avsnitt beskrivs några av de grundläggande begrepp som du måste förstå för att effektivt kunna skapa och underhålla profiler inom plattformen.

### Profilens enhetskomposition

En kundprofil i realtid består av en huvudenhet som kallas **primär entitet** och olika stödjande enheter. När det gäller Experience Platform är den primära enheten vanligtvis en **profilentitet**, som består av egenskaper, beteenden och segmentmedlemskap för en enskild person. Andra företag tillåter att segmenteringsmotorn använder data utanför profilens primära enhet och inkluderar följande:

- **Dimensionell enhet**: Den entitet som används för att förenkla datamodelleringsprocessen för information som delas mellan händelser eller profilposter. Detta kallas även sökentitet eller klassificeringsenhet.
- **B2B-enhet**: Enheter som beskriver profilens relation till konton och affärsmöjligheter för företag.

![Ett diagram som förklarar profilentitetens komposition.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Eftersom dimensionella företag och B2B-företag bara finns utanför den primära enheten används dessa endast för gruppsegmentering.

Dimensionerings- och B2B-enheter länkas till den primära enheten via **schemarelationer**. Mer information finns i följande dokumentation:

- [Skapa en 1:1-schemarelation för sökentiteter](../xdm/tutorials/relationship-ui.md)
- [Skapa en många-till-ett-schemarelation för B2B-entiteter](../xdm/tutorials/relationship-b2b.md)

### Profildatalager

Fast [!DNL Real-Time Customer Profile] bearbetar inkapslade data och använder Adobe Experience Platform [!DNL Identity Service] för att sammanfoga relaterade data via identitetsmappning, lagrar den egna data i [!DNL Profile] datalager. The [!DNL Profile] arkivet är skilt från katalogdata i datasjön och [!DNL Identity Service] data i identitetsdiagrammet.

Profilarkivet använder en Microsoft Azure Cosmos DB-infrastruktur och Platform Data Lake använder Microsoft Azure Data Lake-lagring.

### Profilskyddsutkast

Experience Platform har ett antal skyddsräcken som hjälper dig att undvika att skapa [XDM-scheman (Experience Data Model)](../xdm/home.md) som kundprofilen i realtid inte stöder. Detta inkluderar mjuka gränser som resulterar i försämrade prestanda, samt hårda gränser som resulterar i fel och systemfel. Mer information, inklusive en lista över riktlinjer och exempel på användningsområden, finns i [Profilskyddsutkast](guardrails.md) dokumentation.

### Kontrollpanel för profil {#profile-dashboard}

Användargränssnittet i Experience Platform innehåller en kontrollpanel där du kan visa viktig information om kundprofildata i realtid, som du har tagit med en daglig ögonblicksbild. Så här får du lära dig att komma åt och arbeta med [!DNL Profile] kontrollpanelen i användargränssnittet och detaljerad information om mätvärdena som visas på kontrollpanelen finns i [Användargränssnittshandbok för profilinstrumentpanel](ui/profile-dashboard.md).

### Profilfragment jämfört med sammanslagna profiler {#profile-fragments-vs-merged-profiles}

Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de för att skapa en enda profil för kunden.

Profilfragment representerar med andra ord en unik primär identitet och motsvarande [record](#record-data) eller [event](#time-series-events) data för detta ID inom en viss datauppsättning.

När data från flera datauppsättningar står i konflikt (t.ex. ett fragment listar kunden som&quot;enkel&quot; medan det andra listar kunden som&quot;gift&quot;) [sammanfogningsprincip](#merge-policies) avgör vilken information som ska prioriteras och inkluderas i profilen för den enskilda personen. Det totala antalet profilfragment inom Platform är därför sannolikt alltid högre än det totala antalet sammanfogade profiler, eftersom varje profil vanligtvis består av flera fragment från flera datauppsättningar.

### Registrera data {#record-data}

En profil är en representation av ett ämne, en organisation eller en individ, som består av många attribut (kallas även postdata). Profilen för en produkt kan t.ex. innehålla en SKU och en beskrivning, medan profilen för en person innehåller information som förnamn, efternamn och e-postadress. Använda [!DNL Experience Platform]kan ni anpassa profiler så att de använder specifika data som är relevanta för ert företag. Standarden [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], är den klass som helst för att skapa ett schema när kundpostdata beskrivs, och tillhandahåller data som är integrerade i många interaktioner mellan plattformstjänster. Mer information om att arbeta med scheman finns i [!DNL Experience Platform], kan du börja med att läsa [XDM - systemöversikt](../xdm/home.md).

### Tidsseriehändelser {#time-series-events}

Med tidsseriedata får du en ögonblicksbild av systemet när en åtgärd vidtas antingen direkt eller indirekt av ett ämne, samt data som detaljerar själva händelsen. Tidsseriedata representeras av standardschemaklassen XDM ExperienceEvent och kan beskriva händelser som objekt som läggs till i en kundvagn, länkar som klickas och videofilmer som visas. Tidsseriedata kan användas för att basera segmenteringsregler på, och händelser kan nås individuellt i en profils kontext.

### Identiteter

Alla företag vill kommunicera med sina kunder på ett sätt som känns personligt. En av utmaningarna med att leverera relevanta digitala upplevelser till kunder är dock att förstå hur de ska koppla samman sina fristående data, som ofta sprids över olika digitala kanaler, som surfplattor, mobiltelefoner och bärbara datorer. [!DNL Identity Service] gör att ni kan sammanställa hela bilden av kunden genom att länka identiteter från flera kanaler och skapa ett identitetsdiagram för varje kund. Besök [Översikt över identitetstjänsten](../identity-service/home.md) för mer information.

### Sammanfoga profiler

När du sammanför datafragment från flera olika källor och kombinerar dem för att få en fullständig bild av varje enskild kund, är sammanfogningsprinciper reglerna som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska användas för att skapa kundprofilen.

När det finns data som är i konflikt med varandra från flera datauppsättningar avgör kopplingsregeln hur data ska behandlas och vilket värde som ska användas. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen.

Om du vill veta mer om policyer för sammanslagning och deras roll i Experience Platform börjar du med att läsa [sammanfogningsprinciper - översikt](merge-policies/overview.md).

### Unionens system {#profile-fragments-and-union-schemas}

En av de viktigaste funktionerna i [!DNL Real-Time Customer Profile] är möjligheten att sammanställa flerkanalsdata. När [!DNL Real-Time Customer Profile] används för att få åtkomst till en entitet, kan den ge dig en sammanslagen vy över alla profilfragment för den entiteten i alla datauppsättningar, som kallas&quot;unionsvy&quot; och görs möjlig genom det som kallas för ett unionsschema.

Läs mer om fackliga scheman, inklusive hur du får tillgång till fackliga scheman i användargränssnittet på [gränssnittshandbok för union av schema](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Profiler och segment

Adobe Experience Platform [!DNL Segmentation Service] skapar de målgrupper som behövs för att ge era enskilda kunder bättre upplevelser. När ett målgruppssegment skapas läggs ID:t för det segmentet till i listan över segmentmedlemskap för alla kvalificerande profiler. Segmentregler skapas och tillämpas på [!DNL Real-Time Customer Profile] data med RESTful API:er och användargränssnittet i Segment Builder. Om du vill veta mer om segmentering börjar du med att läsa [Översikt över segmenteringstjänsten](../segmentation/home.md).

### Direktuppspelningsuppläsning och direktuppspelningssegmentering

Realtidsinmatning är möjlig genom en process som kallas direktuppspelning. När data från profil- och tidsserier hämtas, [!DNL Real-Time Customer Profile] bestämmer sig automatiskt för att inkludera eller exkludera data från segment genom en pågående process som kallas direktuppspelningssegmentering, innan de slås samman med befintliga data och unionens vy uppdateras. Resultatet blir att ni omedelbart kan utföra beräkningar och fatta beslut för att leverera förbättrade, individanpassade upplevelser till kunderna när de interagerar med ert varumärke. När data importeras valideras de också för att säkerställa att de importeras på rätt sätt och att de överensstämmer med det schema som datauppsättningen baseras på. Mer information om vilken validering som görs under importen får du om du börjar med att läsa [kvalitetsöversikt över dataöverföring](../ingestion/quality/overview.md).

## Kantprojektioner

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe Experience Platform ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Till exempel använder Adobe-program som Adobe Target och Adobe Campaign kanter för att leverera personaliserade kundupplevelser i realtid. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten. Lär dig mer och börja arbeta med projektioner med [!DNL Real-Time Customer Profile] API, se [slutpunktsguide för kantprojektion](api/edge-projections.md).

## Samla in data i [!DNL Profile]

[!DNL Platform] kan konfigureras för att skicka post- och tidsseriedata till [!DNL Profile], med stöd för direktuppspelning i realtid och batchinmatning. Mer information finns i självstudiekursen med information om hur du [lägga till data i kundprofilen i realtid](tutorials/add-profile-data.md).

>[!NOTE]
>
>Uppgifter som samlats in via Adobe-lösningar, inklusive [!DNL Analytics Cloud], [!DNL Marketing Cloud]och [!DNL Advertising Cloud], flödar till [!DNL Experience Platform] och hämtas till [!DNL Profile].

### Profilätvärden

Med Insikter om observerbarhet kan ni visa nyckeltal i Adobe Experience Platform. Förutom [!DNL Experience Platform] användningsstatistik och resultatindikatorer för olika [!DNL Platform] finns det specifika profilrelaterade mätvärden som gör att du kan få insikt i hur många begäranden som kommer in, hur många som har passerat, hur stora poster som har importerats, och mycket mer. Om du vill veta mer börjar du med att läsa [API-översikt över observationsinsikter](../observability/api/overview.md)och en fullständig lista över kundprofilsmått i realtid finns i dokumentationen om [tillgängliga mått](../observability/api/metrics.md#available-metrics).

## Uppdatera profilarkivdata

Ibland kan det vara nödvändigt att uppdatera data i din organisations Profile Store. Du kan till exempel behöva korrigera poster eller ändra ett attributvärde. Detta kan göras via batchinmatning och kräver en profilaktiverad datauppsättning som konfigurerats med en upsert-tagg. Mer information om hur du konfigurerar en datauppsättning för attributuppdateringar finns i självstudiekursen för [aktivera en datauppsättning för profil och upsert](../catalog/datasets/enable-upsert.md).

## Datastyrning och [!DNL Privacy]

Datastyrning är en serie strategier och tekniker som används för att hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning.

När det gäller åtkomst av data spelar datastyrning en viktig roll inom [!DNL Experience Platform] på olika nivåer:

- Dataanvändningsetikett
- Dataåtkomstprinciper
- Åtkomstkontroll över data för marknadsföringsåtgärder

Datastyrning hanteras vid flera tillfällen. Det kan handla om att bestämma vilka data som ska importeras till [!DNL Platform] och vilka data som är tillgängliga efter intag för en viss marknadsföringsåtgärd. Mer information finns i [datastyrningsöversikt](../data-governance/home.md).

### Hantera avanmälan och förfrågningar om datasekretess

[!DNL Experience Platform] gör det möjligt för dina kunder att skicka avanmälningsförfrågningar relaterade till användning och lagring av sina data inom [!DNL Real-Time Customer Profile]. Mer information om hur avanmälningsbegäranden hanteras finns i dokumentationen om [uppfylla avanmälningsbegäranden](../segmentation/consents.md).

## Nästa steg och ytterligare resurser

Om du vill veta mer om hur du arbetar med kundprofildata i realtid med Experience Platform-gränssnittet eller profilens API börjar du med att läsa [Användargränssnittshandbok för profil](ui/user-guide.md) eller [Utvecklarhandbok för API](api/overview.md), respektive.
