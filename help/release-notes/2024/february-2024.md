---
title: Versionsinformation om Adobe Experience Platform – februari 2024
description: Versionsinformationen för Adobe Experience Platform från februari 2024.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: ht
source-wordcount: '1237'
ht-degree: 100%

---

# Versionsinformation om Adobe Experience Platform

**Releasedatum: 21 februari 2024**

Uppdateringar av befintliga funktioner i Experience Platform:

- [Aviseringar](#alerts)
- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Fliken Aviseringshistorik | Som Experience Platform-administratör kan du använda funktionen Hantera aviseringsprenumeranter för att tilldela en avisering till ett Adobe-användar-ID, en extern e-postadress eller en mailinglista. Mer information om historikfliken finns i [dokumentationen för användargränssnittet för aviseringar](../../observability/alerts/ui.md). |

{style="table-layout:auto"}

Läs [[!DNL Observability Insights] översikten](../../observability/home.md) om du vill veta mer om aviseringar.

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Stöd för webbmeddelanden i appen i Web SDK](../../web-sdk/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK har nu stöd för konfiguration av webbmeddelanden i appen för Adobe Journey Optimizer-kampanjer. |

{style="table-layout:auto"}

Mer information om datainsamlingar finns i [översikten över datainsamlingar](../../tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## Mål  {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya destinationer** {#new-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [Gainsight PX-anslutning](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX är en plattform för produktupplevelser som gör det möjligt för produktteam att förstå hur användarna använder deras produkter, samla in feedback och skapa interaktioner i appen, t.ex. produktgenomgångar, för att få användarna att komma igång och börja använda produkterna. |
| [Mailchimp Tags-anslutning](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp är en populär plattform för automatiserad marknadsföring och en e-postmarknadsföringstjänst. Du kan använda Mailchimp Tags-anslutningen för att strukturera, märka eller kategorisera dina kontakter. |
| [SAP Commerce-anslutning](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce är en molnbaserad e-handelsplattform för B2B- och B2C-företag och är tillgänglig som en del av SAP:s kundupplevelseportfölj. Du kan använda den här destinationen för att uppdatera kundinformationen inom SAP Commerce från en befintlig Experience Platform-målgrupp. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Aktivera kontomålgrupper är allmänt tillgänglig | Funktionen för att aktivera kontomålgrupper för vissa destinationer är nu allmänt tillgänglig för företag som köper utgåvorna [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) och [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) av Real-time Customer Data Platform. Läs självstudiekursen om [att aktivera kontomålgrupper](/help/destinations/ui/activate-account-audiences.md) för att få fullständig information, inklusive vilka destinationer som stöds. |
| Verktyg för verkställande av medgivande enligt Digital Markets Act för Google-destinationer | Google släpper ändringar i [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) och [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) för att stödja de kompatibilitetskrav och medgivanderrelaterade krav som definieras i [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) i EU ([policy för användarmedgivande inom EU](https://www.google.com/about/company/user-consent-policy/)). Tillämpningen av dessa ändringar i medgivandekraven förväntas träda i kraft från och med den 6 mars 2024. <br/><br/> För att kunna följa policyn om användarmedgivande i EU och fortsätta skapa målgruppslistor för användare i Europeiska ekonomiska samarbetsområdet (EES) måste annonsörer och partner se till att de får slutanvändarnas medgivande när de laddar upp målgruppsdata. Som Google-partner tillhandahåller Adobe verktygen som krävs för att uppfylla dessa krav på medgivande enligt DMA i Europeiska unionen.<br/><br/>Kunder som har köpt Adobe Privacy &amp; Security Shield och konfigurerat en [medgivandeprincip](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för att filtrera bort profiler som inte har gett sitt medgivande behöver inte vidta några åtgärder.<br/><br/>Kunder som inte har köpt Adobe Privacy &amp; Security Shield måste använda funktionerna för [segmentdefinition](../../segmentation/home.md#segment-definitions) i [Segment Builder](../../segmentation/ui/segment-builder.md) för att filtrera bort profiler som inte har gett sitt medgivande, så att de kan fortsätta använda de befintliga Real-Time CDP Google-destinationerna utan avbrott. |
| [!BADGE Beta]{type=Informative} Ordna om mappningsfält för gruppdestinationer | Du kan nu ändra ordningen på kolumnerna i CSV-exporter genom att dra och släppa mappningsfälten i [mappningssteget](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Ordningen på de mappade fälten i användargränssnittet återspeglas i ordningen på kolumnerna i den exporterade CSV-filen, uppifrån och ned, där den översta raden är den vänstra kolumnen i CSV-filen. <br/><br/> Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen. |
| [!BADGE Beta]{type=Informative} Förvalda standardscheman för export för gruppdestinationer | Experience Platform anger nu automatiskt ett standardschema för varje filexport. Mer information om hur du ändrar standardplanen finns i dokumentationen om [att planera målgruppsexporter](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). <br/><br/> Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen. |
| [!BADGE Beta]{type=Informative} Massredigera målgruppsaktiveringsscheman för gruppdestinationer | Du kan nu redigera aktiveringplanen för flera målgrupper samtidigt på sidan [Aktiveringsdata](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). <br/><br/> Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen. |
| [!BADGE Beta]{type=Informative} Massexportera filer på begäran till gruppdestinationer | Du kan nu massexportera målgrupper till gruppdestionationer med funktionen [Exportera filer på begäran](../../destinations/ui/export-file-now.md). <br/><br/> Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen. |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [översikten över destinationer](../../destinations/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose det här behovet tillhandahåller Experience Platform sandlådor som partitionerar en enda Experience Platform-instans i separata virtuella miljöer för att utveckla och förbättra program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Verktyg i sandlådan | Förutom att nu ha stöd för objekttyper för medgivande och förvaltningsregler kan du använda verktyg i sandllådan för att importera planer utan aktiverade enhetliga profiler, söka efter saknade attribut i målsandlådan när du importerar ett segment och använda den befintliga sammanfogningsprincipen som standard. Mer information om de här funktionerna finns i [guiden om användargränssnittet för verktyg i sandlådan](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation}

Med [!DNL Segmentation Service] kan du segmentera data som lagras i [!DNL Experience Platform] och som relaterar till individer (t.ex. kunder, potentiella kunder, användare eller organisationer) till målgrupper. Du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Experience Platform] och är tillgängliga för alla Adobe-lösningar.

**Ny funktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Kontomålgrupper | Kontomålgrupper är nu allmänt tillgängliga! Du kan nu använda kontosegmentering för att förenkla och förbättra marknadsföringssegmenteringen från personbaserade målgrupper till kontobaserade målgrupper i både B2B- och B2P-utgåvorna av Real-Time Customer Experience Platform. I den här versionen kan du använda personbaserade målgrupper som en grund för kontobaserade målgrupper, lägga till sökfunktioner, stödja användningen av anpassade entiteter och säkerställa dataförvaltning. Mer information om den här funktionen finns i [översikten över kontomålgrupper](../../segmentation/types/account-audiences.md). |

{style="table-layout:auto"}

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom]-källa | Använd [[!DNL Acxiom Prospecting Data Import] källan](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) för att hämta och mappa data från den potentiella kundtjänsten [!DNL Acxiom] till Experience Platform. |

{style="table-layout:auto"}

Mer information om källor finns i [översikten över källor](../../sources/home.md).
