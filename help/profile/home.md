---
title: Kundprofilöversikt i realtid
description: Kundprofilen i realtid sammanfogar data från olika källor och ger åtkomst till dessa data i form av enskilda kundprofiler och relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 7d515401eb49ffd2ad5cf0bd074896b274c4fb05
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] översikt

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med [!DNL Real-Time Customer Profile] kan du se en helhetsbild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online, offline, CRM och tredje part. Med [!DNL Profile] kan du konsolidera dina kunddata i en enhetlig vy som ger ett åtgärdbart, tidsstämplat konto för varje kundinteraktion. Den här översikten hjälper dig att förstå rollen och användningen av [!DNL Real-Time Customer Profile] i [!DNL Experience Platform].

## [!DNL Profile] i Experience Platform

Förhållandet mellan kundprofilen i realtid och andra tjänster inom Experience Platform framgår av följande diagram:

![Relationen mellan kundprofilen i realtid och andra tjänster i Adobe Experience Platform. Bilden visar att Profilen är en av huvudkomponenterna i Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Förstå profiler

[!DNL Real-Time Customer Profile] sammanfogar data från olika affärssystem och ger sedan åtkomst till dessa data i form av kundprofiler med relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler. I följande avsnitt beskrivs några av de grundläggande begrepp som du måste förstå för att effektivt kunna skapa och underhålla profiler inom plattformen.

### Profilens enhetskomposition

En kundprofil i realtid består av en huvudentitet, som kallas **primär entitet**, och olika stödentiteter. I Experience Platform är den primära entiteten vanligtvis en **profilentitet** som består av egenskaper, beteenden och målgruppsmedlemskap för en enskild person. Andra företag tillåter att segmenteringsmotorn använder data utanför profilens primära enhet och inkluderar följande:

- **Dimensionell entitet**: Den entitet som används för att förenkla datamodelleringsprocessen för information som delas mellan händelser eller profilposter. Detta kallas även sökentitet eller klassificeringsenhet.
- **B2B-entitet**: Enheter som beskriver profilens relation till konton och affärsmöjligheter för företag.

![Ett diagram som förklarar profilentitetens komposition.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Eftersom dimensionella företag och B2B-företag bara finns utanför den primära enheten används dessa endast för gruppsegmentering.

Dimensionella enheter och B2B-enheter länkas till den primära entiteten via **schemarelationer**. Mer information finns i följande dokumentation:

- [Skapa en 1:1-schemarelation för sökentiteter](../xdm/tutorials/relationship-ui.md)
- [Skapa en många-till-ett-schemarelation för B2B-entiteter](../xdm/tutorials/relationship-b2b.md)

### Profildatalager

Även om [!DNL Real-Time Customer Profile] bearbetar inkapslade data och använder Adobe Experience Platform [!DNL Identity Service] för att sammanfoga relaterade data via identitetsmappning, behåller den egna data i datalagret [!DNL Profile]. [!DNL Profile]-arkivet är skilt från katalogdata i datasjön och [!DNL Identity Service] data i identitetsdiagrammet.

Profilarkivet använder en Microsoft Azure Cosmos DB-infrastruktur och Platform Data Lake använder Microsoft Azure Data Lake-lagring.

### Profilskyddsutkast

Experience Platform tillhandahåller en serie skyddsutkast som hjälper dig att undvika att skapa [XDM-scheman (Experience Data Model)](../xdm/home.md) som kundprofilen i realtid inte stöder. Detta inkluderar mjuka gränser som resulterar i försämrade prestanda samt hårda gränser som resulterar i fel och systemfel. Mer information, inklusive en lista över riktlinjer och exempel på användningsfall, finns i dokumentationen för [profilskyddsförslag](guardrails.md).

### Kontrollpanel för profil {#profile-dashboard}

Användargränssnittet i Experience Platform innehåller en kontrollpanel där du kan visa viktig information om kundprofildata i realtid, som du har tagit med en daglig ögonblicksbild. Om du vill lära dig hur du får åtkomst till och arbetar med kontrollpanelen [!DNL Profile] i användargränssnittet, och detaljerad information om mätvärden som visas på kontrollpanelen, kan du läsa [Användargränssnittsguiden för profilkontrollpanelen](ui/profile-dashboard.md).

### Profilfragment jämfört med sammanslagna profiler {#profile-fragments-vs-merged-profiles}

Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de för att skapa en enda profil för kunden.

Profilfragment representerar med andra ord en unik primär identitet och motsvarande [post](#record-data) - eller [händelse](#time-series-events)-data för det ID:t inom en given datauppsättning.

När data från flera datauppsättningar står i konflikt (t.ex. ett fragment listar kunden som&quot;enskild&quot; medan den andra listar kunden som&quot;gift&quot;) avgör [sammanfogningsprincipen](#merge-policies) vilken information som ska prioriteras och inkluderas i profilen för den enskilda personen. Det totala antalet profilfragment inom Platform är därför sannolikt alltid högre än det totala antalet sammanfogade profiler, eftersom varje profil vanligtvis består av flera fragment från flera datauppsättningar.

### Registrera data {#record-data}

En profil är en representation av ett ämne, en organisation eller en individ, som består av många attribut (kallas även postdata). Profilen för en produkt kan t.ex. innehålla en SKU och en beskrivning, medan profilen för en person innehåller information som förnamn, efternamn och e-postadress. Med [!DNL Experience Platform] kan du anpassa profiler så att de använder specifika data som är relevanta för ditt företag. Standardklassen [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], är den klass som helst för att skapa ett schema när kundpostdata beskrivs, och tillhandahåller dataintegriteten för många interaktioner mellan plattformstjänster. Mer information om hur du arbetar med scheman i [!DNL Experience Platform] får du genom att läsa [XDM-systemöversikten](../xdm/home.md).

### Tidsseriehändelser {#time-series-events}

Med tidsseriedata får du en ögonblicksbild av systemet när en åtgärd vidtas antingen direkt eller indirekt av ett ämne, samt data som detaljerar själva händelsen. Tidsseriedata representeras av standardschemaklassen XDM ExperienceEvent och kan beskriva händelser som objekt som läggs till i en kundvagn, länkar som klickas och videofilmer som visas. Tidsseriedata kan användas för att basera segmenteringsregler på, och händelser kan nås individuellt i en profils kontext.

### Identiteter

Alla företag vill kommunicera med sina kunder på ett sätt som känns personligt. En av utmaningarna med att leverera relevanta digitala upplevelser till kunder är dock att förstå hur de ska koppla samman sina fristående data, som ofta sprids över olika digitala kanaler, som surfplattor, mobiltelefoner och bärbara datorer. Med [!DNL Identity Service] kan du sammanfoga hela kundbilden genom att länka identiteter från flera kanaler och skapa ett identitetsdiagram för varje kund. Mer information finns i [Översikt över identitetstjänsten](../identity-service/home.md).

### Sammanfoga profiler

När du sammanfogar datafragment från flera källor och kombinerar dem för att få en fullständig bild av varje enskild kund, är sammanfogningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska användas för att skapa kundprofilen.

När det finns data som är i konflikt med varandra från flera datauppsättningar avgör kopplingsregeln hur data ska behandlas och vilket värde som ska användas. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen.

Om du vill veta mer om sammanfogningsprinciper och deras roll i Experience Platform börjar du med att läsa översikten [för sammanfogningsprinciper](merge-policies/overview.md).

### Unionens system {#profile-fragments-and-union-schemas}

En av de viktigaste funktionerna i [!DNL Real-Time Customer Profile] är möjligheten att sammanställa flerkanalsdata. När [!DNL Real-Time Customer Profile] används för att få åtkomst till en entitet kan den förse dig med en sammanfogad vy över alla profilfragment för den entiteten i alla datauppsättningar, som kallas för&quot;unionsvyn&quot; och som är möjlig genom ett så kallat unionsschema.

Om du vill veta mer om unionsscheman, inklusive hur du kommer åt unionsscheman i användargränssnittet, kan du gå till [gränssnittsguiden för unionsscheman](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Profiler och målgrupper

Adobe Experience Platform [!DNL Segmentation Service] producerar de målgrupper som behövs för att ge era enskilda kunder bättre upplevelser. När en målgrupp skapas läggs målgruppens ID till i listan över målgruppsmedlemskap för alla kvalificerande profiler. Segmentregler skapas och tillämpas på [!DNL Real-Time Customer Profile]-data med RESTful API:er och användargränssnittet i Segment Builder. Om du vill veta mer om segmentering börjar du med att läsa översikten för [segmenteringstjänsten](../segmentation/home.md).

### Direktuppspelningsuppläsning och direktuppspelningssegmentering

Realtidsinmatning är möjlig genom en process som kallas direktuppspelning. När data från profil- och tidsserier importeras bestämmer [!DNL Real-Time Customer Profile] sig automatiskt för att inkludera eller exkludera data från målgrupper via en pågående process som kallas direktuppspelningssegmentering, innan den sammanfogas med befintliga data och unionsvyn uppdateras. Resultatet blir att ni omedelbart kan utföra beräkningar och fatta beslut för att leverera förbättrade, individanpassade upplevelser till kunderna när de interagerar med ert varumärke. När data importeras valideras de också för att säkerställa att de importeras korrekt och att de överensstämmer med det schema som datauppsättningen baseras på. Om du vill ha mer information om vilken validering som görs under importen börjar du med att läsa översikten [för dataöverföringskvalitet](../ingestion/quality/overview.md).

## Hämtar data till [!DNL Profile]

[!DNL Platform] kan konfigureras för att skicka post- och tidsseriedata till [!DNL Profile], med stöd för direktuppspelning i realtid och batchinmatning. Mer information finns i självstudiekursen om hur du [lägger till data i kundprofilen i realtid](tutorials/add-profile-data.md).

>[!NOTE]
>
>Data som samlas in via Adobe-lösningar, inklusive [!DNL Analytics Cloud], [!DNL Marketing Cloud] och [!DNL Advertising Cloud], flödar till [!DNL Experience Platform] och hämtas till [!DNL Profile].

### Profilätvärden

Med Insikter om observerbarhet kan ni visa nyckeltal i Adobe Experience Platform. Förutom [!DNL Experience Platform]-användningsstatistik och prestandaindikatorer för olika [!DNL Platform]-funktioner finns det specifika profilrelaterade mått som gör att du kan få insikt i inkommande begärandefrekvenser, lyckade intagsfrekvenser, inkapslade poststorlekar och mycket annat. Om du vill veta mer kan du börja med att läsa översikten för API:t [Observability Insights](../observability/api/overview.md) och en fullständig lista över kundprofilsmått i realtid finns i dokumentationen om [tillgängliga mätvärden](../observability/api/metrics.md#available-metrics).

## Uppdatera data i profilarkivet

Ibland kan det vara nödvändigt att uppdatera data i din organisations profilarkiv. Du kan till exempel behöva korrigera poster eller ändra ett attributvärde. Detta kan göras via batchinmatning och kräver en profilaktiverad datauppsättning som konfigurerats med en upsert-tagg. Mer information om hur du konfigurerar en datauppsättning för attributuppdateringar finns i självstudiekursen för [att aktivera en datauppsättning för profil och uppdatering](../catalog/datasets/enable-upsert.md).

## Datastyrning och [!DNL Privacy]

Datastyrning är en serie strategier och tekniker som används för att hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning.

När det gäller åtkomst av data spelar datastyrning en nyckelroll inom [!DNL Experience Platform] på olika nivåer:

- Dataanvändningsetikett
- Dataåtkomstprinciper
- Åtkomstkontroll över data för marknadsföringsåtgärder

Datastyrning hanteras vid flera tillfällen. Det kan vara att bestämma vilka data som ska importeras till [!DNL Platform] och vilka data som är tillgängliga efter att de har importerats för en viss marknadsföringsåtgärd. Om du vill ha mer information börjar du med att läsa översikten över [datastyrning](../data-governance/home.md).

### Hantera avanmälan och förfrågningar om datasekretess

[!DNL Experience Platform] gör det möjligt för dina kunder att skicka avanmälningsbegäranden som rör användning och lagring av deras data i [!DNL Real-Time Customer Profile]. Mer information om hur avanmälningsbegäranden hanteras finns i dokumentationen om [hur avanmälningsbegäranden ](../segmentation/consents.md) respekteras.

## Nästa steg och ytterligare resurser

Om du vill veta mer om hur du arbetar med kundprofildata i realtid med hjälp av Experience Platform-gränssnittet eller profil-API:t börjar du med att läsa [gränssnittshandboken för profilen](ui/user-guide.md) respektive [API-utvecklarhandboken](api/overview.md).
