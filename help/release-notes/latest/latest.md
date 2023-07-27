---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation juli 2023 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4064c4a7f855fa065c711df5d02d6b7982cc7627
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 5%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 juli 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainsamling](#data-collection)
- [Dataförberedelse](#data-prep)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

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
