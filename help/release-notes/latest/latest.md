---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation juli 2023 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: d639b0830b88307b249e7da232b3f48b142ad37b
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 juli 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Katalogtjänst](#catalog-service)
- [Datainsamling](#data-collection)
- [Dataförberedelse](#data-prep)
- [Mål ](#destinations)
- [Frågetjänst](#query-service)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)
- [Experience Data Model (XDM)](#xdm)

## Katalogtjänst {#catalog-service}

Katalogtjänsten är arkivsystemet för dataplatser och -länkar inom Adobe Experience Platform. Alla data som importeras till Experience Platform lagras i Data Lake som filer och kataloger, men i Catalog finns metadata och beskrivning för dessa filer och kataloger för sökning och övervakning.

| Funktion | Beskrivning |
| --- | --- |
| Inventeringshantering för datauppsättning | Användargränssnittet för datauppsättningar erbjuder nu en samling infogade åtgärder för att hantera dina datauppsättningar bättre. Avancerad datauppsättningshantering förbättrar arbetseffektiviteten genom att man skapar och tilldelar mappar och taggar till datauppsättningar, vilket möjliggör filtrering och förbättrad identifiering. Mer information om [infogade funktionsmakron](../../catalog/datasets/user-guide.md#inline-actions), hur [sök- och filterdatauppsättningar](../../catalog/datasets/user-guide.md#search-and-filter)och [flytta datauppsättningar till mappar](../../catalog/datasets/user-guide.md#move-to-folders). |

{style="table-layout:auto"}

Mer information om katalogtjänsten finns i [Katalogtjänst - översikt](../../catalog/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Taggar och händelsevidarebefordran | Granskningsloggar för datainsamling | Du kan nu se när en åtgärd utfördes och vem som utförde den här åtgärden över taggar och händelsevidarebefordran. Detta underlättar felsökning, korrekt styrning och intern revision. Dessa granskningsdata visas via snabbmenyer för utskjutning som även innehåller snabbåtgärder och statusuppdateringar för resurser. Dessa data visas i gränssnittet Taggar och Händelsevidarebefordran på följande skärmar:<br><ul><li>[Egenskapsöversikt](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[Regler](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[Dataelement](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[Tillägg](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[Biblioteksgranskning](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[Biblioteket skapades och publicerades senast](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| Dataströmmar | [Geo-sökning](../../datastreams/configure.md#advanced-options) | Nu kan du konfigurera geopositionering och nätverkssökning för datastreams så att den inkluderar information som: <ul><li>Land</li><li>Postnummer</li><li>Stat/provins</li><li>DMA</li><li>Ort</li><li>Latitud </li><li>Longitud</li><li>Fraktfirma</li><li>Domän</li><li>ISP</li></ul> Du ansvarar för att säkerställa att du har fått alla tillstånd, samtycke, klargöranden och tillstånd som krävs enligt tillämpliga lagar och bestämmelser för att samla in, bearbeta och överföra personuppgifter, inklusive exakt geolokaliseringsinformation. <br> Ditt val av IP-adressofuscation påverkar inte nivån på geopositioneringsinformation som kommer att härledas från IP-adressen och skickas till dina konfigurerade Adobe-lösningar. Geoplatssökningar måste begränsas eller inaktiveras separat. <br> Se [datastreams-dokumentation](../../datastreams/configure.md#advanced-options) för mer information. |

{style="table-layout:auto"}

Mer information om datainsamling finns i [datainsamling, översikt](../../tags/home.md).

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya mappningsfunktioner | Du kan nu använda följande funktioner när du mappar objekt i Data Prep: <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> Mer information om dessa funktioner finns i [Handbok för dataprefixfunktioner](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

Mer information om Data Prep finns i [Översikt över datapreflight](../../data-prep/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade destinationer** {#new-updated-destinations}

| Destination | Nytt eller uppdaterat | Beskrivning |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | Nytt | Införliva identiteter från Adobe Experience Platform i [!DNL LiveRamp Connect] så att ni kan inrikta er på användare på mobilen, öppna webben, sociala medier och [!DNL CTV] plattformar, använda [!DNL Ramp ID] identifierare. |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Nytt | Skapa en utgående liveanslutning till [!DNL Azure Data Lake Storage Gen2] att regelbundet exportera datafiler från Adobe Experience Platform till din egen lagringsplats. Det nya målet har förbättrad filexportfunktion och stöd för [!BADGE Beta]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Nytt | [!DNL Data Landing Zone] är en [!DNL Azure Blob] lagringsgränssnittet som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att exportera filer från plattformar. Det nya målet har förbättrad filexportfunktion och stöd för [!BADGE Beta]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Nytt | Skapa en utgående liveanslutning till [!DNL Google Cloud Storage] att regelbundet exportera datafiler från Adobe Experience Platform till era egna. Det nya målet har förbättrad filexportfunktion och stöd för [!BADGE Beta]{type=Informative} |
| [[!DNL Amazon S3] update](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Uppdaterat | Med den här uppdateringen har målet förbättrad filexportfunktion och stöd för [!BADGE Beta]{type=Informative} |
| [[!DNL Azure Blob] update](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Uppdaterat | Med den här uppdateringen har målet förbättrad filexportfunktion och stöd för [!BADGE Beta]{type=Informative} |
| [[!DNL SFTP] update](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Uppdaterat | Med den här uppdateringen har målet förbättrad filexportfunktion och stöd för [!BADGE Beta]{type=Informative} |
| [[!DNL Adobe Campaign Managed Services] anslutning](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Uppdaterat | The [!DNL Adobe Campaign Managed Services] integrering med Adobe Experience Platform har nu stöd för olika typer av målgruppssynkronisering. Använd kontrollen Välj synkroniseringstyp för att avgöra om du ska exportera målgrupper till Adobe Campaign eller målgrupper och deras profilattribut. <br> ![Ny Välj synkroniseringstypsväljare är markerad.](/help/release-notes/2023/assets/acms-destination-export-type.png "Ny Välj synkroniseringstypsväljare är markerad."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

Uppdateringen och den allmänna tillgänglighetsreleasen av de sex molnlagringsmålen ovan innehåller följande funktionalitet:

- Ytterligare [filnamnsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
- Möjlighet att ange anpassade filhuvuden i de exporterade filerna via [förbättrat mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- Möjlighet att anpassa [formatering av exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Beta]{type=Informative}[Stöd för dataexport](/help/destinations/ui/export-datasets.md).


**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

- Vi har åtgärdat ett problem med (API) Salesforce Marketing Cloud-målet där inte alla tillgängliga målattribut returnerades från Salesforce i mappningssteget. Det finns nu en [övre gräns på 2000 målattribut](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) från Salesforce som kan visas.
- Ett problem med Microsoft Dynamics 365-destinationen har korrigerats. Målet har nu stöd för regional routning av data via [Regionväljare](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate)så att ni kan dirigera dataexporter beroende på vilken region ert företag är etablerat i inom Microsoft ekosystem. <br> ![Ny områdesväljare markerad.](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "Ny områdesväljare markerad."){width="100" zoomable="yes"}

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga efter data i Adobe Experience Platform datasjön. Du kan ansluta alla datauppsättningar från datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas i rapporter, Data Science Workspace eller för att matas in i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrad frågeredigerare | Den förbättrade frågeredigeraren ger bättre tillgänglighet och stöd för flera teman. Förbättrade redigeringsinställningar gör att du kan aktivera mörka eller ljusa teman. Se [dokumentation](../../query-service/ui/user-guide.md#enhanced-editor-toggle) för mer information. |
| Aliasnamn för beräknad statistik | Du kan nu ange ett aliasnamn som beskriver resultatet av dina beräkningar i SQL-frågor. I dokumentationen finns information om detta och andra uppdateringar av kommandot COMPUTE STATISTICS. Se [dokumentation](../../query-service/essential-concepts/dataset-statistics.md#alias-name) för mer information. |

{style="table-layout:auto"}

Mer information om frågetjänsten finns i [Översikt över frågetjänsten](../../query-service/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] gör att du kan segmentera data som lagras i [!DNL Experience Platform] som rör enskilda (t.ex. kunder, prospects, användare eller organisationer) till målgrupper. Du kan skapa målgrupper genom segmentdefinitioner eller andra källor från [!DNL Real-Time Customer Profile] data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform]och är lätt tillgängliga för alla Adobe-lösningar.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Målgruppsportal | Audience Portal är ett nytt sätt att surfa bland målgrupper inom Adobe Experience Platform. I Audience Portal kan du visa plattformsgenererade och externt genererade målgrupper, förbättra arbetseffektiviteten genom filtrering, mappar och taggar, skapa plattformsgenererade målgrupper och importera externt genererade målgrupper via CSV-filer. Mer information om Audience Portal finns i [Användargränssnittsguide för segmenteringstjänst](../../segmentation/ui/overview.md). |
| Målgruppssammansättning | Audience Composition är en lättanvänd arbetsyta för att bygga och redigera målgrupper med hjälp av block som används för att representera olika åtgärder. Läs mer om Audience Composition [Användargränssnittsguide för målgruppskomposition](../../segmentation/ui/audience-composition.md). |

Mer information om [!DNL Segmentation Service], kan du läsa [Översikt över segment](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | Nu kan du använda [[!DNL SAP Commerce] källa](../../sources/connectors/ecommerce/sap-commerce.md) för att få prenumerationsfaktureringsdata från [!DNL SAP Commerce] konto till Experience Platform. |
| Stöd för [!DNL Phoenix] | Nu kan du använda [[!DNL Phoenix] källa](../../sources/connectors/databases/phoenix.md) för att hämta data från [!DNL Phoenix] databas till Experience Platform. |
| Autentiseringsuppdateringar till [!DNL Salesforce] och [!DNL Salesforce Service Cloud] | Nu kan du ange API-versionen för [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) och [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) källa vid autentisering av ett nytt konto med användargränssnittet i Experience Platform eller [!DNL Flow Service] API. |

{style="table-layout:auto"}

Mer information om källor finns i [källöversikt](../../sources/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Klass | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1758/files) | Använd den här klassen för att ta in profiler för potentiella kunder som har hämtats från dataleverantörers toppmoderna kundvärvningsexempel. |
| Fältgrupp | [[!UICONTROL Enriched Event Segment Details]](https://github.com/adobe/xdm/pull/1754/files) | En lista över målgrupper som profilen är berättigad till vid tidpunkten för händelsesamlingen. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Uppdatera beskrivning |
| --- | --- | --- |
| Fältgrupp | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från experimentellt till `stable`. |
| Fältgrupp | [[!UICONTROL Media Interaction Details]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `stable` till `deprecated`. |
| Datatyp | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Datatyp | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Datatyp | [[!UICONTROL Player state data information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental`till `stable`. |
| Datatyp | [[!UICONTROL Media event information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Datatyp | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Datatyp | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Datatyp | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `stable` till `deprecated`. |
| Datatyp | [[!UICONTROL Custom metadata details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Datatyp | [[!UICONTROL Chapter details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Datatyp | [[!UICONTROL Advertising Pod details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Datatyp | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/pull/1756/files) | The `meta:status` uppdaterades från `experimental` till `stable`. |
| Utökning (kundresehantering) | [[!UICONTROL Domain]](https://github.com/adobe/xdm/pull/1756/files) | `Domain` fält har lagts till i [!UICONTROL Adobe CJM ExperienceEvent - Message Profile Details] för att registrera domänen för mottagarens e-postadress. |
| Utökning (kundresehantering) | [[!UICONTROL Channel's variant Name]](https://github.com/adobe/xdm/pull/1753/files) | Det här fältet har lagts till i [!UICONTROL AJO Entity Fields] som representerar kanalvariantens namn. |
| Tillägg (Adobe Analytics) | [[!UICONTROL Context value]](https://github.com/adobe/xdm/pull/1761/files) | `Context value` lades till i [!UICONTROL `Adobe Analytics ExperienceEvent Full Extension`]. |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md)

