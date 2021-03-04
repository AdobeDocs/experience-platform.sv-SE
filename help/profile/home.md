---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;enhetlig profil;enhetlig;profil;rtcp;XDM-diagram
title: Kundprofilöversikt i realtid
topic: guide
description: Kundprofil i realtid är ett generiskt uppslagsarkiv som sammanfogar data från olika företagsdatatillgångar och sedan ger tillgång till dessa data i form av enskilda kundprofiler och relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] översikt

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-time Customer Profile] kan ni se en helhetsbild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online, offline, CRM och tredje part. [!DNL Profile] gör att ni kan sammanställa era kunddata i en enhetlig vy som ger en användbar, tidsstämplad bild av varje kundinteraktion. Den här översikten hjälper dig att förstå rollen och användningen av [!DNL Real-time Customer Profile] i [!DNL Experience Platform].

## [!DNL Profile] i Experience Platform

Förhållandet mellan kundprofil i realtid och andra tjänster inom Experience Platform framgår av följande diagram:

![](images/profile-overview/profile-in-platform.png)

## Förstå profiler

[!DNL Real-time Customer Profile] sammanfogar data från olika affärssystem och ger sedan tillgång till dessa data i form av kundprofiler med relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler. I följande avsnitt beskrivs några av de grundläggande begrepp som du måste förstå för att effektivt kunna skapa och underhålla profiler inom plattformen.

### Profildatalager

Även om [!DNL Real-time Customer Profile] bearbetar inkapslade data och använder Adobe Experience Platform [!DNL Identity Service] för att sammanfoga relaterade data via identitetsmappning, behåller den egna data i [!DNL Profile]-datalagret. Lagret [!DNL Profile] är skilt från katalogdata i datasjön och [!DNL Identity Service] data i identitetsdiagrammet.

Profilarkivet använder en Microsoft Azure Cosmos DB-infrastruktur och Platform Data Lake använder Microsoft Azure Data Lake-lagring.

### Profilskyddsutkast

Experience Platform tillhandahåller en rad skyddsutkast som hjälper dig att undvika att skapa [XDM-scheman (Experience Data Model)](../xdm/home.md) som kundprofilen i realtid inte stöder. Detta inkluderar mjuka gränser som resulterar i försämrade prestanda, samt hårda gränser som resulterar i fel och systemfel. Mer information, inklusive en lista över riktlinjer och exempel på användningsfall, finns i [dokumentationen för profilskyddsprofiler](guardrails.md).

### (Beta) Kontrollpanel för profil {#profile-dashboard}

>[!IMPORTANT]
>
>Instrumentpanelsfunktionen är för närvarande i betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Användargränssnittet i Experience Platform innehåller en kontrollpanel där du kan visa viktig information om kundprofildata i realtid, som du har tagit med en daglig ögonblicksbild. Om du vill lära dig hur du får åtkomst till och arbetar med kontrollpanelen [!DNL Profile] i användargränssnittet, och detaljerad information om mätvärden som visas på kontrollpanelen, läser du i handboken [Profilkontrollpanelen](ui/profile-dashboard.md).

### Profilfragment jämfört med sammanslagna profiler {#profile-fragments-vs-merged-profiles}

Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de för att skapa en enda profil för kunden.

