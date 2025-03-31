---
title: Versionsinformation om Adobe Experience Platform mars 2025
description: Versionsinformationen för Adobe Experience Platform i mars 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: edcdf84a8cb954c15f7dd235fb14cf14e11e22c8
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 26%

---

# Versionsinformation om Adobe Experience Platform

**Releasedatum: 26 mars 2025**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [Versionsinformation om Adobe Experience Platform](#adobe-experience-platform-release-notes)

   - [Kontrollpaneler](#dashboards)
   - [Mål ](#destinations)
   - [Federerad målgruppssammansättning](#federated-audience-composition)
   - [Segmenteringstjänst](#segmentation-service)
   - [Källor](#sources)

## Kontrollpaneler {#dashboards}

Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Kontrollpanel för mätningsbaserad licensanvändning | Kontrollpanelen för licensanvändning innehåller nu ett strömlinjeformat gränssnitt med två flikar: **Metrics** och **Products**. Den nya fliken **Metrics** ger en samlad vy över alla spårbara licensvärden för alla köpta produkter. Varje mätvärde innehåller en infoikon som visar beskrivningar och tillhörande produkter. Användare kan välja produktions- eller utvecklingssandlådor, visa historiska användningsmönster i interaktiva diagram och exportera sandlådespecifika data som CSV-filer. Uppdateringarna effektiviserar licensspårningen och ger tydligare insikter. Mer information finns i [kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md). |
| Uppdaterad förutsägelsefrekvens | Kontrollpanelen för licensanvändning ger nu mer korrekta insikter om den förväntade förbrukningen genom att uppdatera användningsprognoserna **varje vecka** i stället för varje månad. Prognoserna visar uppskattad användning under de kommande sex veckorna baserat på aktuella trender. Den här förändringen ger snabbare beslutsfattande, tidigare ingripanden och förbättrad licensplanering. Mer information finns i handboken [för kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md#predicted-usage). |
| Uppdaterade måttbeskrivningar i användargränssnittet | Måttdefinitioner i kontrollpanelen för licensanvändning har reviderats för tydlighet och enhetlighet. Du kan nu visa uppdaterade beskrivningar direkt på kontrollpanelen med hjälp av infoikoner bredvid varje mätvärde på fliken **Metrisk**. Uppdateringarna gör det enklare att förstå hur mätvärden spåras och vilka produkter de gäller. Mer information finns i handboken [för kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md#available-metrics). |

{style="table-layout:auto"}

Läs [översikt över kontrollpaneler](../../dashboards/home.md) för mer information om kontrollpaneler, bland annat hur du beviljar åtkomstbehörigheter och skapar anpassade widgetar.

## Mål  {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Beskrivning |
| --- | --- |
| [Anslutning för Demandbase-användare](/help/destinations/catalog/advertising/demandbase-people.md) | Använd anslutningen [!DNL Demandbase People] för att aktivera profiler för dina Demandbase-kampanjer för målgruppsanpassning, personalisering och nedtryckning. |
| [Bombora-kontoanslutning](/help/destinations/catalog/advertising/bombora.md) | Använd [!DNL Bombora]-anslutningen för att aktivera profiler för era Bombora-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på [kontomåldrar](/help/segmentation/types/account-audiences.md). |
| [Uppgradering av luftfartygsattribut](/help/destinations/catalog/mobile-engagement/airship-attributes.md) | Från och med 25 mars 2025 kan du se två **[!UICONTROL Airship Attributes]**-kort sida vid sida i målkatalogen. Detta beror på en intern uppgradering av måltjänsten. Den befintliga **[!UICONTROL Airship Attributes]**-målkopplingen har bytt namn till **[!UICONTROL (Deprecated) Airship Attributes]** och du har nu tillgång till ett nytt kort med namnet **[!UICONTROL Airship Attributes]**. <br> Använd anslutningen **[!UICONTROL Airship Attributes]** i katalogen för nya aktiveringsdataflöden. Om du har aktiva dataflöden till målet [!DNL (Deprecated) Airship Attributes] uppdateras de automatiskt, så ingen åtgärd krävs från dig. <br> Om du skapar dataflöden via [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden: <ul><li> Flödesspecifikation-ID: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> Anslutningsspecifikation-ID: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| [Förbättringar av rapporteringsnoggrannhet för strömningsmål](../../dataflows/ui/monitor-destinations.md) | Från och med mars 2025 lanserar Adobe en uppdatering som ökar rapporteringsnoggrannheten för direktuppspelningsdestinationer. Den här förbättringen ger bättre anpassning mellan rapporteringen i Experience Platform och målplattformarna. <br> Före den här uppdateringen innehöll **[!UICONTROL Identities failed]** alla aktiveringsåterförsök. Efter den här uppdateringen inkluderas endast det senaste aktiveringsåterförsöket i det totala antalet. <br> Den här förbättringen gäller för alla direktuppspelningsmål. <br> Efter den här förbättringen kan användare av direktuppspelningsmål se en förväntad minskning av antalet **[!UICONTROL Identities failed]**. |
| [Fältexportstöd av karttyp för företag och kantmål](/help/destinations/ui/export-arrays-maps-objects.md) | När du exporterar data till [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) och [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) -destinationer kan du nu välja karttypsfält för export i mappningssteget i aktiveringsarbetsflödet. <br> ![Exportera karttypsfält till företagsmål.](../2025/assets/march/export-map.png "Exportera mappningsfält till företagsmål."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Federerad målgruppssammansättning {#federated-audience-composition}

Information om de senaste uppdateringarna för Federated Audience Composition finns i [dedikerad versionsinformation](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes) här.

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar i Audience Builder för konto | I Audience Builder kan du nu filtrera attribut så att de bara visar ifyllda attribut, samt visa sammanfattningsdata för dessa ifyllda attribut. Mer information om de här förbättringarna finns i [Audience Builder](../../rtcdp/segmentation/audience-builder.md) -dokumentationen. |
| Flexibel allmän tillgänglighet för utvärdering av målgrupper | Flexibel utvärdering av målgrupper finns nu i allmänhet att tillgå! Ni kan använda flexibel målgruppsutvärdering för att skapa nya målgrupper på begäran för tidskänslig kommunikation. Mer information om flexibel målgruppsutvärdering finns i den [flexibla översikten över målgruppsutvärderingen](../../segmentation/methods/flexible-audience-evaluation.md). |

Mer information om [!DNL Segmentation Service] finns i [segmenteringsöversikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Nya källor**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Bombora Intent] | Källan [!DNL Bombora Intent] är nu tillgänglig i källkatalogen. Använd den här källan för att: <ul><li>Integrera Bomboras företagsdata för att identifiera konton som aktivt undersöker era produkter eller tjänster.</li><li>Prioritera marknadskonton för att skapa exakta segment och genomföra hyperriktade ABM-kampanjer, vilket säkerställer att era marknadsföringssatsningar fokuserar på de konton som mest sannolikt konverteras.</li><li>Utnyttja intent-drivna strategier för att optimera annonskostnaderna, öka engagemanget och maximera avkastningen.</li></ul> Mer information finns i guiden om att [ansluta ditt [!DNL Bombora] konto till Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md). |
| [!DNL Demandbase Intent] | [!DNL Demandbase Intent]-källan är nu tillgänglig i källkatalogen. Använd den här källan för att: <ul><li>Integrera data för Demandbase:s kontoåtergivning för att identifiera konton med högt intresse som bygger på realtidsengagemang.</li><li>Genom att prioritera de starkaste avsiktssignalerna kan ni skapa exakta segment och leverera målinriktade kampanjer för att säkerställa att era marknadsföringssatsningar fokuserar på konton som mest sannolikt konverteras.</li><li>Aktivera intent-drivna strategier för att optimera annonskostnaderna, öka engagemanget och få högre avkastning.</li></ul> Mer information finns i guiden om att [ansluta ditt [!DNL Demandbase] konto till Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md). |

{style="table-layout:auto"}

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar av [!DNL Google Ads]-källan | Du kan nu använda [[!DNL Google Ads] source](../../sources/connectors/advertising/ads.md) för att importera sammanställningsdata. Du kan använda [!DNL Google Ads Query Builder] för att ange de attribut, segment och resurser som du vill importera till Experience Platform. Mer information finns i guiden om att [ansluta ditt [!DNL Google Ads] konto till Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md). |
| Förbättringar av [!DNL Microsoft Dynamics]-källan | Du kan nu ange primärnyckeln för en angiven [!DNL Microsoft Dynamics]-tabell när du undersöker innehållet och strukturen för dina data. Använd den här funktionen för att optimera dina frågor med källan [!DNL Microsoft Dynamics]. Mer information finns i handboken om att [ansluta [!DNL Microsoft Dynamics] källan till Experience Platform med API:t](../../sources/tutorials/api/create/crm/ms-dynamics.md). |
| Stöd för API-nyckelautentisering i självbetjäningskällor (Batch SDK) | Nu kan du använda API-nyckelautentisering som autentiseringstyp när du integrerar en ny källa med självbetjäningskällor (Batch SDK). Mer information finns i guiden [Konfigurera din autentiseringsspecifikation i Batch SDK](../../sources/sources-sdk/config/authspec.md). |
| Stöd för attributbaserad åtkomstkontroll i källor | Nu kan du använda attributbaserade åtkomstkontrollsfunktioner mot källans dataflöden. Mer information finns i följande handböcker: <ul><li>[Använd etiketter i källans dataflöden med API:t](../../sources/tutorials/api/labels.md)</li><li>[Använd etiketter i källans dataflöden med hjälp av gränssnittet ](../../sources/tutorials/ui/labels.md). |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).
