---
title: Versionsinformation om Adobe Experience Platform april 2023
description: Versionsinformation från april 2023 för Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 7c4bdee9f8599e27ffab776c4df5083d2e29e26c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 april 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Dataförberedelse](#data-prep)
- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Experience Data Model](#xdm)
- [Kundprofil i realtid](#profile)
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
| IP-adressofuscation för datastreams | Nu kan du definiera IP-obfusionsalternativ på hel- eller partiell datastream-nivå i [användargränssnitt för konfiguration av datastream](../../edge/datastreams/configure.md). <br><br>Inställningen för IP-förfalskning på datastream-nivå har företräde framför IP-förfalskning som har konfigurerats i Adobe Target och Audience Manager. <br><br>Data som skickas till Adobe Analytics påverkas inte av datastream-nivån [!UICONTROL IP Obfuscation] inställning. Adobe Analytics får för närvarande oantastade IP-adresser. För att Analytics ska kunna ta emot dolda IP-adresser måste du konfigurera IP-förfalskning separat i Adobe Analytics. Detta beteende kommer att uppdateras i framtida versioner.<br><br> Mer information om IP-förfalskning och instruktioner om hur du konfigurerar den finns i [konfigurationsdokumentation för datastream](../../edge/datastreams/configure.md#advanced-options). |
| [Åsidosättningar av dataströmskonfiguration](../../edge/datastreams/overrides.md) | Nu kan du definiera ytterligare konfigurationsalternativ för datastreams, som du kan använda för att åsidosätta specifika inställningar, som händelsedatamängder, Target-egenskapstoken, ID-synkroniseringsbehållare och rapportsviter för Analytics. <br><br>Att åsidosätta datastream-konfigurationer är en tvåstegsprocess: <ol><li>Först måste du definiera åsidosättningar av dataströmskonfigurationer i [konfigurationssida för datastream](../../edge/datastreams/configure.md).</li><li>Sedan måste du skicka åsidosättningarna till Edge Network antingen via ett Web SDK-kommando eller via Web SDK [taggtillägg](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |

{style="table-layout:auto"}

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer** {#new-destinations}

| Destination | Beskrivning |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] anslutning](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Använd Salesforce Marketing Cloud Account Engagement (tidigare Pardot) för att hämta, spåra, poängsätta och betygsätta leads. Använd den här destinationen för B2B-ärenden som omfattar flera avdelningar och beslutsfattare som kräver längre försäljnings- och beslutscykler. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Dataflödesövervakning för [!DNL Custom Personalization] och [!DNL Adobe Commerce] mål | <p> Nu kan du se aktiveringsstatistik för [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Anpassad personalisering](../../destinations/catalog/personalization/custom-personalization.md) och [Anpassad personalisering med attribut](../../destinations/catalog/personalization/custom-personalization.md) anslutningar. </p> <p>![Adobe Commerce, bild](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce metrics"){width="100" zoomable="yes"}</p>  Se [Övervaka dataflöden på arbetsytan Destinationer](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) för mer information. |
| Nytt **[!UICONTROL Append segment ID to segment name]** fält för [!DNL Google Ad Manager] och [!DNL Google Ad Manager 360] mål | <p>Nu kan du ha segmentnamnet i [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) och [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) inkludera segment-ID från Experience Platform, så här: `Segment Name (Segment ID)`.</p><p>![Lägg till bild för segment-ID](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nytt Lägg till segment-ID till segmentnamnsfält "){width="100" zoomable="yes"}</p> |
| Schemalagda efterfyllningar av målgrupper | <p>För [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) är aktiveringen av målgruppens efterfyllningar till målet planerad till 24-48 timmar efter att ett segment först har mappats till en målanslutning. Uppdateringen är ett svar på Google policy att vänta i 24 timmar tills data har importerats och kommer att förbättra matchningsfrekvensen mellan realtidskodskiften och [!DNL Google Display & Video 360].</p> <p>Observera att detta är en backend-konfiguration som endast gäller för det här målet och som inte har något samband med några schemaläggningsalternativ som kan konfigureras av kunden i användargränssnittet.</p> |

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

Mer information om XDM in Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förfallodatum för pseudonyma profiler | Nu kan pseudonyma profildata förfalla. Den här versionen tar kontinuerligt bort inaktuella pseudonyma profiler från din Experience Platform-instans när den har aktiverats. Läs mer om den här funktionen och pseudonyma profiler i [Förfalloguide för pseudonyma profildata](../../profile/pseudonymous-profiles.md). |

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| API-stöd för filtrering av radnivådata för Microsoft Dynamics, Salesforce CRM och Salesforce Marketing Cloud | Använd logiska operatorer och jämförelseoperatorer för att filtrera radnivådata för källorna i Microsoft Dynamics, Salesforce CRM och Salesforce Marketing Cloud. Läs guiden på [filtrera data för en källa med API](../../sources/tutorials/api/filter.md) för mer information. |
| Betaversion av Shopify Streaming | The [Förminska strömningskälla](../../sources/connectors/ecommerce/shopify-streaming.md) finns nu i betaversion. Använd Shopify Streaming-källan för att strömma data från ditt Shopify-partnerkonto till Experience Platform. |
| Allmän tillgänglighet för OneTrust-integrering | The [OneTrust Integration-källa](../../sources/connectors/consent-and-preferences/onetrust.md) är nu GA. Använd OneTrust Integration-källan för att skicka data om samtycke och inställningar från OneTrust Integration-kontot till Experience Platform. |
| Allmän tillgänglighet för Oracle Service Cloud | The [Oracle Service Cloud-källa](../../sources/connectors/customer-success/oracle-service-cloud.md) är nu GA. Använd Oraclets Service Cloud-källa för att skicka Oracle Service Cloud-data till Experience Platform. |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).
