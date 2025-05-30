---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;kunddataplattform i realtid;cdp i realtid;b2b;cdp;kundens AI
title: Real-Time CDP B2B edition - översikt
description: Översikt över Real-Time Customer Data Platform B2B Edition-konto
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---

# Real-Time Customer Data Platform B2B edition - översikt

Real-Time CDP B2B edition bygger på Adobe Real-Time Customer Data Platform (Real-Time CDP) och är utformat för marknadsförare som arbetar i en affärs-till-affärstjänstmodell. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

Det finns förbättringar i en rad olika Adobe Experience Platform-funktioner som skiljer Real-Time CDP B2B edition från B2C-motsvarigheten. De innehåller förbättringar av Experience Data Model (XDM) för B2B-användningsfall, uppgraderingar av identitetsupplösning och profilsegmentering samt en anpassad anslutning och mål för [!DNL Marketo Engage]. Med [!DNL Marketo]-kontakten kan B2B-varumärken koppla sina branschledande B2B-interaktionsdata till beteendeinformation för att vårda leads och förbättra kontobaserade marknadsföringsaktiviteter.

Med Real-Time CDP B2B edition kan man

* Kombinera data som samlats in från flera källor till en enda vy för att skapa helhetsbilder och kontoprofiler.
* Förbättra, segmentera och exportera alla era data från olika källor från en central lagringsplats med enhetliga kontoprofiler.
* Hantera era data med hjälp av datastyrningsverktyg som är tillgängliga i varje steg av centraliseringsprocessen för att säkerställa att era data följer juridiska regler och affärspolicyer.

Mer information om förbättringarna för Real-Time CDP B2B edition finns i avsnitten nedan.

## XML

Real-Time CDP B2B edition har flera nya XDM-schemaklasser, fältgrupper och relationstyper för att hämta in och strukturera data specifikt för B2B-ändamål. I översikten om [XDM i Real-Time CDP B2B edition](./schemas/b2b.md) finns en beskrivning av alla dessa förbättringar.

Genom att använda förkonfigurerade B2B-scheman kan du hämta in data i en standardiserad, hanterbar struktur. Många av de nya schemaklasserna mappas nästan direkt till de som finns i vanliga CRM-klasser som [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] och andra B2B-datakällor. Med Real-Time CDP B2B edition kan ni enkelt överföra data från B2B-källor till Experience Platform och få resultat som är enkla att granska.

Dessa XDM-förbättringar gör det möjligt att bättre importera och aktivera data via B2B-centrerade källor och mål, vilket förbättrar datainsamlingen och presentationen för fler olika och mer flexibla användningsfall.

## Identitetsupplösning

När scheman har definierats och data har importerats i enlighet med dessa scheman identifierar Real-Time CDP B2B edition källposter som representerar verkliga människor och företag via ett kraftfullt system för identitetsupplösning i realtid.

Identitetsupplösningssystemet har följande funktioner:

* Kombinerade register över B2B- och B2C-personal
* En kontohierarki på flera nivåer
* Många-till-många-anslutningar från människa till konto
* Personer och kontoidentiteter löses i realtid

Identitetsupplösningssystemet har utökats med stöd för en mer mångfacetterad klassificering av människor. Systemet gör det möjligt att identifiera människor som leads i affärsmöjligheter och kunder.

Kontoposter som synkroniseras av CRM-källan och som ansluts via flera sökvägar i systemet sammanfogas av Experience Platform. Systemet sammanför de personer som är förknippade med affärsmöjligheter och de som är registrerade som kunder, men det går även att bevara skillnaden mellan dem som ett attribut om de är identifierbara.

Matchande identifierare används för att länka samman och sammanfoga kontoposter från flera system. Kontohierarkier bevaras under hela den här processen. Differentiatorer används för att undersöka om en person är kopplad till ett konto eller inte och för att kunna skilja dem från kontot vid behov.

## Profiler och segmentering

När Real-Time CDP B2B edition har inhämtat data och löst identiteter relaterade till människor, företag, attribut och beteenden används dessa data för att skapa profiler. Dessa profiler kan sedan segmenteras i webbläsbara målgrupper som sedan kan aktiveras för olika målgrupper.

När det implementeras korrekt spåras personer som använder unika primära identifierare i stället för attribut som kan ändras, till exempel e-postadresser. Det innebär att när någon ändrar jobb följer systemet dem fortfarande. Personen är fortfarande samma enhet, men i stället är de kopplade till ett nytt konto. Denna inbyggda funktionalitet är en utmärkt vektor för att expandera till nya konton eftersom systemet följer dessa personer som individer, inklusive alla deras attribut och beteenden.

## B2B-källor

Med Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Med källan [!DNL Marketo] kan du strömma B2B-data till Experience Platform och hålla dessa data uppdaterade med Experience Platform-anslutna program. Det stöder valfritt antal instanser av [!DNL Marketo] (vilket är fördelaktigt för stora företag med flera instanser) och samlas i en enda organisation där data sammanfogas.

>[!NOTE]
>
>[!DNL Marketo]-källan krävs **inte** för att använda Real-Time CDP B2B edition.

Se [källorna i dokumentationen för Real-Time CDP B2B edition](./sources/b2b.md) om du vill ha mer information om Marketo och hur du överför B2B-data till Experience Platform.

## B2B-mål

Experience Platform-mål som Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads och Google Ad Manager är tillgängliga och stöds fullt ut av Real-Time CDP B2B edition. Marketo Engage mål strömmar även data om segmentmedlemskap från Experience Platform och gör dem tillgängliga som listor i Marketo.

Mer information finns i översikten på [Marketo Engage Destination](../destinations/catalog/adobe/marketo-engage.md).

För företag med mer än en CRM kan Real-Time CDP B2B edition konfigurera målanslutningar till separata instanser av Marketo eller CRM. Om det behövs kan du konfigurera målanslutningar för varje instans och skicka målgrupper till var och en av CRM-instanserna separat.

## Nästa steg

Nu när ni bättre förstår fördelarna för marknadsförarna som Real-Time CDP B2B edition erbjuder, och skillnaderna mellan det och Real-Time CDP, kan ni lära er hur ni använder dessa funktioner i er egen organisation.

Följande dokumentation hjälper dig att komma igång:

* [Ett exempel på hur man använder Real-Time CDP B2B edition](./b2b-use-case.md)
* [En komplett självstudiekurs för Real-Time Customer Data Platform B2B edition](./b2b-tutorial.md)
* [Importera data](./sources/b2b.md)
* [Åtkomst till profiler](./profile/profile-overview.md)
* [Scheman i Real-Time Customer Data Platform B2B edition](./schemas/b2b.md)
* [Så här skapar du målgrupper](./segmentation/b2b.md)
* [Så här aktiverar du målgrupper till destinationer](./destinations/b2b.md)
* [Definiera och tillämpa policyer för datastyrning](./privacy/data-governance-overview.md)
