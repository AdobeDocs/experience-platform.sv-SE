---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
title: Översikt över kundprofiler i realtid
topic: guide
description: Kundprofil i realtid är ett generiskt uppslagsarkiv som sammanfogar data från olika företagsdatatillgångar och sedan ger tillgång till dessa data i form av enskilda kundprofiler och relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler.
translation-type: tm+mt
source-git-commit: b8d6bd5caf6c6f4d1da218b6ca12cec154d64412
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] översikt

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-time Customer Profile]det kan ni få en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion. Den här översikten hjälper dig att förstå rollen och användningen av [!DNL Real-time Customer Profile] i [!DNL Experience Platform].

## [!DNL Profile] i Experience Platform

Förhållandet mellan kundprofil i realtid och andra tjänster inom Experience Platform framgår av följande diagram:

![Adobe Experience Platform tjänster.](images/profile-overview/profile-in-platform.png)

### Profildatalager

Även om inkapslade data [!DNL Real-time Customer Profile] bearbetas och Adobe Experience Platform används [!DNL Identity Service] för att sammanfoga relaterade data via identitetsmappning, behåller det sina egna data i [!DNL Profile] arkivet. Lagringen [!DNL Profile] är skild från [!DNL Catalog] data i [!DNL Data Lake] och [!DNL Identity Service] data i identitetsdiagrammet.

Profilarkivet använder en Microsoft Azure Cosmos DB-infrastruktur och Platform Data Lake använder Microsoft Azure Data Lake-lagring.

### Profilskyddsutkast

Experience Platform tillhandahåller ett antal skyddsutkast som hjälper dig att undvika att skapa XDM-scheman ( [Experience Data Model)](../xdm/home.md) som kundprofilen i realtid inte stöder. Detta inkluderar mjuka gränser som resulterar i försämrade prestanda, samt hårda gränser som resulterar i fel och systemfel. Mer information, inklusive en lista över riktlinjer och exempel på användningsfall, finns i dokumentationen för [profilskyddsutkast](guardrails.md) .

## Förstå profiler

[!DNL Real-time Customer Profile] sammanfogar data från olika affärssystem och ger sedan tillgång till dessa data i form av kundprofiler med relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler. I följande avsnitt beskrivs några av de grundläggande begrepp som du måste förstå för att effektivt kunna skapa och underhålla profiler inom plattformen.

### Profilfragment jämfört med sammanslagna profiler {#profile-fragments-vs-merged-profiles}

Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de för att skapa en enda profil för kunden.

