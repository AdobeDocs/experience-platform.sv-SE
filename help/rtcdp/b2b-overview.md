---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;kunddataplattform i realtid;cdp i realtid;b2b;cdp;kundens AI
title: Översikt över CDP B2B Edition i realtid
description: Översikt över Real-time Customer Data Platform B2B Edition-konto
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B Edition - översikt

CDP B2B Edition i realtid bygger på Real-time Customer Data Platform (Real-time CDP) och är särskilt framtagen för marknadsförare som använder en modell för business-to-business-service. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

Det finns förbättringar i en rad olika Adobe Experience Platform-funktioner som skiljer CDP B2B Edition i realtid från B2C-motsvarigheten. De innehåller förbättringar av Experience Data Model (XDM) för B2B-användningsfall, uppgraderingar av identitetsupplösning och profilsegmentering samt en anpassad anslutning och destination för [!DNL Marketo Engage]. The [!DNL Marketo] Tack vare kopplingen kan B2B-varumärken koppla sina branschledande B2B-interaktionsdata till beteendeinformation för att vårda leads och förbättra kontobaserade marknadsföringsaktiviteter.

Med CDP B2B Edition i realtid kan man

* Kombinera data som samlats in från flera källor till en enda vy för att skapa helhetsbilder och kontoprofiler.
* Förbättra, segmentera och exportera alla era data från olika källor från en central lagringsplats med enhetliga kontoprofiler.
* Hantera era data med hjälp av datastyrningsverktyg som är tillgängliga i varje steg av centraliseringsprocessen för att säkerställa att era data följer juridiska regler och affärspolicyer.

Mer omfattande information om förbättringarna för CDP B2B Edition i realtid finns i avsnitten nedan.

## XDM

CDP B2B Edition i realtid innehåller flera nya XDM-schemaklasser, fältgrupper och relationstyper för att hämta in och strukturera data specifikt för B2B-ändamål. Se översikten på [XDM i realtid CDP B2B Edition](./schemas/b2b.md) för en beskrivning av alla dessa förbättringar.

Genom att använda förkonfigurerade B2B-scheman kan du hämta in data i en standardiserad, hanterbar struktur. Många av de nya schemaklasserna mappas nästan direkt till dem som finns i vanliga CRM-system, som [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo]och andra B2B-datakällor. Med CDP B2B Edition i realtid kan ni överföra data från B2B-källor till plattformen på ett enkelt sätt och med resultat som är enkla att granska.

Dessa XDM-förbättringar gör det möjligt att bättre importera och aktivera data via B2B-centrerade källor och mål, vilket förbättrar datainsamlingen och presentationen för fler olika och mer flexibla användningsfall.

## Identitetsupplösning

När scheman har definierats och data har importerats i enlighet med dessa scheman identifierar CDP B2B Edition i realtid källposter som representerar verkliga människor och företag via ett kraftfullt system för identitetsmatchning i realtid.

Identitetsupplösningssystemet har följande funktioner:

* Kombinerade register över B2B- och B2C-personal
* En kontohierarki på flera nivåer
* Många-till-många-anslutningar från människa till konto
* Personer och kontoidentiteter löses i realtid

Identitetsupplösningssystemet har utökats med stöd för en mer mångfacetterad klassificering av människor. Systemet gör det möjligt att identifiera människor som leads i affärsmöjligheter och kunder.

Kontoposter som synkroniseras av CRM-källan och som ansluts via flera sökvägar i systemet sammanfogas av plattformen. Systemet sammanför de personer som är förknippade med affärsmöjligheter och de som är registrerade som kunder, men det går även att bevara skillnaden mellan dem som ett attribut om de är identifierbara.

Matchande identifierare används för att länka samman och sammanfoga kontoposter från flera system. Kontohierarkier bevaras under hela den här processen. Differentiatorer används för att undersöka om en person är kopplad till ett konto eller inte och för att kunna skilja dem från kontot vid behov.

## Profiler och segmentering

När CDP B2B Edition i realtid har inhämtat data och löst identiteter relaterade till människor, företag, attribut och beteenden används dessa data för att skapa profiler. Dessa profiler kan sedan segmenteras i webbläsbara målgrupper som sedan kan aktiveras för olika målgrupper.

När det implementeras korrekt spåras personer som använder unika primära identifierare i stället för attribut som kan ändras, till exempel e-postadresser. Det innebär att när någon ändrar jobb följer systemet dem fortfarande. Personen är fortfarande samma enhet, men i stället är de kopplade till ett nytt konto. Denna inbyggda funktionalitet är en utmärkt vektor för att expandera till nya konton eftersom systemet följer dessa personer som individer, inklusive alla deras attribut och beteenden.

## B2B-källor

Plattformen gör det möjligt att importera data från externa källor samtidigt som du får möjlighet att strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. The [!DNL Marketo] Med -källa kan du strömma B2B-data till plattformen och hålla dessa data uppdaterade med plattformsanslutna program. Det stöder valfritt antal förekomster av [!DNL Marketo] (vilket är fördelaktigt för stora företag med flera instanser) och samlas i en enda IMS-organisation där data sammanfogas.

>[!NOTE]
>
>The [!DNL Marketo] källan är **not** krävs för att använda CDP B2B Edition i realtid.

Se [källor i realtid CDP B2B Edition](./sources/b2b.md) om du vill ha mer information om Marketo och hur man lägger in B2B-data i Platform.

## B2B-destinationer

Destinationer som Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads och Google Ad Manager är tillgängliga och stöds fullt ut av CDP B2B Edition i realtid. Marketo Engage-målet strömmar även data om segmentmedlemskap från Platform och gör dem tillgängliga som listor i Marketo.

Se översikten på [Marketo Engage destination](../destinations/catalog/adobe/marketo-engage.md) för mer information.

För företag med mer än en CRM kan man i realtid med CDP B2B Edition konfigurera målanslutningar till separata instanser av Marketo eller CRM. Om det behövs kan du konfigurera målanslutningar för varje instans och skicka målgrupper till var och en av CRM-instanserna oberoende av varandra.

## Nästa steg

Nu när ni bättre förstår fördelarna för marknadsförare som erbjuds av CDP B2B Edition i realtid och skillnaderna mellan den och CDP i realtid kan ni lära er hur ni använder dessa funktioner i er egen IMS-organisation.

Om du vill veta hur CDP B2B Edition i realtid kan vara till nytta för din business-to-business-servicemodell kan du läsa följande dokumentation som hjälper dig att komma igång:

* [Ett exempel på hur man använder CDP B2B Edition i realtid](./b2b-use-case.md)
* [En komplett självstudiekurs för Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
* [Så här importerar du data](./sources/b2b.md)
* [Åtkomst till profiler](./profile/profile-overview.md)
* [Scheman i Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
* [Så här skapar du segment](./segmentation/b2b.md)
* [Så här aktiverar du segment till mål](./destinations/b2b.md)
* [Definiera och tillämpa policyer för datastyrning](./privacy/data-governance-overview.md)
