---
title: Versionsinformation om Adobe Experience Platform april 2023
description: Versionsinformationen för Adobe Experience Platform från april 2023.
exl-id: 7b501467-99a7-4aee-ae86-66c851250ecf
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 30%

---

# Versionsinformation för Adobe Experience Platform

>[!IMPORTANT]
>
>Från och med 15 maj 2023 kommer statusen `Existing` att tas bort från segmentmedlemskartan för att ta bort redundans i segmentmedlemskapets livscykel. Efter den här ändringen representeras profiler som är kvalificerade i ett segment som `Realized` och de profiler som är diskvalificerade fortsätter att representeras som `Exited`. Mer information om den här ändringen finns i avsnittet [Segmenteringstjänst](#segmentation).

**Releasedatum: 26 april 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Dataförberedelse](#data-prep)
- [Datainsamling](#data-collection)
- [Mål](#destinations)
- [Experience Data Model](#xdm)
- [Plattform för kunddata i realtid](#rtcdp)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner** {#dashboards-new-updated-features}

| Funktion | Beskrivning |
| --- | --- |
| Användardefinierade kontrollpaneler | Du kan nu **filtrera historiska data** från dina widgetinsikter och använda antingen senaste data eller en anpassad analysperiod. Mer information finns i handboken [användardefinierade kontrollpaneler](../../dashboards/standard-dashboards.md#filter-historical-data).<br>Du kan nu även **duplicera dina befintliga widgetar**. Genom att anpassa en dubblett och redigera deras attribut kan du undvika att starta om från början när du skapar en ny, unik widget. Läs [widgetens dupliceringsguide](../../dashboards/standard-dashboards.md#duplicate-a-widget) om du vill veta mer. |

{style="table-layout:auto"}

Läs [översikt över kontrollpaneler](../../dashboards/home.md) för mer information om kontrollpaneler, bland annat hur du beviljar åtkomstbehörigheter och skapar anpassade widgetar.

## Dataförberedelse {#data-prep}

Med dataförberedelse kan utvecklare mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av bakåtfyllnadsperiod för Adobe Analytics i icke-produktionssandlådor | Förifyllningsperioden för Adobe Analytics i icke-produktionssandlådor har reducerats till tre månader. Backfill för produktionssandlådor är desamma vid 13 månader. Den här ändringen gäller endast för nya flöden och påverkar inte befintliga flöden. Mer information finns i [Adobe Analytics-översikten](../../sources/connectors/adobe-applications/analytics.md). |
| Ny mappningsfunktion som konverterar FPID-strängar till ECID | Använd funktionen `fpid_to_ecid` för att konvertera FPID-strängar till ECID för användning i Experience Platform- och Experience Cloud-program. Mer information finns i handboken [Dataförberedelser ](../../data-prep/functions.md). |

{style="table-layout:auto"}

Mer information om dataprep finns i [översikten för dataprep](../../data-prep/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| IP-adressofuscation för datastreams | Nu kan du definiera IP-obfusionsalternativ på partiell eller fullständig datastream-nivå i [datastream-konfigurationens gränssnitt](../../datastreams/configure.md). <br><br>Inställningen för IP-obfusacering på datastream-nivå har företräde framför IP-ofuscation som har konfigurerats i Adobe Target och Audience Manager. <br><br>Data som skickas till Adobe Analytics påverkas inte av inställningen [!UICONTROL IP Obfuscation] på datastream-nivå. Adobe Analytics får för närvarande oantastade IP-adresser. För att Analytics ska kunna ta emot dolda IP-adresser måste du konfigurera IP-förfalskning separat i Adobe Analytics. Detta beteende kommer att uppdateras i framtida versioner.<br><br> Mer information om IP-förfalskning och instruktioner om hur du konfigurerar det finns i [dokumentationen för datastream-konfigurationen](../../datastreams/configure.md#advanced-options). |
| [Åsidosättningar av dataströmskonfiguration](../../datastreams/overrides.md) | Nu kan du definiera ytterligare konfigurationsalternativ för datastreams, som du kan använda för att åsidosätta specifika inställningar, som händelsedatamängder, Target-egenskapstoken, ID-synkroniseringsbehållare och rapportsviter för Analytics. <br><br>Åsidosättning av datastream-konfigurationer är en tvåstegsprocess: <ol><li>Först måste du definiera åsidosättningar av datastream-konfigurationen på [datastreams konfigurationssida](../../datastreams/configure.md).</li><li>Sedan måste du skicka åsidosättningarna till Edge Network antingen via ett Web SDK-kommando eller med hjälp av Web SDK [taggtillägg](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).</li></ol> |
| OAuth JWT Secret | Med [OAuth JWT-hemlighet](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) kan kunder använda Adobe- och Google Service-tokens för att ge stöd för server-till-server-interaktioner vid händelsevidarebefordran. |
| [!DNL Pinterest Conversions API]-tillägg | Med tillägget [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) för vidarebefordran av händelser kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka det till [!DNL Pinterest] i form av händelser på serversidan med hjälp av [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya destinationer** {#new-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] anslutning](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Använd Salesforce Marketing Cloud Account Engagement (tidigare Pardot) för att hämta, spåra, poängsätta och betygsätta leads. Använd den här destinationen för B2B-ärenden som omfattar flera avdelningar och beslutsfattare som kräver längre försäljnings- och beslutscykler. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Dataflödesövervakning för [!DNL Custom Personalization] och [!DNL Adobe Commerce] mål | <p> Du kan nu se aktiveringsmått för [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md)-, [anpassade Personalization](../../destinations/catalog/personalization/custom-personalization.md)- och [anpassade Personalization-anslutningar med attribut](../../destinations/catalog/personalization/custom-personalization.md). </p> <p>![Adobe Commerce-bild](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce-mått"){width="100" zoomable="yes"}</p>  Mer information finns i [Övervaka dataflöden på arbetsytan Destinationer](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace). |
| Nytt **[!UICONTROL Append segment ID to segment name]**-fält för [!DNL Google Ad Manager]- och [!DNL Google Ad Manager 360]-mål | <p>Du kan nu ha segmentnamnet i [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) och [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) inkludera segment-ID från Experience Platform, så här: `Segment Name (Segment ID)`.</p><p>![Lägg till bild för segment-ID](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nytt Lägg till segment-ID i segmentnamnsfältet "){width="100" zoomable="yes"}</p> |
| Schemalagda efterfyllningar av målgrupper | <p>För målet [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) planeras aktiveringen av målgruppsåterfyllningar till målet ske 24-48 timmar efter att ett segment först har mappats till en målanslutning. Uppdateringen svarar på Google policy att vänta i 24 timmar tills data har importerats och kommer att förbättra matchningsfrekvensen mellan Real-Time CDP och [!DNL Google Display & Video 360].</p> <p>Observera att detta är en backend-konfiguration som endast gäller för det här målet och som inte har något samband med några schemaläggningsalternativ som kan konfigureras av kunden i användargränssnittet.</p> |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

- Vi har åtgärdat ett problem i **Identiteter exkluderade**-rapporteringsmått för filbaserad målexport. Kunderna fick alla exporterade ID:n från den aktiverade exporten som förväntat. Rapporteringsmåttet **Identiteter som uteslutits** i användargränssnittet visade emellertid felaktigt ett stort antal utelämnade identiteter på grund av felaktigt antal identiteter som aldrig skulle exporteras. (PLAT-149774)
- Vi har åtgärdat ett problem i **schemaläggningssteget** i aktiveringsarbetsflödet. För mål som kräver ett mappnings-ID kunde kunderna inte lägga till ett mappnings-ID för segment som lagts till i befintliga målanslutningar. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Växla visningsnamn | Schemaredigeraren har nu en funktion för att växla mellan de ursprungliga fältnamnen och de mer läsbara visningsnamnen.<br>![Schemaredigeraren med visningsnamnet växlat markerat.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Växla visningsnamn för Schemaredigeraren"){width="100" zoomable="yes"}<br>Tack vare den här flexibiliteten kan du identifiera och redigera dina scheman. Visningsnamnen för standardfältgrupper genereras av systemet men kan vid behov anpassas via användargränssnittet. Läs [visningsnamnet för att växla dokumentation](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) om du vill veta mer. |

{style="table-layout:auto"}

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Schema | [[!UICONTROL Adobe Target Classification Fields]](https://github.com/adobe/xdm/pull/1719/files) | Ett nytt XDM-schema för målklassificeringsdatamängder som innehåller en uppsättning metadatafält för att klassificera Target-aktiviteter och -upplevelser. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [[!UICONTROL Adobe Unified Profile Service Account Union Extension]](https://github.com/adobe/xdm/pull/1696/files) | En fältgrupp för kontotillägg för kundprofil i realtid har lagts till som gör det möjligt för användare att lägga till segmentmedlemskap i en kontounion. |
| Schema | [[!UICONTROL Computed Attributes System Schema]](https://github.com/adobe/xdm/pull/1696/files) | Fältgruppen Beräknade attribut som används av kundprofilen i realtid har uppdaterats till ett skrivskyddat globalt schema. |
| Fältgrupp | Flera | Flera händelser har lagts till som fält för [[!UICONTROL Time-series Schema]](https://github.com/adobe/xdm/pull/1718/files). |
| Fältgrupp | Profilens lojalitetsinformation | [Korrigerade titeln ](https://github.com/adobe/xdm/pull/1717/files) för `xdm:upgradeDate` från &quot;Programnamn&quot; till &quot;Uppgraderingsdatum&quot;. |
| Fältgrupp | Flera | Flera fält från [[!UICONTROL Decision Item]](https://github.com/adobe/xdm/pull/1714/files) har uppdaterats för att ta bort den dubbla kapslade hierarkin. |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Plattform för kunddata i realtid

Plattformen för kunddata i realtid ([!DNL Real-Time CDP]) bygger på Experience Platform och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligenta beslut under hela kundresan. [!DNL Real-Time CDP] kombinerar flera datakällor från företag för att skapa kundprofiler i realtid. Segment som byggs upp utifrån dessa profiler kan sedan skickas till mål i senare led för att ge personliga kundupplevelser i alla kanaler och på alla enheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrad startsida för Real-Time CDP | [Real-Time CDP hemsida](https://experience.adobe.com) har förbättrats med en uppdaterad look och förbättrade prestanda. Hemsidan är nu behörighetsmedveten och visar widgetar som är relevanta för de funktioner du har tillgång till. Mer information finns i översikten [Real-Time CDP hemsidespanel](../../rtcdp/home-page-dashboards.md). |
| Självidentifieringsundersökning | Självidentifieringsundersökningen är ett kort frågeformulär som presenteras på Adobe Experience Platform användargränssnittets hemsida. Använd självidentifieringsundersökningen för att bygga upp din Experience Platform personliga profil och få anpassade riktlinjer baserade på dina val. Mer information finns i [översikten över självidentifieringsundersökningen](../../landing/self-identification.md). |

Mer information om [!DNL Real-Time CDP] finns i [[!DNL Real-Time CDP] översikten](../../rtcdp/overview.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid får du en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online, offline, CRM och data från tredje part. Med profilen kan du konsolidera kunddata till en enhetlig vy som ger en handlingsbar, tidsstämplad redogörelse för varje kundinteraktion.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förfallodatum för pseudonyma profiler | Nu kan pseudonyma profildata förfalla. Den här versionen tar kontinuerligt bort inaktuella pseudonyma profiler från din Experience Platform-instans när den har aktiverats. Om du vill veta mer om funktionen och pseudonyma profiler kan du ta del av [guiden för förfallotid för pseudonyma profilens data](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Segmentmedlemskapskarta | Som en uppföljning till det föregående meddelandet i februari, 15 maj 2023, kommer statusen `Existing` att tas bort från segmentmedlemskartan för att ta bort redundans i segmentmedlemskapets livscykel. Efter den här ändringen representeras profiler som är kvalificerade i ett segment som `Realized` och de profiler som är diskvalificerade fortsätter att representeras som `Exited`.<br/><br/> Den här ändringen kan påverka dig om du använder [företagsmål](../../destinations/destination-types.md#advanced-enterprise-destinations) (Amazon Kinesis, Azure Event Hubs, HTTP API) och kan ha automatiserade processer längre fram i kedjan baserat på statusen `Existing`. Om så är fallet för dig, se över integreringarna i senare led. Om du är intresserad av att identifiera nyligen kvalificerade profiler mer än en viss tid kan du använda en kombination av `Realized`-status och `lastQualificationTime` i din segmentmedlemskarta. Kontakta Adobe om du vill ha mer information. |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service] finns i [segmenteringsöversikten](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| API-stöd för filtrering av radnivådata för Salesforce CRM-källan. | Använd logiska operatorer och jämförelseoperatorer för att filtrera radnivådata för Salesforce CRM-källan. Mer information finns i guiden [om att filtrera data för en källa med API](../../sources/tutorials/api/filter.md). |
| Beta tillgänglighet för Shopify Streaming | [Källan för punktuppspelning](../../sources/connectors/ecommerce/shopify-streaming.md) är nu tillgänglig i betaversionen. Använd Shopify Streaming-källan för att strömma data från ditt Shopify-partnerkonto till Experience Platform. |
| Allmän tillgänglighet för OneTrust-integrering | [OneTrust Integration-källan](../../sources/connectors/consent-and-preferences/onetrust.md) är nu GA. Använd OneTrust Integration-källan för att skicka data om samtycke och inställningar från OneTrust Integration-kontot till Experience Platform. |

{style="table-layout:auto"}

Mer information om källor finns i [översikten över källor](../../sources/home.md).