När data från flera källor står i konflikt (t.ex. ett fragment listar kunden som&quot;enskild&quot; medan den andra anger kunden som&quot;gift&quot;) avgör [sammanfogningspolicyn](#merge-policies) vilken information som ska prioriteras och inkluderas i profilen för den enskilda personen. Det totala antalet profilfragment inom Platform är därför sannolikt alltid högre än det totala antalet sammanfogade profiler, eftersom varje profil består av flera fragment.

### Registrera data

En profil är en representation av ett ämne, en organisation eller en individ, som består av många attribut (kallas även postdata). Profilen för en produkt kan t.ex. innehålla en SKU och en beskrivning, medan profilen för en person innehåller information som förnamn, efternamn och e-postadress. Med [!DNL Experience Platform]kan ni anpassa profiler så att de använder specifika data som är relevanta för ert företag. Standardklassen [!DNL Experience Data Model] (XDM) [!DNL XDM Individual Profile]är den klass som ska användas för att skapa ett schema när kundpostdata beskrivs och som tillhandahåller data som är integrerade i många interaktioner mellan plattformstjänster. Mer information om hur du arbetar med scheman i [!DNL Experience Platform]finns i [XDM-systemöversikten](../xdm/home.md).

### Tidsseriehändelser

Med tidsseriedata får du en ögonblicksbild av systemet när en åtgärd vidtas antingen direkt eller indirekt av ett ämne, samt data som detaljerar själva händelsen. Tidsseriedata representeras av standardschemaklassen XDM ExperienceEvent och kan beskriva händelser som objekt som läggs till i en kundvagn, länkar som klickas och videofilmer som visas. Tidsseriedata kan användas för att basera segmenteringsregler på, och händelser kan nås individuellt i en profils kontext.

### Identiteter

Alla företag vill kommunicera med sina kunder på ett sätt som känns personligt. En av utmaningarna med att leverera relevanta digitala upplevelser till kunder är dock att förstå hur de ska koppla samman sina fristående data, som ofta sprids över olika digitala kanaler, som surfplattor, mobiltelefoner och bärbara datorer. [!DNL Identity Service] gör att ni kan sammanställa hela bilden av kunden genom att länka identiteter från flera kanaler och skapa ett identitetsdiagram för varje kund. Mer information finns i översikten över [identitetstjänsten](../identity-service/home.md) .

### Sammanfoga profiler

När du sammanför datafragment från flera olika källor och kombinerar dem för att få en fullständig bild av varje enskild kund, är sammanfogningsprinciper reglerna som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska användas för att skapa kundprofilen. När det finns data som är i konflikt med varandra från flera datauppsättningar avgör kopplingsregeln hur dessa data ska behandlas och vilket värde som ska användas. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Mer information om hur du arbetar med sammanfogningsprinciper med [!DNL Real-time Customer Profile] API finns i [slutpunktshandboken](api/merge-policies.md)för sammanfogningsprinciper. Om du vill arbeta med sammanfogningsprinciper med hjälp av [!DNL Experience Platform] användargränssnittet läser du i användarhandboken för [sammanfogningsprinciper](ui/merge-policies.md).

### Unionens system {#profile-fragments-and-union-schemas}

En av de viktigaste funktionerna i [!DNL Real-time Customer Profile] är möjligheten att sammanställa flerkanalsdata. När [!DNL Real-time Customer Profile] används för att få åtkomst till en enhet kan den ge dig en sammanslagen vy över alla profilfragment för den entiteten i alla datauppsättningar, som kallas unionsvyn och som görs möjlig genom ett så kallat unionsschema. [!DNL Real-time Customer Profile] data sammanfogas mellan olika källor när en enhet eller profil används av dess ID eller exporteras som ett segment. Mer information om hur du får åtkomst till profiler och unionsvyer med [!DNL Real-time Customer Profile] API:t finns i [enheternas slutpunktshandbok](api/entities.md).

### Segmentering

Adobe Experience Platform [!DNL Segmentation Service] producerar de målgrupper som behövs för att ge era enskilda kunder bättre upplevelser. När ett målgruppssegment skapas läggs ID:t för det segmentet till i listan över segmentmedlemskap för alla kvalificerande profiler. Segmentregler byggs och tillämpas på [!DNL Real-time Customer Profile] data med RESTful API:er och användargränssnittet i Segment Builder. Om du vill veta mer om segmentering börjar du med att läsa översikten över [segmenteringstjänsten](../segmentation/home.md).

### (Alfa) Konfigurera beräknade attribut

>[!IMPORTANT]
>
>Den beräknade attributfunktionen är alfavärden. Dokumentationen och funktionaliteten kan komma att ändras.

Med beräknade attribut kan du automatiskt beräkna fältvärden baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån, vilket innebär att du kan samla värden över alla poster och händelser. Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut eller i en händelse. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Mer information om beräknade attribut och steg-för-steg-instruktioner om hur du arbetar med dem med API:t finns i [!DNL Real-time Customer Profile] slutpunktshandboken [](api/computed-attributes.md)för beräknade attribut. Den här guiden hjälper dig att bättre förstå vilken roll beräknade attribut spelar i Adobe Experience Platform, och den innehåller exempel på API-anrop för grundläggande CRUD-åtgärder.

## Realtidskomponenter

I det här avsnittet introduceras de komponenter som gör det möjligt [!DNL Real-time Customer Profile] att uppdatera och övervaka post- och tidsseriedata i realtid.

### Direktuppspelningsuppläsning och direktuppspelningssegmentering

Realtidsinmatning är möjlig genom en process som kallas direktuppspelning. När data från profil- och tidsserier hämtas bestämmer sig [!DNL Real-time Customer Profile] automatiskt för att inkludera eller exkludera data från segment via en pågående process som kallas direktuppspelningssegmentering, innan de slås samman med befintliga data och unionsvyn uppdateras. Resultatet blir att ni omedelbart kan utföra beräkningar och fatta beslut för att leverera förbättrade, individanpassade upplevelser till kunderna när de interagerar med ert varumärke. När data importeras valideras de också för att säkerställa att de importeras på rätt sätt och att de överensstämmer med det schema som datauppsättningen baseras på. Om du vill ha mer information om vilken validering som görs under importen kan du börja med att läsa [kvalitetsöversikten](../ingestion/quality/overview.md)för dataimporten.

### Konfiguration och mål för Edge-projektion

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe Experience Platform ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Adobe-program som Adobe Target och Adobe Campaign använder kanter för att leverera personaliserade kundupplevelser i realtid. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten. Om du vill veta mer och börja arbeta med projektioner med hjälp av [!DNL Real-time Customer Profile] API:t kan du läsa guiden [för](api/edge-projections.md)kantprojektionsslutpunkter.

## Infoga data i [!DNL Profile]

[!DNL Platform] kan konfigureras för att skicka post- och tidsseriedata till [!DNL Profile]med stöd för direktuppspelning i realtid och batchförbrukning. Mer information finns i självstudiekursen om hur du [lägger till data i kundprofilen](tutorials/add-profile-data.md)i realtid.

>[!NOTE]
>
>Data som samlas in via Adobe-lösningar, inklusive [!DNL Analytics Cloud], [!DNL Marketing Cloud]och [!DNL Advertising Cloud]flödar in [!DNL Experience Platform] och hämtas in i [!DNL Profile].

### [!DNL Profile] mätvärden för förtäring

Med Insikter om observerbarhet kan ni visa nyckeltal i Adobe Experience Platform. Förutom [!DNL Platform] användningsstatistik och resultatindikatorer för olika [!DNL Platform] funktioner finns det specifika [!DNL Profile]mätvärden som gör att ni kan få insikt i hur många begäranden som kommer in, hur många som kommer in, hur många som kommer in, hur många som kommer in, hur många som kommer in i bilden och hur många som kommer in. Om du vill veta mer kan du börja med att läsa översikten över API:t för [observabilitet](../observability/api/overview.md), och en fullständig lista över [!DNL Profile] mätvärden finns i dokumentationen om [tillgängliga mätvärden](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] och [!DNL Privacy]

[!DNL Data governance] är en serie strategier och tekniker som används för att hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning.

När det gäller åtkomst av data spelar datastyrning en viktig roll på [!DNL Experience Platform] olika nivåer:
* Dataanvändningsetikett
* Dataåtkomstprinciper
* Åtkomstkontroll över data för marknadsföringsåtgärder

[!DNL Data governance] hanteras vid flera tillfällen. Det handlar om att bestämma vilka data som ska importeras till [!DNL Platform] och vilka data som är tillgängliga efter intag för en viss marknadsföringsåtgärd. Mer information får du om du börjar med att läsa översikten över [datastyrning](../data-governance/home.md).

### Hantera avanmälan och förfrågningar om datasekretess

[!DNL Experience Platform] gör det möjligt för dina kunder att skicka avanmälningsförfrågningar som rör användningen och lagringen av deras data inom [!DNL Real-time Customer Profile]. Mer information om hur avanmälningsbegäranden hanteras finns i dokumentationen om [hur avanmälningsbegäranden](../segmentation/honoring-opt-outs.md)respekteras.

## Nästa steg och ytterligare resurser

Mer information om hur du arbetar med [!DNL Real-time Customer Profile]finns i [Profilanvändarhandboken](ui/user-guide.md) eller [API-utvecklarhandboken](api/overview.md).

>[!WARNING]
>
>Användargränssnittet i Experience Platform uppdateras ofta och kan ha ändrats sedan videon spelades in. Läs användarhandboken för [kundprofilen i realtid](ui/user-guide.md) för de senaste skärmbilderna och funktionerna i användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)