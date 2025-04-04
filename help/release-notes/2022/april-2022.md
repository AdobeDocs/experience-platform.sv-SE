---
title: Versionsinformation om Adobe Experience Platform april 2022
description: Versionsinformationen för Adobe Experience Platform från april 2022.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 13%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 27 april 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Dataflöden](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Real-Time Customer Data Platform B2B-utgåva](#B2B)
- [Källor](#sources)

## [!DNL Dashboards] {#dashboards}

Experience Platform tillhandahåller flera kontrollpaneler där du kan visa viktig information om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

Kontrollpanelerna tillhandahåller förkonfigurerade rapportalternativ för organisationens data och är inbyggda direkt i marknadsföringsarbetsflödet i Experience Platform. Dessa instrumentpaneler är tillgängliga utan behov av ytterligare IT-support eller den tid och ansträngning som annars skulle behövas för att exportera och bearbeta data med ytterligare design och implementering av datalagerhantering.

Följande widgetar är tillgängliga via widgetbiblioteket på deras respektive instrumentpaneler. Mer information om [hur du lägger till widgetar via widgetbiblioteket](../../dashboards/customize/widget-library.md) finns i dokumentationen.

**Nya widgetar**

| Widget | Kontrollpanel | Beskrivning |
| ------ | --------- | ----------- |
| [!UICONTROL Profiles added trend] | Profiler | Den här widgeten använder ett linjediagram för att illustrera det totala antalet sammanfogade profiler som har lagts till i profilbutiken dagligen under de senaste 30 dagarna, 90 dagar eller 12 månaderna. |
| [!UICONTROL Audiences mapped to destination status] | Profiler | Den här widgeten visar det totala antalet både mappade och omappade målgrupper i ett enda mätresultat och använder ett ringdiagram för att illustrera den proportionella skillnaden mellan deras summor. |
| [!UICONTROL Audiences size] | Profiler | Den här widgeten innehåller en tabell med två kolumner som visar upp till 20 segment och det totala antalet målgrupper i varje segment. Listan är beroende av vilken sammanfogningspolicy som tillämpas och ordnas från hög till låg enligt det totala antalet målgrupper. |
| [!UICONTROL Profile count trend] | Profiler | Den här widgeten använder ett linjediagram för att illustrera trenden i det totala antalet profiler som finns i systemet över tiden. Data kan visualiseras under 30 dagar, 90 dagar och 12 månader. |
| [!UICONTROL Single identity profiles by identity] | Profiler | Den här widgeten använder ett stapeldiagram för att illustrera det totala antalet profiler som identifieras med endast en unik identifierare. Widgeten stöder upp till fem av de vanligaste identiteterna. |
| [!UICONTROL Destination status] | Mål | Den här widgeten visar det totala antalet aktiverade destinationer som ett enda mått och använder ett ringdiagram för att illustrera den proportionella skillnaden mellan aktiverade och inaktiverade destinationer. |
| [!UICONTROL Active destinations by destination platform] | Mål | Den här widgeten använder en tabell med två kolumner för att visa en lista över aktiva målplattformar och det totala antalet aktiva destinationer för varje målplattform. |
| [!UICONTROL Activated audiences across all destinations] | Mål | Den här widgeten visar totalt antal målgrupper som har aktiverats för alla destinationer i ett enda mätresultat. |
| [!UICONTROL Audience activation order] | Segment | Den här widgeten innehåller en tabell med tre kolumner som visar målnamnet, plattformen och aktiveringsdatumet för målgruppen. |
| [!UICONTROL Audience size trend] | Segment | Den här widgeten innehåller en illustration av ett linjediagram för det totala antalet profiler som uppfyller villkoren för en segmentdefinition under 30 dagar, 90 dagar och 12-månadersperioder. |
| [!UICONTROL Audience size change trend] | Segment | Den här widgeten innehåller ett linjediagram som illustrerar skillnaden i det totala antalet profiler som är kvalificerade för ett visst segment mellan de senaste ögonblicksbilderna. Perioden för trendanalys kan visualiseras under 30 dagar, 90 dagar och 12 månader. |
| [!UICONTROL Audience size trend by identity] | Segment | Den här widgeten visar trenden för målgruppsstorlek för ett visst segment baserat på en vald identitetstyp. Perioden för trendanalys kan visualiseras under 30 dagar, 90 dagar och 12 månader. |

**Nya funktioner** {#new-features}

| Funktion | Kontrollpanel | Beskrivning |
| ------- | --------- | ----------- |
| Rensning av överblivet profilsegmentmedlemskap | Profiler och licensanvändning | Profiltjänsten tar nu bort kvarvarande segment dagligen för att ge en mer korrekt återgivning av dina profiler i ditt system. Den här rensningen inträffar när alla profilfragment för en viss profil har tagits bort. Detta kan visa en minskning av&quot;adresserbar målgrupp&quot;-måttet på kontrollpanelen för licensanvändning och kan visa en minskning i &quot;profilantalet&quot;-måttet på kontrollpanelen för profiler, eftersom dessa mått inkluderade kvarvarande segment före den här versionen. |

{style="table-layout:auto"}

Mer information om [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md) och [[!DNL Segments]](../../dashboards/guides/audiences.md) kontrollpaneler finns i dokumentationen.

## Dataflöden {#dataflows}

I Experience Platform hämtas data från många olika källor, analyseras i systemet och aktiveras till en mängd olika destinationer. Experience Platform gör processen att spåra detta potentiellt icke-linjära dataflöde enklare genom att tillhandahålla genomskinlighet med dataflöden.

Dataflöden är en representation av jobb som flyttar data mellan Experience Platform. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, där de sedan används av identitetstjänsten och kundprofilen i realtid innan de aktiveras för destinationerna.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Kontrollpanel för segment | Nu kan du använda kontrollpanelen för övervakning för att övervaka dataflöden för segment. Mer information finns i guiden om [övervakning av segment i användargränssnittet](../../dataflows/ui/monitor-audiences.md). |

Mer allmän information om dataflöden finns i [dataflödesöversikten](../../dataflows/home.md). Mer information om segmentering finns i [segmenteringsöversikten](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för Adobe Analytics | Adobe Analytics-källan har nu stöd för Data Prep-funktioner, vilket gör att du kan mappa data från Analytics-rapportsviten till ett mål-XDM-schema när du skapar ett dataflöde. Mer information finns i självstudiekursen [Skapa en Analytics-källanslutning](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Import av befintliga mappningsregler | Nu kan du importera mappningsregler från ett befintligt dataflöde för att snabba upp dataflödeskonfigurationerna och begränsa antalet fel. Mer information finns i självstudiekursen [Importera befintliga mappningsregler](../../data-prep/ui/mapping.md). |

Mer information om [!DNL Data Prep] finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| Avancerade målanslutningar för företag | Tre målanslutningar för företag är nu allmänt tillgängliga: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md) och [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> Den allmänna tillgängligheten för Enterprise-målanslutningar omfattar alla funktioner som tidigare fanns i Beta-fasen och mycket mer: <ul><li>Nya autentiseringsfunktioner, inklusive [signatur för delad åtkomst i Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) och fler [autentiseringstyper](../../destinations/catalog/streaming/http-destination.md#authentication-information) (innehavartoken, OAuth2) i HTTP API-målet;</li><li>[Bakgrundsfyllning av tidigare profildata](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (skickar historiska profiler som är kvalificerade för segmentet när det aktiveras första gången);</li><li>Data Flow Run-mätvärden stöds nu för dessa destinationer.</li><li>[Ytterligare segmentmetadata](../../destinations/catalog/streaming/http-destination.md#destination-details) ingår i datanyttolasten, inklusive segmentnamn och segmenttidsstämplar;</li><li>Stöd för [statiska IP-adresser](/help/destinations/catalog/streaming/ip-address-allow-list.md) för kunder som behöver tillåtslista Experience Platform.</li></ul> |
| Aviseringar i sitt sammanhang för måldataflöden | Du kan nu [prenumerera på aviseringar](../../destinations/ui/alerts.md) när du skapar ett måldataflöde och få varningsmeddelanden om status, slutförande eller fel i dataflödet. Du kan välja att få aviseringar i Experience Platform-gränssnittet eller via e-post. |

### Frisläppningsprocess för avancerade målanslutningar för företag {#release-process-enterprise-destinations}

För Amazon Kinesis, Azure Event Hubs och HTTP API-destinationer visas både det tidigare Beta-destinationskortet och det nya allmänt tillgängliga (GA) destinationskortet i målkatalogen under versionsprocessen (från och med den 27 april). Alla dataflöden som konfigureras av kunder som använder betatestarna migreras inom de närmaste dagarna till GA-versionen av samma mål. Denna migrering bör vara slutförd till slutet av fredagen den 29 april. Beta-destinationerna kommer att fortsätta vara synliga under det här korta tidsfönstret och märkta med **Föråldrat**.

Observera följande om du har använt dessa destinationer under Beta fas:

- Om du tidigare har varit i Beta med någon av de tre destinationerna behövs ingen åtgärd. Alla dataflöden som installeras som en del av Beta kommer att fortsätta att fungera och kommer att migreras till GA-versionen.
- Om du vill konfigurera dessa destinationer från och med den 27 april, gör det med den nya GA-versionen av destinationerna.
- Betakorten som markerats som inaktuella tas bort när releaseversionen är klar, vilket beräknas inträffa till slutet av fredagen den 29 april. Experience Platform tekniska team håller på att övervaka en lyckad lanseringsåtgärd.

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [!DNL Criteo] | Anslut och aktivera data till annonsplattformen [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md). |
| [!DNL Sendgrid] | Anslut och aktivera data till [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md)-plattformen för transaktions- och marknadsföringsmeddelanden. |

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Lägga till eller ta bort enskilda standardfält för ett schema | Nu kan du lägga till delar av standardfältgrupper i scheman, vilket ger större flexibilitet för de fält du väljer att ta med utan att du behöver skapa anpassade resurser från grunden.<br><br>Du kan nu även definiera egna ad hoc-fält direkt i schemastrukturen och tilldela dem till en ny eller befintlig anpassad fältgrupp utan att behöva skapa eller redigera fältgruppen i förväg.<br><br>Mer information om de här nya arbetsflödena finns i guiden [Skapa och redigera scheman i användargränssnittet](../../xdm/ui/resources/schemas.md). |

{style="table-layout:auto"}

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Globalt schema | [[!UICONTROL Data Hygiene Operation Request]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Hämtar information om en datarensningsbegäran om att ta bort eller ändra poster i en angiven datamängd eller sandlåda. |
| Beskrivning | [[!UICONTROL Time-series Granularity Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Anger granulariteten för tidsserie- och sammanfattningsdata. När schemat används är schemats `timestamp`-fält den första tidsstämpeln i en period av den här granulariteten. |
| Klass | [[!UICONTROL XDM Summary Metrics]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Tillhandahåller försummerade mått med grupperingsdimensioner, t.ex. resultatet av en SQL SELECT med en GROUP BY. |
| Fältgrupp | [[!UICONTROL Consent policies evaluation results map]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Hämtar utvärderingsresultatet för principen för samtycke för en individ. |
| Fältgrupp | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Hämtar platssökningsrelaterad information som sökfråga, filtrering och ordning. |
| Fältgrupp | [[!UICONTROL Merge Leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Hämtar information om en händelse där två eller flera leads sammanfogas. |
| Fältgrupp | [[!UICONTROL Email Sent]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Hämtar information om en händelse där ett e-postmeddelande skickas till en mottagare. |
| Fältgrupp | [[!UICONTROL Stitching Fields]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Hämtar värden som beräknas genom identitetssammanfogningsprocessen för en händelse. |
| Fältgrupp | [[!UICONTROL Secondary Recipient Detail For Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | En Adobe Journey Optimizer-fältgrupp som samlar in en sekundär mottagarinformation för en granskning. |
| Fältgrupp | [[!UICONTROL XDM Business Account Person Relation Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hämtar information som är relaterad till en konto-person-relation. |
| Fältgrupp | [[!UICONTROL Account Person Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hämtar information som är relaterad till en konto-person-relation. |
| Datatyp | [[!UICONTROL Cart]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Fångar information om en e-handelskundvagn. |
| Datatyp | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Hämtar leveransinformation för en eller flera produkter. |
| Datatyp | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Hämtar information om webbplatssökningsaktivitet. |
| Tillägg (Workfront) | [[!UICONTROL Operational Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Hämtar information om en operativ uppgift. |
| Tillägg (Workfront) | [[!UICONTROL Work Portfolio Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Hämtar information om en arbetsportfölj. |
| Tillägg (Workfront) | [[!UICONTROL Work Program Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Hämtar information om ett arbetsprogram. |
| Tillägg (Workfront) | [[!UICONTROL Work Project Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Hämtar information om ett arbetsprojekt. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Uppdatera beskrivning |
| --- | --- | --- |
| Globalt schema | [[!UICONTROL Destinations]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nya uppräkningsvärden för `destinationCategory`. |
| Beskrivning | [[!UICONTROL Friendly Name Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Stöd för borttagning av föreslagna värden (`meta:enum`) som inte behövs från standardfält har lagts till. |
| Fältgrupp | [[!UICONTROL User Login Process]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | Fältet `createProfile` har lagts till. |
| Datatyp | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Flera kundvagnsrelaterade fält har lagts till. |
| Datatyp | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nya fält har lagts till för valda alternativ och rabattbelopp. |
| Tillägg (Intelligent Services) | [[!UICONTROL Intelligent Services JourneyAI Send Time Optimization]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimera lagringsformatet för bakgrundsmusik. |
| Tillägg (Workfront) | [[!UICONTROL Workfront Change Event]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Flera fält har ersatts med ett `workfront:customData`-fält för anpassade formulärfält. |
| Tillägg (Workfront) | [[!UICONTROL Work Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Flera fält har lagts till. |
| Tillägg (Workfront) | [[!UICONTROL Work Object]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nya fält för överordnad objekttyp och anpassade formulärfält. |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

AI/ML-tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskap.

### Attribution AI

Attribution AI används för att attribuera krediter till kontaktpunkter som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktpunkt för marknadsföring över kundresor.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för flera datauppsättningar | Funktionen Multi DataSet har nu stöd för alla Experience Event-datamängder samt valet av Identity Map som identitet. Kunder kan välja identitetskartan och alla associerade ID:n så länge det finns ett gemensamt ID-namnutrymme mellan datauppsättningar. Attribution AI har stöd för följande scheman: Adobe Analytics, Experience Event, Consumer Experience Event. Mer information om stöd för flera datauppsättningar i Attribution AI finns i användarhandboken för [Attribution AI](../../intelligent-services/attribution-ai/user-guide.md). |

Mer information om [!DNL Intelligent Services] finns i [[!DNL Intelligent Services] översikten](../../intelligent-services/home.md).

### Kund-AI

Customer AI available in Real-Time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, utbilda eller distribuera.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för flera datauppsättningar | Funktionen Multi DataSet har nu stöd för alla Experience Event-datamängder samt valet av Identity Map som identitet. Kunder kan välja identitetskartan och alla associerade ID:n så länge det finns ett gemensamt ID-namnutrymme mellan datauppsättningar. Kunds-AI stöder följande scheman: Adobe Analytics, Experience Event, Consumer Experience Event och Adobe Audience Manager schema. Mer information om stöd för flera datauppsättningar i kundens AI finns i [användarhandboken för AI för kunder](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nya mått för modellutvärdering i kundens AI | Nya vinstscheman i kundens AI gör det möjligt för marknadsförare att fastställa gruppstorleken utifrån sin budget och sina lönsamhetsmål. Nya Lyft-diagram mäter modellens kvalitet och ger bättre synlighet i lyften de skulle få över slumpmässig målinriktning. Mer information finns i dokumentet [Identifiera insikter med kundens AI](../../intelligent-services/customer-ai/user-guide/discover-insights.md). |

Mer information om [!DNL Intelligent Services] finns i [[!DNL Intelligent Services] översikten](../../intelligent-services/home.md).

## Real-Time Customer Data Platform B2B-utgåva {#B2B}

Real-Time CDP B2B edition bygger på Real-Time Customer Data Platform (Real-Time CDP) och är utformat för marknadsförare som arbetar i en affärs-till-affärstjänstmodell. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för funktionen `isDeleted` | Alla [!DNL Marketo]-datauppsättningar utom `Activities` har nu stöd för mappningen `isDeleted`. Den nya mappningen läggs automatiskt till i dina befintliga B2B-dataflöden. Du kan använda mappningen `isDeleted` för att filtrera bort poster som har tagits bort så att dina data i [!DNL Data Lake] är konsekventa med dina källdata. Mer information om `isDeleted` finns i guiden [[!DNL Marketo] för mappningsfält](../../sources/connectors/adobe-applications/mapping/marketo.md). |

Mer information om Real-Time Customer Data Platform B2B edition finns i [B2B-översikten](../../rtcdp/b2b-overview.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för [!DNL OneTrust Integration] | Du kan nu använda källan [!DNL OneTrust Integration] för att importera medgivanden och inställningsdata från ditt [!DNL OneTrust]-konto till Experience Platform. Mer information finns i dokumentationen om [att skapa en [!DNL OneTrust Integration] källanslutning](../../sources/connectors/consent-and-preferences/onetrust.md). |
| Stöd för [!DNL Square] | Du kan nu använda källan [!DNL Square] för att importera betalningsdata från ditt [!DNL Square]-konto till Experience Platform. |
| Stöd för att ta bort kundattributsdataflöden | Nu kan du ta bort dataflöden som har skapats med källkopplingen för kundattribut. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
