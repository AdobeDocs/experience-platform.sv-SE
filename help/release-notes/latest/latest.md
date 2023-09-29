---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation för september 2023 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 05136ca1a44fa0ecbf2fd9941d047c3a0899f2d1
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 28 september 2023**

Nya funktioner i Adobe Experience Platform:

- [Beräknade attribut](#computed-attributes)

Uppdateringar av befintliga funktioner i Experience Platform:

- [Larm](#alerts)
- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Identitetstjänst](#identity-service)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Beräknade attribut {#computed-attributes}

Beräknade attribut gör det enkelt att sammanfatta händelsedata i profilattribut via ett intuitivt gränssnitt för förbättrad beteendebaserad segmentering, personalisering och aktivering. Med den här funktionen kan du skapa beräknade attribut på ett självbetjäningssätt, hantera dem och använda dem vid segmentering, Real-Time CDP-destinationer eller Adobe Journey Optimizer. Dessutom förenklar beräkningsattribut segmenterings- och researbetsflödena så att ni smidigt kan leverera relevanta upplevelser. Läs mer om beräknade attribut i [översikt över beräknade attribut](../../profile/computed-attributes/overview.md).

## Larm {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika plattformsaktiviteter. Du kan prenumerera på olika varningsregler via [!UICONTROL Alerts] -fliken i användargränssnittet för plattformen och kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Fliken Aviseringshistorik | Varningarna [!UICONTROL History] kommer nu att inkludera alla händelser, inklusive fördröjningar, starter, lyckade och misslyckade. Läs [dokumentation för varningsgränssnitt](../../observability/alerts/ui.md) om du vill ha mer information om fliken Historik. |

{style="table-layout:auto"}

Läs mer om varningar i [[!DNL Observability Insights] översikt](../../observability/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Dataströmmar | Stöd för enhetssökning | När du konfigurerar en datastream kan du nu välja vilken nivå av enhetssökningsinformation som ska samlas in. Enhetssökningsinformation innehåller information om enheten, maskinvaran, operativsystemet och webbläsaren som används för att interagera med sidan. <br>  Det går inte att samla in information om enhetssökning tillsammans med användaragent- och klienttips. Om du väljer att samla in enhetsinformation inaktiveras samlingen av användaragent- och klienttips och vice versa. All enhetssökningsinformation lagras i `xdm:device` fältgrupp. Läs mer i dokumentationen om [konfigurera datastreams](../../datastreams/configure.md#geolocation-device-lookup). |
| Tillägg | [!DNL TikTok] API-tillägg för webbhändelser | The [[!DNL TikTok] API för webbhändelser](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL TikTok] i form av händelser på serversidan med [!DNL TikTok] Webbhändelser-API. |

{style="table-layout:auto"}

Läs mer om datainsamling i [datainsamling - översikt](../../tags/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade destinationer** {#new-updated-destinations}

| Destination | Nytt eller uppdaterat | Beskrivning |
| ----------- |----------------|----------- |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nytt | [[!DNL HubSpot]](https://www.hubspot.com) är en CRM-plattform med all programvara, alla integreringar och resurser ni behöver för att koppla samman marknadsföring, försäljning, innehållshantering och kundservice. Ni kan koppla samman data, team och kunder på en och samma CRM-plattform. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Uppdaterat | Stöd för [!DNL Dynamics 365] anpassade fältprefix för anpassade fält som inte skapades i standardlösningen i [!DNL Dynamics 365]. Ett nytt inmatningsfält, **[!UICONTROL Customization Prefix]**, har lagts till i [Fyll i målinformation](#destination-details) steg. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | New | Activate audiences previously onboarded to [!DNL LiveRamp] to premium publishers across mobile, web, display, and connected TV mediums. <br> After onboarding audiences to your [!DNL LiveRamp] account through the [LiveRamp - Onboarding](liveramp-onboarding.md) connection, use the new [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) connection to activate the audiences to downstream destinations.  |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Updated | The Experience Cloud Audiences destination is now generally available. Use this destination to activate audiences from Real-Time CDP to Audience Manager and Adobe Analytics. You need an Audience Manager license to send audiences to Adobe Analytics. |

-->

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Dataexport i Real-Time CDP | The [datauppsättningsexport](../../destinations/ui/export-datasets.md) är nu allmänt tillgängliga. Se [vilka datauppsättningar du kan exportera baserat på appen Experience Platform](../../destinations/ui/export-datasets.md#datasets-to-export) du köpt och kontrollera [skyddsutkast för export av datauppsättningar](/help/destinations/guardrails.md#dataset-exports). |
| (Beta) Stöd för export av arraytypobjekt | Exportera matriser med primitiva värden (sträng-, int- eller booleska värden) som platta schemafiler till molnlagringsplatser. Läs mer om funktionerna i [dokumentation](../../destinations/ui/export-arrays-calculated-fields.md). |
| Dynamiska listruteväljare i Destinationen SDK | När du skapar ett mål via Destination SDK kan du nu använda [dynamiska listruteväljare](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) om du vill fylla i fälten i en nedrullningsbar väljare med värden som hämtats från ett API. |

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

- Använd [transparens](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) nu tillgängligt för företagsdestinationer ([HTTP-API](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) och [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) på dataflödets körnivå för att övervaka aktiveringsstatistik och status i [detaljvy för dataflöde](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), med ytterligare information via felkoder och meddelanden för felsökning.
- När du uppdaterar namnet på målgrupper mappat till [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md)och andra destinationer som använder [mallar för målgruppsuppdateringar](../../destinations/destination-sdk/metadata-api/update-audience-template.md), återspeglas nu dessa namnändringar längre fram i målfönstret.

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Identitetstjänst {#identity-service}

Adobe Experience Platform identitetstjänst ger er en heltäckande bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar i användargränssnittet för identitetstjänsten | Använd det förbättrade verktyget för att skapa namnutrymmen i användargränssnittet i Experience Platform för att bättre hantera dina anpassade namnutrymmen och motsvarande identitetstyper. Det förbättrade användargränssnittet för identitetstjänsten ger dig: <ul><li>Sammanhangsbaserad upplevelse: visuella indikeringar, klarhet och sammanhang för vad ett identitetsnamnutrymme är och identitetstyper är.</li><li>Noggrannhet: Bättre felhantering utan fler dubblerade identitetsnamn.</li><li>Identifiering: Åtkomst till dokumentation inifrån en produktdialogruta.</li></ul> Mer information finns i guiden [skapa anpassade namnutrymmen](../../identity-service/namespaces.md#create-namespaces). |
| Ändringar av begränsningar för identitetsdiagram | Gränsen för identitetsdiagram har ändrats från 150 identiteter till 50 identiteter. När en ny identitet har importerats till ett fullständigt diagram tas den äldsta identiteten som baseras på tidsstämpeln för inmatningen och identitetstypen bort. Cookie-identitetstyper prioriteras för borttagning. Kontakta kontoteamet på Adobe för att begära en ändring av identitetstypen om din produktionssandlåda innehåller: <ul><li>ett anpassat namnutrymme där personidentifierarna (t.ex. CRM-ID:n) är konfigurerade som cookie/enhetsidentitetstyp.</li><li>ett anpassat namnutrymme där cookie-/enhetsidentifierare har konfigurerats som identitetstyp för olika enheter.</li></ul> Dessa förfrågningar behandlas manuellt av Adobe. Mer information finns i [skyddsutkast för identitetstjänstens data](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Läs mer om identitetstjänsten i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] gör att du kan segmentera data som lagras i [!DNL Experience Platform] som rör enskilda (t.ex. kunder, prospects, användare eller organisationer) till målgrupper. Du kan skapa målgrupper genom segmentdefinitioner eller andra källor från [!DNL Real-Time Customer Profile] data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform]och är lätt tillgängliga för alla Adobe-lösningar.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Anpassningsbara kolumner | Nu kan du anpassa layouten för Audience Portal med kolumner som kan storleksändras. Mer information om den här funktionen finns i [gränssnittsguide för segmentering](../../segmentation/ui/overview.md#customize). |
| Uppdatera frekvensuppdelning | Du kan nu visa en beskrivning av uppdateringsfrekvenserna för målgrupperna i din organisation. Mer information om den här funktionen finns i [gränssnittsguide för segmentering](../../segmentation/ui/overview.md#browse). |

Läs mer om källor i [källöversikt](../../sources/home.md).

Läs mer om segmenteringstjänsten i [Översikt över segmenteringstjänsten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya parametrar för `offset` sidindelning i självbetjäningskällor (SDK för batch) | Nu kan du ange en `endConditionName` och `endConditionValue` för källan när du använder `offset` sidnumrering. Med de här parametrarna kan du ange vilket villkor som ska avsluta pagineringsslingan i nästa HTTP-begäran. Mer information finns i [sidnumreringsguide för självbetjäningskällor (batch-SDK)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).