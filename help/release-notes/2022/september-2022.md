---
title: Adobe Experience Platform Release Notes september 2022
description: Versionsinformation för september 2022 för Adobe Experience Platform.
source-git-commit: 5335c77b4636d10064e8786525c9f8f893371b9b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 28 september 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Experience Data Model (XDM)](#xdm)
- [Identitetstjänst](#identity-service)
- [Källor](#sources)

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Gränssnittsstöd för uppräkningar och föreslagna värden | Förutom uppräkningar som aktiverar dataverifiering kan du nu [lägga till eller ta bort föreslagna värden](../../xdm/ui/fields/enum.md) för standardsträngfält eller anpassade strängfält så att plattformsanvändare har en egen lista med värden att välja mellan när segment skapas. |

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Egenskaper för ett specifikt element som interagerades och som orsakade att proposition-händelsen utlöstes. |
| Fältgrupp | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Spåra medieinteraktioner över tid. |
| Fältgrupp | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Information om medieinformation spåras. |
| Fältgrupp | [[!UICONTROL Adobe CJM ExperienceEvent - Surfaces]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Beskriver ytor för Experience Events i Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Beteende | [[!UICONTROL Time series]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Tillagda värden för `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Borttagna värden för `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Fältgrupp | (Flera) | [Uppdaterade flera fältbeskrivningar](https://github.com/adobe/xdm/pull/1628/files) över Journey Orchestration-komponenter. |
| Fältgrupp | (Flera) | [Titlarna för flera Adobe Workfront-komponenter har uppdaterats](https://github.com/adobe/xdm/pull/1634/files) för enhetlighet. |
| Fältgrupp | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Namnutrymmena för flera fält har uppdaterats till `xdm`. |
| Fältgrupp | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Ett nytt fält har lagts till, `isReadSegmentTriggerStartEvent`. |
| Fältgrupp | [[!UICONTROL Forecasted Weathers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Ändrad `xdm:uvIndex` fält till en heltalstyp och lägger till `xdm` namnutrymme till flera fält som saknades. |
| Fältgrupp | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` och `xdm:implementationDetails` har tagits bort från fältgruppen. |
| Datatyp | (Flera) | [Uppdaterat flera mediaegenskapsnamn](https://github.com/adobe/xdm/pull/1626/files) i flera datatyper för att vara konsekventa. |
| Datatyp | [[!UICONTROL Implementation details]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Okända namn för fladder har lagts till. |
| Datatyp | [[!UICONTROL Point of interest details]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Datatypen kan nu acceptera en lista med metadatanyckelvärdepar som är associerade med den aktuella punkten. |
| Datatyp | [[!UICONTROL Proposition Action]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] har bytt namn till [!UICONTROL Proposition Action]. |
| Datatyp | [[!UICONTROL Proposition Event Type]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] har bytt namn till [!UICONTROL Proposition Action]. |
| (Flera) | (Flera) | Experimentella egenskaper har [stabiliserad för alla B2B-komponenter](https://github.com/adobe/xdm/pull/1617/files). |
| (Flera) | (Flera) | Adobe Journey Optimizer enheter har [stabiliserad](https://github.com/adobe/xdm/pull/1625/files). |
| (Flera) | (Flera) | Namnutrymmen för vissa fält i flera experimentella komponenter har [uppdaterat för enhetlighet](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Identitetstjänst {#identity-service}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för borttagning av datauppsättningar | Identitetstjänsten har nu stöd för borttagning av datauppsättningar vid begäran via [Katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), användargränssnittet eller datahygien. Läs guiden på [ta bort datauppsättningar i användargränssnittet](../../catalog/datasets/user-guide.md#delete-a-dataset) för mer information. |

Mer information om identitetstjänsten finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Audience Manager segmentpopulationens påverkan på kundprofilen i realtid | Intag av stora Audience Manager-segmentpopulationer har en direkt inverkan på det totala antalet profiler när du för första gången skickar ett Audience Manager-segment till plattformen via Audience Manager. Det innebär att om du väljer alla segment kan det eventuellt leda till ett profilantal som överskrider licensanvändningsbehörigheten. Mer information finns i [Översikt över Audience Manager-källa](../../sources/connectors/adobe-applications/audience-manager.md). Mer information om licensanvändningen finns i dokumentationen om [med kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md). |

Läs mer om källor i [källöversikt](../../sources/home.md).