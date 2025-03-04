---
title: Versionsinformation om Adobe Experience Platform september 2023
description: Versionsinformationen för Adobe Experience Platform från september 2023.
exl-id: ff7fb0c1-6941-4339-8648-58f9b9e9a91f
source-git-commit: 2d640b282feb783694276c69366b1fccadddfd78
workflow-type: tm+mt
source-wordcount: '2240'
ht-degree: 28%

---

# Versionsinformation om Adobe Experience Platform

**Releasedatum: 28 september 2023**

Nya funktioner i Adobe Experience Platform:

- [Beräknade attribut](#computed-attributes)

Uppdateringar av befintliga funktioner i Experience Platform:

- [Aviseringar](#alerts)
- [Kontrollpaneler](#dashboards)
- [Datainsamling](#data-collection)
- [Dataförvaltning](#data-governance)
- [Datahygien](#hygiene)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identitetstjänst](#identity-service)
- [Frågetjänst](#query-service)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Beräknade attribut {#computed-attributes}

Beräknade attribut gör det enkelt att sammanfatta händelsedata i profilattribut via ett intuitivt gränssnitt för förbättrad beteendebaserad segmentering, personalisering och aktivering. Med den här funktionen kan du skapa beräknade attribut på ett självbetjäningssätt, hantera dem och använda dem vid segmentering, Real-Time CDP-destinationer eller Adobe Journey Optimizer. Dessutom förenklar beräkningsattribut segmenterings- och researbetsflödena så att ni smidigt kan leverera relevanta upplevelser. Läs [översikten över beräknade attribut](../../profile/computed-attributes/overview.md) om du vill veta mer om beräknade attribut.

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Fliken Aviseringshistorik | Fliken [!UICONTROL History] för aviseringar kommer nu att innehålla alla händelser, inklusive fördröjningar, starter, lyckade och misslyckade. Mer information om historikfliken finns i [dokumentationen för användargränssnittet för aviseringar](../../observability/alerts/ui.md). |

{style="table-layout:auto"}

Läs [[!DNL Observability Insights] översikten](../../observability/home.md) om du vill veta mer om aviseringar.

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera [!DNL dashboards] som du kan använda för att visa viktig information om organisationens data, som de har hämtats under dagliga ögonblicksbilder.

| Funktion | Beskrivning |
| --- | --- |
| [Förbättring av kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md) | Behåll kontrollen över era licensavtal med förbättrad rapportering och viktiga mätvärden för organisationens licensanvändning. Dessa förbättringar ger en hög detaljrikedom i förhållande till era användningsvärden för licenser för alla Experience Platform-produkter ni har köpt. |

{style="table-layout:auto"}

Mer information om kontrollpanelen för licensanvändning finns i [översikten över kontrollpanelen för licensanvändning](../../dashboards/guides/destinations.md).

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Dataströmmar | Stöd för enhetssökning | När du konfigurerar en datastream kan du nu välja vilken nivå av enhetssökningsinformation som ska samlas in. Enhetssökningsinformation innehåller information om enheten, maskinvaran, operativsystemet och webbläsaren som används för att interagera med sidan. <br> Det går inte att samla in information om enhetssökning tillsammans med användaragent- och klienttips. Om du väljer att samla in enhetsinformation inaktiveras samlingen av användaragent- och klienttips och vice versa. All enhetssökningsinformation lagras i fältgruppen `xdm:device`. Läs mer i dokumentationen om [konfiguration av datastreams](../../datastreams/configure.md#geolocation-device-lookup). |
| Tillägg | API-tillägg för [!DNL TikTok]-webbhändelser | Med tillägget [[!DNL TikTok] API:t för webbhändelser](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka det till [!DNL TikTok] i form av händelser på serversidan med hjälp av API:t för webbhändelser i [!DNL TikTok] . |

{style="table-layout:auto"}

Läs [datainsamlingsöversikten](../../tags/home.md) om du vill veta mer om datainsamling.

## Dataförvaltning {#data-governance}

Dataförvaltning i Adobe Experience Platform är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Den spelar en viktig roll inom Experience Platform på olika nivåer, bland annat katalogföring, datahärkomst, märkning av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya etiketter för ekosystem för partners för data från tredje part | Det finns nya etiketter för dataanvändning för anrikning och prospektering från tredje part. Mer information finns i [dokumentationen om etiketter för partnerekosystem](../../data-governance/labels/reference.md#partner). |

{style="table-layout:auto"}

Läs [översikten över datastyrning](../../data-governance/home.md) om du vill veta mer om datastyrning.

## Datahygien {#hygiene}

Experience Platform har en serie funktioner för datthygien som gör att du kan hantera lagrade data genom att ta bort konsumentposter och datauppsättningar programmatiskt. Med arbetsytan [!UICONTROL Data Lifecycle] i användargränssnittet eller genom anrop till API:t för datahygien kan du hantera dina datalager effektivt. Använd dessa funktioner för att säkerställa att informationen används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationspolicyer anser det nödvändigt.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} Ta bort post (begränsad version) | Hantera datalivscykeln i alla datalager för att uppfylla kundernas åtaganden och licensavtal med de avancerade funktionerna för livscykelhantering i Adobe Experience Platform: Automatiserad datamängdsförfallotid och borttagning av post.<br>Med automatisk förfallotid för datauppsättning kan du ta bort hela datauppsättningar och ange ett datum och en tid för när datauppsättningen ska tas bort.<br>Med Ta bort post kan du ta bort enskilda konsumentprofiler genom att ange deras primära identiteter som mål. Du kan ange de primära identiteterna individuellt via användargränssnittet eller via CSV/JSON-filöverföring. Mer information finns i [dokumentationen för borttagning av post](../../hygiene/ui/record-delete.md) |
| Utgångsdatum för datauppsättning | Minimera era era data och ha full kontroll över era licensavtal med Automated Dataset Expiration. Minska datavolymer genom att ta bort hela datauppsättningar och ange datum och tid för när datauppsättningen ska tas bort. Mer information finns i [dokumentationen om förfallodatum för datauppsättning](../../hygiene/ui/dataset-expiration.md). |

{style="table-layout:auto"}

Mer information om plattformens datahygien finns i [översikten över datahygien](../../hygiene/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Nytt eller uppdaterat | Beskrivning |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | Nyhet | Aktivera målgrupper som tidigare har anslutit till [!DNL LiveRamp] för premiumutgivare på olika medier för mobil, webb, skärm och ansluten TV. <br> När du har introducerat målgrupper till ditt [!DNL LiveRamp]-konto via [LiveRamp - introduktion](../../destinations/catalog/advertising/liveramp-onboarding.md) använder du den nya [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md)-anslutningen för att aktivera målgrupperna till underordnade mål. |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nyhet | [[!DNL HubSpot]](https://www.hubspot.com) är en CRM-plattform med all programvara, alla integreringar och resurser du behöver för att koppla samman marknadsföring, försäljning, innehållshantering och kundtjänst. Ni kan koppla samman data, team och kunder på en och samma CRM-plattform. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Uppdaterat | Stöd har lagts till för [!DNL Dynamics 365] anpassade fältprefix för anpassade fält som inte skapades i standardlösningen i [!DNL Dynamics 365]. Ett nytt inmatningsfält, **[!UICONTROL Customization Prefix]**, har lagts till i steget [Fyll i målinformation](#destination-details). |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Uppdaterat | Experience Cloud Audiences-målet är nu allmänt tillgängligt. Använd det här målet för att aktivera målgrupper från Real-Time CDP till Audience Manager och Adobe Analytics. Du behöver en Audience Manager-licens för att skicka målgrupper till Adobe Analytics. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 

-->

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

| Funktionalitet | Beskrivning |
| ----------- | ----------- |
| Dataexport i Real-Time CDP | Funktionen för [datauppsexport](../../destinations/ui/export-datasets.md) är nu allmänt tillgänglig. Se [vilka datauppsättningar du kan exportera baserat på den Experience Platform-app](../../destinations/ui/export-datasets.md#datasets-to-export) du har köpt och kontrollera [skyddsutkast för export av datauppsättningar](/help/destinations/guardrails.md#dataset-exports). |
| (Beta) Stöd för export av arraytypobjekt | Exportera matriser med primitiva värden (sträng-, int- eller booleska värden) som platta schemafiler till molnlagringsplatser. Läs mer om funktionerna i [dokumentationen](../../destinations/ui/export-arrays-maps-objects.md). |
| Dynamiska listruteväljare i Destination SDK | När du skapar ett mål via Destination SDK kan du nu använda [dynamiska listruteväljare](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) för att fylla i fälten i en nedrullningsbar väljare med värden som hämtats från ett API. |

**Korrigeringar och förbättringar** {#destinations-fixes-and-enhancements}

- Använd [övervakning av genomskinlighet](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) som nu är tillgänglig för företagsmål ([HTTP API](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) och [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) vid körningsnivån för att övervaka aktiveringsmått och status i [dataflödesdetaljvyn](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), med ytterligare information via felkoder och felsökningsmeddelanden.
- När du uppdaterar namnet på målgrupper som är mappade till [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md) och andra mål som använder [målgruppsuppdateringsmallar](../../destinations/destination-sdk/metadata-api/update-audience-template.md), återspeglas nu dessa namnändringar nedströms i målet.

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Snabbåtgärder som lagts till i schemaredigeraren | Nya snabbåtgärder har lagts till på arbetsytan i Schemaredigeraren. Nu kan du kopiera JSON-strukturen eller ta bort schemat direkt från redigeraren.<br>![Snabbåtgärderna i schemaredigeraren.](../2023/assets/schema-editor-copy-json.png "Schemaredigeraren med Mer och Kopiera till JSON är markerat."){width="100" zoomable="yes"} |
| Filtrera XDM-resurser efter anpassad eller standardskapare | Listorna med tillgängliga scheman, fältgrupper, datatyper och klasser är nu förfiltrerade baserat på den metod som används för att skapa dem. På så sätt kan du filtrera resurser baserat på om de har skapats eller byggts av Adobe.<br>![Standardfilter och anpassade filter på arbetsytan Scheman.](../2023/assets/standard-and-custom-classes.png "Arbetsytan Scheman med standardfilter och anpassade filter markerade."){width="100" zoomable="yes"} <br> Mer information finns i [dokumentationen för att skapa och redigera resurser](../../xdm/ui/resources/classes.md#filter.md). |

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdaterat arbetsflöde för att skapa schema | Ett nytt arbetsflöde för att skapa scheman har implementerats för att effektivisera processen. <br> ![Det nya gränssnittet för schemaskapande.](../2023/assets/schema-class-options.png "Väljaren för ny schemainformation har markerats."){width="100" zoomable="yes"} <br> Mer information finns i [schemaskapandedokumentationen](../../xdm/ui/resources/schemas.md#create). |

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Datatyp | [[!UICONTROL Return]](https://github.com/adobe/xdm/pull/1773/files) | RMA (Return Merchandise Authorization) har utfärdats. |
| Datatyp | [[!UICONTROL Return Item]](https://github.com/adobe/xdm/pull/1773/files) | Det returnerade objektets information i RMA (Return Merchandise Authorization). |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Uppdatera beskrivning |
| --- | --- | --- |
| Tillägg | [!UICONTROL AJO Entity Fields] | [[!UICONTROL flag for multi-variant]](https://github.com/adobe/xdm/pull/1774/files) lades till i [!UICONTROL AJO Entity Fields] för att identifiera om varianten är en multivariant eller inte. |
| Datatyp | [!UICONTROL Product list item] | [[!UICONTROL Return Item]](https://github.com/adobe/xdm/pull/1773/files) lades till för att inkludera information om auktorisering för returförsäljning. |
| Datatyp | Beställning | [[!UICONTROL Return Info]](https://github.com/adobe/xdm/pull/1773/files) lades till för att inkludera den RMA (Return Merchandise Authorization) som utfärdats. |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [systemöversikten för XDM](../../xdm/home.md)

## Identitetstjänst {#identity-service}

Adobe Experience Platforms identitetstjänst ger dig en heltäckande bild av dina kunder och deras beteende genom att koppla samman identiteter mellan enheter och system så att du kan leverera effektiva, personliga digitala upplevelser i realtid.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar i användargränssnittet för identitetstjänsten | Använd det förbättrade verktyget för att skapa namnutrymmen i Experience Platform-användargränssnittet för att bättre hantera dina anpassade namnutrymmen och motsvarande identitetstyper. Det förbättrade användargränssnittet för identitetstjänsten ger dig: <ul><li>Sammanhangsbaserad upplevelse: visuella indikeringar, klarhet och sammanhang för vad ett identitetsnamnutrymme är och identitetstyper är.</li><li>Noggrannhet: Bättre felhantering utan fler dubblerade identitetsnamn.</li><li>Identifiering: Åtkomst till dokumentation inifrån en produktdialogruta.</li></ul> Mer information finns i handboken [Skapa anpassade namnutrymmen](../../identity-service/features/namespaces.md#create-namespaces). |
| Ändringar av begränsningar för identitetsdiagram | Gränsen för identitetsdiagram har ändrats från 150 identiteter till 50 identiteter. När en ny identitet har importerats till ett fullständigt diagram tas den äldsta identiteten som baseras på tidsstämpeln för inmatningen och identitetstypen bort. Cookie-identitetstyper prioriteras för borttagning. Kontakta Adobe Account Team om du vill ändra identitetstypen om din produktionssandlåda innehåller: <ul><li>ett anpassat namnutrymme där personidentifierarna (t.ex. CRM-ID:n) är konfigurerade som cookie/enhetsidentitetstyp.</li><li>ett anpassat namnutrymme där cookie-/enhetsidentifierare har konfigurerats som identitetstyp för olika enheter.</li></ul> Dessa förfrågningar behandlas manuellt av Adobe Engineering. Mer information finns i [skyddsutkastet för Identity Service-data](../../identity-service/guardrails.md) och i guiden om [tillstånd för datahanteringslicenser ](../../landing/license-usage-and-guardrails/data-management-best-practices.md). |

{style="table-layout:auto"}

Om du vill veta mer om identitetstjänsten kan du läsa [översikt över identitetstjänsten](../../identity-service/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard SQL för att söka efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla samman alla datauppsättningar från [!DNL Data Lake] och samla in sökresultaten som en ny datauppsättning för användning i rapportering, arbetsytan för datavetenskap eller för inmatning i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Loggfiltrering av gränssnittsuppdateringar | Förbättrad filtrering av frågeloggar ger ökad synlighet för användargenererade loggar för övervakning, administration och felsökning. Du kan filtrera listan med frågeloggar baserat på olika inställningar. <br> ![Filterinställningar för frågeloggfilter.](../2023/assets/log-filter-settings.png "Nya frågeloggsfilter är markerade."){width="100" zoomable="yes"} <br> Mer information finns i [frågeloggsdokumentationen](../../query-service/ui/query-logs.md#filter-logs). |
| Gränssnittsuppdateringar för flerfrågeredigeraren | Du kan nu köra flera sekventiella frågor i Frågeredigeraren eller skriva mer än en fråga och köra alla frågor på ett sekventiellt sätt. Om du vill göra frågekörningen mer flexibel kan du markera den valda frågan och välja att köra den specifika frågan oberoende av de andra. Mer information finns i [Användargränssnittsguiden för frågeredigeraren](../../query-service/ui/user-guide.md#execute-multiple-sequential-queries). |

{style="table-layout:auto"}

Mer information om frågetjänster finns i [översikten över frågetjänster](../../query-service/home.md).

## Segmenteringstjänst {#segmentation}

Med [!DNL Segmentation Service] kan du segmentera data som lagras i [!DNL Experience Platform] och som relaterar till individer (t.ex. kunder, potentiella kunder, användare eller organisationer) till målgrupper. Du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform] och är tillgängliga för alla Adobe-lösningar.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Anpassningsbara kolumner | Nu kan du anpassa layouten för Audience Portal med kolumner som kan storleksändras. Mer information om den här funktionen finns i [Översikt över målportalen](../../segmentation/ui/audience-portal.md#customize). |
| Uppdatera frekvensuppdelning | Du kan nu visa en beskrivning av uppdateringsfrekvenserna för målgrupperna i din organisation. Mer information om den här funktionen finns i [segmenteringsgränssnittsguiden](../../segmentation/ui/overview.md#browse). |

Läs [Översikt över segmenteringstjänsten](../../segmentation/home.md) om du vill veta mer om segmenteringstjänsten.

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya parametrar för `offset`-sidindelning i självbetjäningskällor (Batch SDK) | Du kan nu ange `endConditionName` och `endConditionValue` för källan när du använder sidnumrering `offset`. Med de här parametrarna kan du ange vilket villkor som ska avsluta pagineringsslingan i nästa HTTP-begäran. Mer information finns i [pagineringsguiden för självbetjäningskällor (Batch SDK)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Läs [Källöversikten](../../sources/home.md) om du vill veta mer om källor.
