---
title: Versionsinformation om Adobe Experience Platform april 2023
description: Versionsinformation från april 2023 för Adobe Experience Platform.
exl-id: 7b501467-99a7-4aee-ae86-66c851250ecf
source-git-commit: 5de1ec17b78c97be21c0d2afd6f0b119a6074b6f
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

>[!IMPORTANT]
>
>Från 15 maj 2023 `Existing` status tas bort från segmentmedlemskartan för att ta bort redundans i segmentmedlemskapets livscykel. Efter den här ändringen representeras profiler som är kvalificerade i ett segment som `Realized` och de diskvalificerade profilerna kommer även fortsättningsvis att representeras som `Exited`. Mer information om den här ändringen finns i [Segmenteringstjänstavsnitt](#segmentation).

**Releasedatum: 26 april 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Dataförberedelse](#data-prep)
- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Experience Data Model](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner** {#dashboards-new-updated-features}

| Funktion | Beskrivning |
| --- | --- |
| Användardefinierade kontrollpaneler | Nu kan du **filtrera historiska data** utifrån widgetens insikter och använd antingen senaste data eller en anpassad analysperiod. Se [användardefinierad handbok för kontrollpaneler](../../dashboards/user-defined-dashboards.md#filter-historical-data) för mer information.<br>Du kan också göra det nu **duplicera dina befintliga widgetar**. Genom att anpassa en dubblett och redigera deras attribut kan du undvika att starta om från början när du skapar en ny, unik widget. Läs [guide för duplicering av widget](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) om du vill veta mer. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikt över instrumentpaneler](../../dashboards/home.md).

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av bakåtfyllnadsperiod för Adobe Analytics i icke-produktionssandlådor | Förifyllningsperioden för Adobe Analytics i icke-produktionssandlådor har reducerats till tre månader. Backfill för produktionssandlådor är desamma vid 13 månader. Den här ändringen gäller endast för nya flöden och påverkar inte befintliga flöden. Mer information finns i [Adobe Analytics - översikt](../../sources/connectors/adobe-applications/analytics.md). |
| Ny mappningsfunktion som konverterar FPID-strängar till ECID | Använd `fpid_to_ecid` funktion för att konvertera FPID-strängar till ECID för användning i Experience Platform och Experience Cloud. Mer information finns i [Handbok för dataprefixfunktioner](../../data-prep/functions.md). |

{style="table-layout:auto"}

Mer information om Data Prep finns i [Översikt över datapreflight](../../data-prep/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| IP-adressofuscation för datastreams | Nu kan du definiera IP-obfusionsalternativ på hel- eller partiell datastream-nivå i [användargränssnitt för konfiguration av datastream](../../datastreams/configure.md). <br><br>Inställningen för IP-förfalskning på datastream-nivå har företräde framför IP-förfalskning som har konfigurerats i Adobe Target och Audience Manager. <br><br>Data som skickas till Adobe Analytics påverkas inte av datastream-nivån [!UICONTROL IP Obfuscation] inställning. Adobe Analytics får för närvarande oantastade IP-adresser. För att Analytics ska kunna ta emot dolda IP-adresser måste du konfigurera IP-förfalskning separat i Adobe Analytics. Detta beteende kommer att uppdateras i framtida versioner.<br><br> Mer information om IP-förfalskning och instruktioner om hur du konfigurerar den finns i [konfigurationsdokumentation för datastream](../../datastreams/configure.md#advanced-options). |
| [Åsidosättningar av dataströmskonfiguration](../../datastreams/overrides.md) | Nu kan du definiera ytterligare konfigurationsalternativ för datastreams, som du kan använda för att åsidosätta specifika inställningar, som händelsedatamängder, Target-egenskapstoken, ID-synkroniseringsbehållare och rapportsviter för Analytics. <br><br>Att åsidosätta datastream-konfigurationer är en tvåstegsprocess: <ol><li>Först måste du definiera åsidosättningar av dataströmskonfigurationer i [konfigurationssida för datastream](../../datastreams/configure.md).</li><li>Sedan måste du skicka åsidosättningarna till Edge Network antingen via ett Web SDK-kommando eller via Web SDK [taggtillägg](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).</li></ol> |
| OAuth JWT Secret | The [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) gör att kunder kan använda Adobe och Google Service Token för att stödja interaktioner mellan server och server vid händelsevidarebefordran. |
| [!DNL Pinterest Conversions API] extension | The [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) tillägg för händelsevidarebefordran gör att du kan utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Pinterest] i form av händelser på serversidan med [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer** {#new-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] anslutning](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Använd Salesforce Marketing Cloud Account Engagement (tidigare Pardot) för att hämta, spåra, poängsätta och betygsätta leads. Använd den här destinationen för B2B-ärenden som omfattar flera avdelningar och beslutsfattare som kräver längre försäljnings- och beslutscykler. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Dataflödesövervakning för [!DNL Custom Personalization] och [!DNL Adobe Commerce] mål | <p> Nu kan du se aktiveringsstatistik för [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Anpassad personalisering](../../destinations/catalog/personalization/custom-personalization.md) och [Anpassad personalisering med attribut](../../destinations/catalog/personalization/custom-personalization.md) anslutningar. </p> <p>![Adobe Commerce, bild](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce metrics"){width="100" zoomable="yes"}</p>  Se [Övervaka dataflöden på arbetsytan Destinationer](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) för mer information. |
| Nytt **[!UICONTROL Append segment ID to segment name]** fält för [!DNL Google Ad Manager] och [!DNL Google Ad Manager 360] mål | <p>Nu kan du ha segmentnamnet i [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) och [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) inkludera segment-ID från Experience Platform, så här: `Segment Name (Segment ID)`.</p><p>![Lägg till bild för segment-ID](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nytt Lägg till segment-ID till segmentnamnsfält "){width="100" zoomable="yes"}</p> |
| Schemalagda efterfyllningar av målgrupper | <p>För [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) är aktiveringen av målgruppens efterfyllningar till målet planerad till 24-48 timmar efter att ett segment först har mappats till en målanslutning. Uppdateringen svarar på Google policy att vänta i 24 timmar tills data har importerats och kommer att förbättra matchningsfrekvensen mellan Real-Time CDP och [!DNL Google Display & Video 360].</p> <p>Observera att detta är en backend-konfiguration som endast gäller för det här målet och som inte har något samband med några schemaläggningsalternativ som kan konfigureras av kunden i användargränssnittet.</p> |

{style="table-layout:auto"}

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

- Vi har åtgärdat ett problem i **Undantagna identiteter** rapportmått för filbaserad destinationsexport. Kunderna fick alla exporterade ID:n från den aktiverade exporten som förväntat. Men **Undantagna identiteter** rapportmåttet i användargränssnittet visade felaktigt ett stort antal utelämnade identiteter på grund av felaktigt antal identiteter som aldrig skulle exporteras. (PLAT-149774)
- Vi har åtgärdat ett problem i **Schemaläggning** steg i aktiveringsarbetsflödet. För mål som kräver ett mappnings-ID kunde kunderna inte lägga till ett mappnings-ID för segment som lagts till i befintliga målanslutningar. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Växla visningsnamn | Schemaredigeraren har nu en funktion för att växla mellan de ursprungliga fältnamnen och de mer läsbara visningsnamnen.<br>![Schemaredigeraren med växlingsknappen för visningsnamn markerad.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Växla mellan visningsnamn för Schemaredigeraren"){width="100" zoomable="yes"}<br>Tack vare den här flexibiliteten blir det enklare att hitta och redigera dina scheman. Visningsnamnen för standardfältgrupper genereras av systemet men kan vid behov anpassas via användargränssnittet. Läs [visa namnväxlingsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) om du vill veta mer. |

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
| Fältgrupp | Profilens lojalitetsinformation | [Titeln har åtgärdats](https://github.com/adobe/xdm/pull/1717/files) for `xdm:upgradeDate` från&quot;Programnamn&quot; till&quot;Uppgraderingsdatum&quot;. |
| Fältgrupp | Flera | Flera fält från [[!UICONTROL Decision Item]](https://github.com/adobe/xdm/pull/1714/files) har uppdaterats för att ta bort den dubbla kapslade hierarkin. |

{style="table-layout:auto"}

Mer information om XDM in Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Real-Time Customer Data Platform

Built on Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. [!DNL Real-Time CDP] kombinerar flera datakällor för företag för att skapa kundprofiler i realtid. Segment som byggts utifrån dessa profiler kan sedan skickas till efterföljande destinationer för att tillhandahålla personliga kundupplevelser i alla kanaler och enheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrad startsida för Real-Time CDP | The [Real-Time CDP hemsida](https://experience.adobe.com) har förbättrats med en uppdaterad stil och förbättrade prestanda. Hemsidan är nu behörighetsmedveten och visar widgetar som är relevanta för de funktioner du har tillgång till. Mer information finns i [Översikt över kontrollpanelen för Real-Time CDP hemsida](../../rtcdp/home-page-dashboards.md). |
| Självidentifieringsundersökning | Självidentifieringsundersökningen är ett kort frågeformulär som presenteras på Adobe Experience Platform användargränssnittets hemsida. Använd självidentifieringsundersökningen för att bygga upp din personliga profil för Experience Platform och få anpassade riktlinjer baserade på dina val. Mer information finns i [översikt över självidentifieringsundersökning](../../landing/self-identification.md). |

Mer information om [!DNL Real-Time CDP], se [[!DNL Real-Time CDP] översikt](../../rtcdp/overview.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förfallodatum för pseudonyma profiler | Nu kan pseudonyma profildata förfalla. Den här versionen tar kontinuerligt bort inaktuella pseudonyma profiler från din Experience Platform-instans när den har aktiverats. Läs mer om den här funktionen och pseudonyma profiler i [Förfalloguide för pseudonyma profildata](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Segmentmedlemskapskarta | Som en uppföljning av det föregående meddelandet i februari den 15 maj 2023 `Existing` status tas bort från segmentmedlemskartan för att ta bort redundans i segmentmedlemskapets livscykel. Efter den här ändringen representeras profiler som är kvalificerade i ett segment som `Realized` och de diskvalificerade profilerna kommer även fortsättningsvis att representeras som `Exited`.<br/><br/> Den här förändringen kan påverka dig om du använder [företagsmål](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) och kan ha automatiserade processer längre fram i kedjan baserat på `Existing` status. Om så är fallet för dig, se över integreringarna i senare led. Om du är intresserad av att identifiera nyligen kvalificerade profiler längre än en viss tid, vänligen väl använda en kombination av `Realized` status och `lastQualificationTime` i er medlemskarta för segment. Mer information får du av Adobe. |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service], se [Översikt över segment](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| API-stöd för filtrering av radnivådata för Salesforce CRM-källan. | Använd logiska operatorer och jämförelseoperatorer för att filtrera radnivådata för Salesforce CRM-källan. Läs guiden på [filtrera data för en källa med API](../../sources/tutorials/api/filter.md) för mer information. |
| Betaversion av Shopify Streaming | The [Förminska strömningskälla](../../sources/connectors/ecommerce/shopify-streaming.md) finns nu i betaversion. Använd Shopify Streaming-källan för att strömma data från ditt Shopify-partnerkonto till Experience Platform. |
| Allmän tillgänglighet för OneTrust-integrering | The [OneTrust Integration-källa](../../sources/connectors/consent-and-preferences/onetrust.md) är nu GA. Använd OneTrust Integration-källan för att skicka data om samtycke och inställningar från OneTrust Integration-kontot till Experience Platform. |
| Allmän tillgänglighet för Oracle Service Cloud | The [Oracle Service Cloud-källa](../../sources/connectors/customer-success/oracle-service-cloud.md) är nu GA. Använd Oraclets Service Cloud-källa för att skicka Oracle Service Cloud-data till Experience Platform. |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).
