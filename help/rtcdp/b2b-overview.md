---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;realtime customer data platform;real time cdp;b2b;cdp;Customer AI
title: Översikt över CDP B2B Edition i realtid
seo-title: Real-time Customer Data Platform B2B Edition overview
description: Översikt över Kunddataplattform B2B Edition-konto i realtid
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: e54bd747a332e37920e24ce07602470f8ad74231
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# Översikt över Customer Data Platform B2B Edition i realtid

>[!IMPORTANT]
>
>CDP B2B Edition är i realtid i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

CDP B2B Edition i realtid bygger på Customer Data Platform (CDP i realtid) och är avsedd för marknadsförare som använder en modell för business-to-business-service. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

Det finns förbättringar i en rad olika Adobe Experience Platform-funktioner som skiljer CDP B2B Edition i realtid från B2C-motsvarigheten. De innehåller förbättringar av Experience Data Model (XDM) för B2B-användningsfall, uppgraderingar av identitetsupplösning och profilsegmentering samt en anpassad anslutning och destination för [!DNL Marketo Engage]. Med [!DNL Marketo]-kopplingen kan B2B-varumärken koppla sina branschledande B2B-interaktionsdata till beteendeinformation för att vårda leads och förbättra kontobaserade marknadsföringsaktiviteter.

Med CDP B2B Edition i realtid kan man

* Kombinera data som samlats in från flera källor till en enda vy för att skapa helhetsbilder och kontoprofiler.
* Förbättra, segmentera och exportera alla era data från olika källor från en central lagringsplats med enhetliga kontoprofiler.
* Hantera era data med hjälp av datastyrningsverktyg som är tillgängliga i varje steg av centraliseringsprocessen för att säkerställa att era data följer juridiska regler och affärspolicyer.

Mer omfattande information om förbättringarna för CDP B2B Edition i realtid finns i avsnitten nedan.

## XDM

CDP B2B Edition i realtid innehåller flera nya XDM-schemaklasser, fältgrupper och relationstyper för att hämta in och strukturera data specifikt för B2B-ändamål. I översikten om [XDM i CDP B2B-utgåva i realtid](./schemas/b2b.md) finns en beskrivning av alla dessa förbättringar.

Genom att använda förkonfigurerade B2B-scheman kan du hämta in data i en standardiserad, hanterbar struktur. Många av de nya schemaklasserna mappas nästan direkt till de som finns i vanliga CRM-klasser som [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] och andra B2B-datakällor. Med CDP B2B Edition i realtid kan ni överföra data från B2B-källor till plattformen på ett enkelt sätt och med resultat som är enkla att granska.

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

Plattformen gör det möjligt att importera data från externa källor samtidigt som du får möjlighet att strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Med källan [!DNL Marketo] kan du strömma B2B-data till plattformen och hålla dessa data uppdaterade med plattformsanslutna program. Det stöder valfritt antal instanser av [!DNL Marketo] (vilket är fördelaktigt för stora företag med flera instanser) och samlas i en enda IMS-organisation där data sammanfogas.

>[!NOTE]
>
>[!DNL Marketo]-källan är **inte** som krävs för att använda CDP B2B Edition i realtid.

Läs källorna i dokumentationen för CDP B2B Edition i realtid om du vill ha mer information om Marketo och hur man lägger in B2B-data på plattformen.

<!-- PLACEHOLDER [sources in Real-time CDP B2B Edition](./sources/b2b) -->

## B2B-destinationer

Alla mål för Experience Platform som [!DNL Google], [!DNL Linkedin] eller [!DNL Facebook] är tillgängliga och stöds fullt ut av CDP B2B Edition i realtid. Det finns också ett [!DNL Marketo Engage]-mål som direktuppspelar data från [!DNL Marketo] eller utanför plattformen och gör den tillgänglig som målgrupper.

Målet [!DNL Marketo] är ett smidigt och snabbt sätt att hämta information från Experience Platform till [!DNL Marketo]. Målet gör att marknadsförare kan skicka segment som skapats i Adobe Experience Platform till [!DNL Marketo]. I [!DNL Marketo] är dessa målgrupper sedan tillgängliga som statiska listor.

För företag med mer än en CRM kan du konfigurera målanslutningar till separata instanser av [!DNL Marketo] eller CRM i realtid med CDP B2B Edition. Om det behövs kan du konfigurera målanslutningar för varje instans och skicka målgrupper till var och en av CRM-instanserna oberoende av varandra.

## Nästa steg

Nu när ni bättre förstår fördelarna för marknadsförare som erbjuds av CDP B2B Edition i realtid och skillnaderna mellan den och CDP i realtid kan ni lära er hur ni använder dessa funktioner i er egen IMS-organisation.

<!-- PLACEHOLDER [example use case for Real-time CDP B2B Edition]() -->

Om du vill veta hur CDP B2B Edition i realtid kan vara till nytta för din business-to-business-servicemodell kan du läsa exemplet på CDP B2B Edition i realtid. Du kan även läsa [scheman i dokumentationen för kunddataplattformen B2B Edition](./schemas/b2b.md) i realtid för mer specifik vägledning om hur du skapar scheman och definierar relationer för viktiga B2B-datatabeller.