När data från flera källor står i konflikt (t.ex. ett fragment listar kunden som&quot;enkel&quot; medan det andra listar kunden som&quot;gift&quot;) avgör [sammanfogningsprincipen](#merge-policies) vilken information som ska prioriteras och inkluderas i profilen för den enskilda personen. Det totala antalet profilfragment inom Platform är därför sannolikt alltid högre än det totala antalet sammanfogade profiler, eftersom varje profil består av flera fragment.

### Registrera data

En profil är en representation av ett ämne, en organisation eller en individ, som består av många attribut (kallas även postdata). Profilen för en produkt kan t.ex. innehålla en SKU och en beskrivning, medan profilen för en person innehåller information som förnamn, efternamn och e-postadress. Med [!DNL Experience Platform] kan du anpassa profiler så att de använder specifika data som är relevanta för ditt företag. Standardklassen [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], är den klass som ska användas för att skapa ett schema när kundpostdata beskrivs, och tillhandahåller data som är integrerade i många interaktioner mellan plattformstjänster. Mer information om hur du arbetar med scheman i [!DNL Experience Platform] får du genom att läsa [systemöversikten för XDM](../xdm/home.md).

### Tidsseriehändelser

Med tidsseriedata får du en ögonblicksbild av systemet när en åtgärd vidtas antingen direkt eller indirekt av ett ämne, samt data som detaljerar själva händelsen. Tidsseriedata representeras av standardschemaklassen XDM ExperienceEvent och kan beskriva händelser som objekt som läggs till i en kundvagn, länkar som klickas och videofilmer som visas. Tidsseriedata kan användas för att basera segmenteringsregler på, och händelser kan nås individuellt i en profils kontext.

### Identiteter

Alla företag vill kommunicera med sina kunder på ett sätt som känns personligt. En av utmaningarna med att leverera relevanta digitala upplevelser till kunder är dock att förstå hur de ska koppla samman sina fristående data, som ofta sprids över olika digitala kanaler, som surfplattor, mobiltelefoner och bärbara datorer. [!DNL Identity Service] gör att ni kan sammanställa hela bilden av kunden genom att länka identiteter från flera kanaler och skapa ett identitetsdiagram för varje kund. Mer information finns på [Översikt över identitetstjänsten](../identity-service/home.md).

### Sammanfoga profiler

När du sammanför datafragment från flera olika källor och kombinerar dem för att få en fullständig bild av varje enskild kund, är sammanfogningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska användas för att skapa kundprofilen. När det finns data som är i konflikt med varandra från flera datauppsättningar avgör kopplingsregeln hur dessa data ska behandlas och vilket värde som ska användas. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen.

Mer information om hur du arbetar med sammanfogningsprinciper med API:t [!DNL Real-time Customer Profile] finns i [slutpunktshandboken för sammanfogningsprinciper](api/merge-policies.md). Om du vill arbeta med sammanfogningsprinciper med hjälp av användargränssnittet för [!DNL Experience Platform] läser du i användargränssnittshandboken för [sammanfogningsprinciper](ui/merge-policies.md).

### Unionens scheman {#profile-fragments-and-union-schemas}

En av de viktigaste funktionerna i [!DNL Real-time Customer Profile] är möjligheten att sammanställa flerkanalsdata. När [!DNL Real-time Customer Profile] används för att få åtkomst till en entitet kan den ge dig en sammanfogad vy över alla profilfragment för den entiteten över datauppsättningar, som kallas&quot;unionsvy&quot; och som görs möjlig genom ett så kallat unionsschema.

Om du vill veta mer om unionsscheman, inklusive hur du kommer åt unionsscheman i användargränssnittet, kan du gå till [gränssnittsguiden för unionsscheman](ui/union-schema.md).

### (Alfa) Beräknade attribut

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är alfavärden. Dokumentationen och funktionerna kan komma att ändras.

Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Mer information om beräknade attribut, inklusive hur rollberäknade attribut fungerar i Adobe Experience Platform, får du om du börjar med att läsa översikten [beräknade attribut](computed-attributes/overview.md).

## Profiler och segment

Adobe Experience Platform [!DNL Segmentation Service] producerar de målgrupper som behövs för att ge era enskilda kunder bättre upplevelser. När ett målgruppssegment skapas läggs ID:t för det segmentet till i listan över segmentmedlemskap för alla kvalificerande profiler. Segmentregler byggs och tillämpas på [!DNL Real-time Customer Profile]-data med RESTful API:er och användargränssnittet i Segment Builder. Läs [Översikt över segmenteringstjänsten](../segmentation/home.md) om du vill veta mer om segmentering.

### Direktuppspelningsuppläsning och direktuppspelningssegmentering

Realtidsinmatning är möjlig genom en process som kallas direktuppspelning. När data från profil- och tidsserier importeras bestämmer [!DNL Real-time Customer Profile] automatiskt att data ska inkluderas eller exkluderas från segment via en pågående process som kallas direktuppspelningssegmentering, innan de slås samman med befintliga data och unionsvyn uppdateras. Resultatet blir att ni omedelbart kan utföra beräkningar och fatta beslut för att leverera förbättrade, individanpassade upplevelser till kunderna när de interagerar med ert varumärke. När data importeras valideras de också för att säkerställa att de importeras på rätt sätt och att de överensstämmer med det schema som datauppsättningen baseras på. Om du vill ha mer information om vilken validering som görs under importen kan du börja med att läsa kvalitetsöversikten [för dataöverföring](../ingestion/quality/overview.md).

## Kantprojektioner

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe Experience Platform ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Till exempel använder Adobe-program som Adobe Target och Adobe Campaign kanter för att leverera personaliserade kundupplevelser i realtid. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten. Om du vill veta mer och börja arbeta med projektioner med hjälp av API:t [!DNL Real-time Customer Profile] kan du läsa [slutpunktshandboken för kantprojektion](api/edge-projections.md).

## Samlar in data i [!DNL Profile]

[!DNL Platform] kan konfigureras för att skicka post- och tidsseriedata till  [!DNL Profile]med stöd för direktuppspelning i realtid och batchförbrukning. Mer information finns i självstudiekursen om hur du [lägger till data i kundprofilen i realtid](tutorials/add-profile-data.md).

>[!NOTE]
>
>Data som samlas in via Adobe-lösningar, inklusive [!DNL Analytics Cloud], [!DNL Marketing Cloud] och [!DNL Advertising Cloud], flödar till [!DNL Experience Platform] och hämtas till [!DNL Profile].

### Profilätvärden

Med Insikter om observerbarhet kan ni visa nyckeltal i Adobe Experience Platform. Förutom [!DNL Experience Platform]-användningsstatistik och prestandaindikatorer för olika [!DNL Platform]-funktioner finns det specifika profilrelaterade mått som gör att du kan få insikt i inkommande begärandefrekvenser, lyckade intag, intagna poststorlekar och mycket annat. Om du vill veta mer kan du börja med att läsa översikten [API:t för observabilitet](../observability/api/overview.md), och en fullständig lista över kundprofilsmått i realtid finns i dokumentationen om [tillgängliga mätvärden](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] och [!DNL Privacy]

[!DNL Data governance] är en serie strategier och tekniker som används för att hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning.

När det gäller åtkomst av data spelar datastyrning en viktig roll inom [!DNL Experience Platform] på olika nivåer:
* Dataanvändningsetikett
* Dataåtkomstprinciper
* Åtkomstkontroll över data för marknadsföringsåtgärder

[!DNL Data governance] hanteras vid flera tillfällen. Det kan vara att bestämma vilka data som ska importeras till [!DNL Platform] och vilka data som är tillgängliga efter att ha fått i sig en viss marknadsföringsåtgärd. Om du vill ha mer information börjar du med att läsa [översikten över datastyrning](../data-governance/home.md).

### Hantera avanmälan och förfrågningar om datasekretess

[!DNL Experience Platform] gör det möjligt för dina kunder att skicka avanmälningsförfrågningar som rör användningen och lagringen av deras data inom  [!DNL Real-time Customer Profile]. Mer information om hur avanmälningsbegäranden hanteras finns i dokumentationen om [hur avanmälningsbegäranden](../segmentation/honoring-opt-outs.md) respekteras.

## Nästa steg och ytterligare resurser

Om du vill veta mer om hur du arbetar med [!DNL Real-time Customer Profile]-data med hjälp av användargränssnittet i Experience Platform eller profil-API:t börjar du med att läsa [gränssnittshandboken för profiler](ui/user-guide.md) respektive [API-utvecklarhandboken](api/overview.md).