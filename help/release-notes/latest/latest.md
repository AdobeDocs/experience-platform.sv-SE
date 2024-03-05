---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformationen för Adobe Experience Platform i januari 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 21 februari 2024**

Uppdateringar av befintliga funktioner i Experience Platform:

- [Larm](#alerts)
- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Larm {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika plattformsaktiviteter. Du kan prenumerera på olika varningsregler via [!UICONTROL Alerts] -fliken i användargränssnittet för plattformen och kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.
**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning | 
| --- | --- | 
| Fliken Aviseringshistorik | Som Experience Platform-administratör kan du använda funktionen Hantera aviseringsprenumeranter för att tilldela en avisering till ett Adobe-användar-ID, en extern e-postadress eller en e-postgrupplista. Mer information finns i [dokumentation för varningsgränssnitt](../../observability/alerts/ui.md) om du vill ha mer information om fliken Historik. |

{style="table-layout:auto"}

Läs mer om varningar i [[!DNL Observability Insights] översikt](../../observability/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Stöd för webb-meddelanden i appen i Web SDK](../../web-sdk/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK har nu stöd för konfiguration av Web In-App Messaging för Adobe Journey Optimizer-kampanjer. |

{style="table-layout:auto"}

Läs mer om datainsamlingar i [datainsamling, översikt](../../tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer** {#new-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [Gainsight PX-anslutning](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX är en plattform för produktupplevelser som gör det möjligt för produktteamen att förstå hur användarna använder sina produkter, samla in feedback och skapa interaktioner i appen som produktgenomgångar för att få användarna att komma igång och implementera produkterna. |
| [Anslutning av Mailchimp-taggar](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp är en populär plattform för automatiserad marknadsföring och en e-postmarknadsföringstjänst. Du kan använda kopplingen för Mailchimp-taggar för att strukturera, etikettera eller kategorisera dina kontakter. |
| [SAP Commerce Connection](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce är en molnbaserad e-handelsplattform för B2B- och B2C-företag och finns som en del av SAP:s kundupplevelseportfölj. Du kan använda den här destinationen för att uppdatera kundinformationen inom SAP Commerce från en befintlig Experience Platform-målgrupp. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Aktivera kontomålgrupper som är allmänt tillgängliga | Funktionen för att aktivera kontomaterial för vissa destinationer är nu allmänt tillgänglig för företag som köper [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) och [Personligt arbete](/help/rtcdp/overview.md#rtcdp-b2p) utgåvor av Real-time Customer Data Platform. Läs självstudiekursen om [aktivera kontomålgrupper](/help/destinations/ui/activate-account-audiences.md) för att få fullständig information, inklusive destinationer som stöds. |
| Digital Markets Act Consent Enforcement tools for Google destination | Google släpper ändringar i [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Kundmatchning](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)och [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) för att stödja de krav på efterlevnad och samtycke som anges i [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) i Europeiska unionen ([Policy för EU-användarsamtycke](https://www.google.com/about/company/user-consent-policy/)). Tillämpningen av dessa ändringar i medgivandekraven förväntas träda i kraft från och med den 6 mars 2024. <br/><br/> För att kunna följa EU:s policy för användargodkännande och fortsätta att skapa målgruppslistor för användare i Europeiska ekonomiska samarbetsområdet (EES) måste annonsörer och partners se till att slutanvändarnas samtycke skickas när målgruppsdata överförs. Som Google-partner tillhandahåller Adobe de verktyg som krävs för att uppfylla dessa krav på medgivande enligt DMA i Europeiska unionen.<br/><br/>Kunder som har köpt skölden för skydd och säkerhet av Adobe och konfigurerat en [samtyckespolicy](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) om du vill filtrera bort profiler som inte är godkända behöver du inte göra något.<br/><br/>Kunder som inte har köpt Adobe Privacy &amp; Security Shield måste använda [segmentdefinition](../../segmentation/home.md#segment-definitions) funktioner inom [Segment Builder](../../segmentation/ui/segment-builder.md) för att filtrera bort profiler som inte godkänts, så att du kan fortsätta använda Real-Time CDP Google-destinationer utan avbrott. |
| [!BADGE Beta]{type=Informative} Ändra ordning på mappningsfält för batchmål | Du kan nu ändra ordningen på kolumnerna i CSV-exporter genom att dra och släppa mappningsfälten i [mappning](../../destinations/ui/activate-batch-profile-destinations.md#mapping) steg. Ordningen på de mappade fälten i användargränssnittet återspeglas i ordningen på kolumnerna i den exporterade CSV-filen, uppifrån och ned, där den översta raden är den vänstra kolumnen i CSV-filen. <br/><br/> Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen. |
| [!BADGE Beta]{type=Informative} Förvalt standardexportschema för batchmål | Experience Platform anger nu automatiskt ett standardschema för varje filexport. Läs dokumentationen om [schemalägga målgruppsexport](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) om du vill lära dig hur du ändrar standardschemat. <br/><br/> Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen. |
| [!BADGE Beta]{type=Informative} Redigera målgruppsaktiveringsplaner gruppsmål gruppvis | Du kan nu redigera aktiveringsschemat för flera målgrupper samtidigt från [Aktiveringsdata](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) sida. <br/><br/> Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen. |
| [!BADGE Beta]{type=Informative} Massexportera filer on-demand till batchmål | Du kan nu exportera målgrupper i grupp till gruppmål via [exportera filer on demand](../../destinations/ui/export-file-now.md) funktionalitet. <br/><br/> Den här funktionen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få tillgång till den här funktionen. |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Verktyg i sandlådan | Förutom att nu ha stöd för objekttyper för samtycke och styrningsregler kan du använda sandlådeverktyg för att importera scheman utan att ha enhetliga profiler aktiverade, söka efter saknade attribut i målsandlådan när du importerar ett segment och använda den befintliga sammanfogningsprincipen som standard. Mer information om de här funktionerna finns i [gränssnittshandbok för sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikt över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] gör att du kan segmentera data som lagras i [!DNL Experience Platform] som rör enskilda (t.ex. kunder, prospects, användare eller organisationer) till målgrupper. Du kan skapa målgrupper genom segmentdefinitioner eller andra källor från [!DNL Real-Time Customer Profile] data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform]och är lätt tillgängliga för alla Adobe-lösningar.

**Ny funktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Målgrupper | Målgrupper finns nu att tillgå generellt! Nu kan ni använda kontosegmentering för att göra marknadsföringssegmenteringen från personbaserade målgrupper mer enkel och avancerad till kontobaserade målgrupper i både B2B- och B2P-utgåvorna av kundplattformen i realtid. I den här versionen kan ni använda personbaserade målgrupper som predikat för kontobaserade målgrupper, lägga till sökfunktioner, stödja användningen av anpassade entiteter och följa datastyrning. Mer information om den här funktionen finns i [kontomålgrupper - översikt](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] källa | Använd [[!DNL Acxiom Prospecting Data Import] källa](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) hämta och mappa data från [!DNL Acxiom] service till Experience Platform. |

{style="table-layout:auto"}

Mer information om källor finns i [källöversikt](../../sources/home.md).
