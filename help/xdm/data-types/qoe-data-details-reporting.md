---
title: QoE (Quality of Experience), datadetaleringsdatatyp
description: Läs mer om datatypen QoE (Quality of Experience) Data Details Reporting Data Type Experience Data Model (XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# QoE (Quality of Experience), datadetaleringsdatatyp

[!UICONTROL QoE Data Details] Rapportering är en XDM-datatyp (Standard Experience Data Model) som ger detaljerade mått för upplevelsekvaliteten (QoE) under medieuppspelningen. Använd [!UICONTROL QoE Data Details] Rapporterar datatyp för att samla in information som bithastighetsinformation, bildrutehastigheter, buffringshändelser, uteslutna bildrutor och så vidare. Medierapporteringsfält används av Adobe-tjänster för att analysera de Media Collection-fält som skickas av användarna. Dessa data, tillsammans med andra specifika användarvärden, beräknas och rapporteras utifrån. Den här datatypen gör det möjligt att analysera uppspelningskvaliteten, vilket ger insikter i direktuppspelningsprestanda, användarupplevelse och eventuella problem som uppstår under uppspelningssessioner.

+++Välj för att visa datatypen QoE Data Details Reporting.
![Ett diagram över datatypen QoE (Quality of Experience) Data Details.](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>Varje visningsnamn innehåller en länk med mer information om dess ljud- och videoparametrar. De länkade sidorna innehåller information om videoannonser som samlats in av Adobe, implementeringsvärden, nätverksparametrar, rapporter och viktiga överväganden.

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|---------------------------------------------------------------------------------------------------|
| [[!UICONTROL Average Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate-1) | `bitrateAverage` | tal | Genomsnittlig bithastighet (i kbit/s, heltal). Beräknas som ett vägt medelvärde av bithastighetsvärden. |
| [[!UICONTROL Average Bitrate Bucket]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrateAverageBucket` | string | Den genomsnittliga bithastigheten (i kbit/s) som kategoriseras i fördefinierade intervall med 100 kbit/s intervall. |
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | heltal | Bithastighetsvärdet (i kbit/s). |
| [[!UICONTROL Bitrate Change Impacted Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | boolesk | Anger om strömmar påverkades av bithastighetsändringar under uppspelning. |
| [[!UICONTROL Bitrate Changes]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-changes) | `bitrateChangeCount` | heltal | Det totala antalet bithastighetsändringar under uppspelning. |
| [[!UICONTROL Buffer Events]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-events) | `bufferCount` | heltal | Antalet olika buffertlägen under uppspelning. |
| [[!UICONTROL Buffer Impacted Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-impacted-streams) | `hasBufferImpactedStreams` | boolesk | Anger om strömmar påverkades av buffring under uppspelning. |
| [[!UICONTROL Dropped Frame Impacted Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | boolesk | Anger om strömmar påverkades av uteslutna bildrutor under uppspelningen. |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames-1) | `droppedFrames` | heltal | Det totala antalet bildrutor som utelämnas under uppspelningen. |
| [[!UICONTROL Drops Before Starts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#drops-before-start) | `isDroppedBeforeStart` | boolesk | Anger om användare stänger av videon innan den börjar, oavsett annonser. |
| [[!UICONTROL Error Impacted Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#error-impacted-streams) | `hasErrorImpactedStreams` | boolesk | Anger om strömmar råkade ut för fel under uppspelning. |
| [[!UICONTROL Errors]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#errors-%2F-error-events) | `errorCount` | heltal | Det totala antalet fel som uppstod under uppspelningen. |
| [[!UICONTROL External Error IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#external-error-ids) | `externalErrors` | array med strängar | Unika fel-ID från externa källor, t.ex. CDN-fel. |
| [[!UICONTROL Frames Per Second]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | heltal | Aktuell flödeshastighet (i bildrutor per sekund). |
| [[!UICONTROL Media SDK Error IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#media-sdk-error-ids) | `mediaSdkErrors` | array med strängar | Unika fel-ID:n som genereras av Media SDK under uppspelning. |
| [[!UICONTROL Player SDK Error IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#player-sdk-error-ids) | `playerSdkErrors` | array med strängar | Unika fel-ID:n som genereras av spelarens SDK under uppspelning. |
| [[!UICONTROL Stalling Events]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-events) | `stallCount` | heltal | Antalet förhalande händelser under uppspelning. |
| [[!UICONTROL Stalling Impacted Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-impacted-streams) | `hasStallImpactedStreams` | boolesk | Anger om strömmar upplevde fördröjning under uppspelning. |
| [[!UICONTROL Time To Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | heltal | Varaktighet (i sekunder) mellan inläsning av video och start. |
| [[!UICONTROL Total Buffer Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-buffer-duration-1) | `bufferTime` | heltal | Sammanlagd tid (i sekunder) för buffring under uppspelning. |
| [[!UICONTROL Total Stalling Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-stalling-duration) | `stallTime` | heltal | Den totala tiden (i sekunder) som uppspelningen stoppades under uppspelningen. |

{style="table-layout:auto"}
