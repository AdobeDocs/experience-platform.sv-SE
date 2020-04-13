---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Översikt över kundprofiler i realtid
topic: guide
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c

---


# Översikt över kundprofiler i realtid

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder, oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av en profil kan ni sammanställa olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion. Denna översikt hjälper er att förstå vilken roll ni har och hur ni använder kundprofilen i realtid i Experience Platform.

## Förstå kundprofil i realtid

Kundprofil i realtid är ett generiskt uppslagsarkiv som sammanfogar data från olika företagsdatatillgångar och sedan ger tillgång till dessa data i form av enskilda kundprofiler och relaterade tidsseriehändelser. Med den här funktionen kan marknadsförarna skapa samordnade, enhetliga och relevanta upplevelser med sina målgrupper i flera kanaler.

### Profildatalager

Även om kundprofilen i realtid bearbetar inkapslade data och använder Adobe Experience Platform Identity Service för att sammanfoga relaterade data via identitetsmappning, behåller den sina egna data i profilarkivet. Profilarkivet är med andra ord skilt från data för katalogdata (Data Lake) och identitetstjänst (identitetsdiagram).

### Profil- och plattformstjänster

Förhållandet mellan kundprofil i realtid och andra tjänster inom Experience Platform framgår av följande diagram:

![Förhållandet mellan profilen och andra Experience Platform-tjänster.](images/profile-overview/profile-in-platform.png)

### Profiler och registrera data

En profil är en representation av ett ämne, en organisation eller en individ, som också kallas registerdata. Profilen för en produkt kan t.ex. innehålla en SKU och en beskrivning, medan profilen för en person innehåller information som förnamn, efternamn och e-postadress. Med Experience Platform kan ni anpassa profiler för att använda olika typer av data som är relevanta för ert företag. Klassen XDM (Standard Experience Data Model) för en enskild profil är den klass som rekommenderas för att skapa ett schema när kundpostdata beskrivs, och som tillhandahåller data som är integrerade i många interaktioner mellan plattformstjänster. Mer information om hur du arbetar med scheman i Experience Platform får du om du börjar med att läsa översikten över [XDM-systemet](../xdm/home.md).

### Tidsseriehändelser

Med tidsseriedata får du en ögonblicksbild av systemet när en åtgärd vidtas antingen direkt eller indirekt av ett ämne, samt data som detaljerar själva händelsen. Tidsseriedata representeras av standardschemaklassen XDM ExperienceEvent och kan beskriva händelser som objekt som läggs till i en kundvagn, länkar som klickas och videofilmer som visas. Tidsseriedata kan användas för att basera segmenteringsregler på, och händelser kan nås individuellt i en profils kontext.

### Identiteter

Alla företag vill kommunicera med sina kunder på ett sätt som känns personligt. En av utmaningarna med att leverera relevanta digitala upplevelser till kunder är dock att förstå hur de ska koppla samman sina fristående data, som ofta sprids över olika digitala kanaler, som surfplattor, mobiltelefoner och bärbara datorer. Med Identity Service kan ni sammanställa hela bilden av kunden genom att länka identiteter från flera kanaler, skapa ett identitetsdiagram för varje kund så att ni bättre kan förstå dem. Mer information finns i översikten över [identitetstjänsten](../identity-service/home.md) .

### Segmentering

Adobe Experience Platform Segmentation Service producerar de målgrupper som behövs för att ge era enskilda kunder bättre upplevelser. När ett målgruppssegment skapas läggs ID:t för det segmentet till i listan över segmentmedlemskap för alla kvalificerande profiler. Segmentregler byggs och tillämpas på kundprofildata i realtid med RESTful API:er och användargränssnittet i Segment Builder. Om du vill veta mer om segmentering börjar du med att läsa översikten över [segmenteringstjänsten](../segmentation/home.md).

### Profilfragment och föreningsscheman {#profile-fragments-and-union-schemas}

En av de viktigaste funktionerna i kundprofilen i realtid är möjligheten att sammanställa flerkanalsdata. När kundprofilen i realtid används för att få åtkomst till en enhet kan den ge dig en sammanslagen vy över alla profilfragment för den entiteten i alla datauppsättningar, som kallas unionsvy och görs möjlig genom ett så kallat unionsschema. Kundprofildata i realtid sammanfogas mellan olika källor när en enhet eller profil nås via dess ID eller exporteras som ett segment. Om du vill veta mer om hur du får tillgång till profiler och unionsvyer kan du besöka underhandboken för utveckling av kundprofil-API i realtid på [entiteter, som också kallas profilåtkomst](api/entities.md).

### Sammanfoga profiler

När ni sammanfogar data från flera olika källor och kombinerar dem för att få en fullständig bild av var och en av era enskilda kunder, är sammanslagningsprinciper de regler som Platform använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Mer information om hur du arbetar med sammanfogningsprinciper med API:er finns i delhandboken [för](api/merge-policies.md) sammanfogningsprinciper för kundprofil i realtid eller användarhandboken för [sammanfogningsprinciper](ui/merge-policies.md) för hur du arbetar med sammanfogningsprinciper med hjälp av användargränssnittet för plattformen.

## (Alfa) Konfigurera beräknade attribut

>[!IMPORTANT]
>Den beräknade attributfunktionaliteten som beskrivs i det här dokumentet är alfavärden. Dokumentationen och funktionaliteten kan komma att ändras.

Med beräknade attribut kan du automatiskt beräkna fältvärden baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån, vilket innebär att du kan samla värden för alla poster och händelser. Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut eller i en händelse. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Mer information om beräknade attribut och steg-för-steg-anvisningar om hur du arbetar med dem finns i [underhandledningen till kundprofils-API:t i realtid om beräknade attribut](api/computed-attributes.md). Den här guiden hjälper dig att bättre förstå vilken roll beräknade attribut spelar i Adobe Experience Platform, och den innehåller exempel på API-anrop för att utföra grundläggande CRUD-åtgärder med hjälp av kundprofils-API:t i realtid.

## Realtidskomponenter

I det här avsnittet introduceras de komponenter som gör att kundprofilen i realtid kan uppdatera och övervaka data från post- och tidsserier i realtid.

### Direktuppspelningsuppläsning och direktuppspelningssegmentering

Realtidsinmatning är möjlig genom en process som kallas direktuppspelning. När data från profil- och tidsserier hämtas bestämmer kundprofilen i realtid automatiskt att inkludera eller exkludera data från segment genom en pågående process som kallas direktuppspelningssegmentering, innan den sammanfogas med befintliga data och unionsvyn uppdateras. Resultatet blir att ni omedelbart kan utföra beräkningar och fatta beslut för att leverera förbättrade, individanpassade upplevelser till kunderna när de interagerar med ert varumärke. När data importeras valideras de också för att säkerställa att de importeras på rätt sätt och att de överensstämmer med det schema som datauppsättningen baseras på. Om du vill ha mer information om vilken validering som görs under importen kan du börja med att läsa [kvalitetsöversikten](../ingestion/quality/overview.md)för dataimporten.

### Kantprojektioner

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Med Adobe Experience Platform får ni tillgång till data i realtid genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Adobe-program som Adobe Target och Adobe Campaign använder kanter för att leverera personaliserade kundupplevelser i realtid. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten. Om du vill veta mer och börja arbeta med kanter och projektioner kan du läsa underhandboken [Edge Projection för kundprofil i realtid](api/edge-projections.md).

## Lägg till data i kundprofilen i realtid

Plattformen kan konfigureras för att skicka data från poster och tidsserier till profilen, med stöd för direktuppspelning i realtid och batchinmatning. Mer information finns i självstudiekursen om hur du [lägger till data i kundprofilen](tutorials/add-profile-data.md)i realtid.

>[!Note]
>Data som samlas in via Adobe-lösningar, inklusive Analytics Cloud, Marketing Cloud och Advertising Cloud, flödar till Experience Platform och är inkapslade i profilen.

### Inmatningsstatistik för profilströmning

Med Insikter om observerbarhet kan ni visa viktiga mätvärden i Adobe Experience Platform. Förutom statistik om plattformsanvändning och prestandaindikatorer för olika plattformsfunktioner finns det specifika profilrelaterade mätvärden som gör att du kan få insikt i hur många begäranden som kommer in, hur många som kommer in, hur många som kommer in, hur många som kommer in i bilden och hur många som kommer in i posten. Om du vill veta mer kan du börja med att läsa översikten [över](../observability/home.md)observabilitetsinsikter och en fullständig lista över profilmått finns i dokumentationen om [tillgängliga mätvärden](../observability/metrics.md).

## Datastyrning och integritet

Datastyrning är en serie strategier och tekniker som används för att hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning.

När det gäller åtkomst av data spelar datastyrning en viktig roll inom Experience Platform på olika nivåer:
* Dataanvändningsetikett
* Dataåtkomstprinciper
* Åtkomstkontroll över data för marknadsföringsåtgärder

Datastyrning hanteras vid flera tillfällen. Det handlar om att bestämma vilka data som hämtas till Platform och vilka data som är tillgängliga efter att ha importerats för en viss marknadsföringsåtgärd. Mer information får du om du börjar med att läsa översikten över [datastyrning](../data-governance/home.md).

### Hantera avanmälan och förfrågningar om datasekretess

Med Experience Platform kan era kunder skicka avanmälningsförfrågningar relaterade till användningen och lagringen av sina data i kundprofilen i realtid. Mer information om hur avanmälningsbegäranden hanteras finns i dokumentationen om [hur avanmälningsbegäranden](../segmentation/honoring-opt-outs.md)respekteras.

## Nästa steg och ytterligare resurser

Om du vill veta mer om kundprofilen i realtid kan du fortsätta att läsa dokumentationen som finns i den här guiden och komplettera din inlärning genom att titta på videon nedan eller utforska andra videokurser [om](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)