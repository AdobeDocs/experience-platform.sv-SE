---
title: Kapitelinformation, rapportdatatyp
description: Läs mer om datatypen Kapitel Details Reporting Experience Data Model (XDM).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# [!UICONTROL Chapter Details] Typ av rapportdata

[!UICONTROL Chapter Details] Rapportering är en XDM-datatyp (Standard Experience Data Model) som beskriver olika attribut som rör kapitel eller segment i medieinnehåll. Använd [!UICONTROL Chapter Details] Rapportera datatyp för att samla in detaljer som kapitelnamn, varaktighet, position, ID, uppspelningsstatus (start/slutförd) och hur lång tid som har ägnats åt varje kapitel. Medierapporteringsfält används av Adobe-tjänster för att analysera de Media Collection-fält som skickas av användarna. Dessa data, tillsammans med andra specifika användarvärden, beräknas och rapporteras utifrån.

![Ett diagram över datatypen Chapter Details Reporting.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Varje visningsnamn innehåller en länk med mer information om dess ljud- och videoparametrar. De länkade sidorna innehåller information om videoannonser som samlats in av Adobe, implementeringsvärden, nätverksparametrar, rapporter och viktiga överväganden.

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Chapter Completed]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | boolesk | Anger om kapitlet har slutförts eller inte. |
| [[!UICONTROL Chapter ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | string | Kapitelets automatiskt genererade ID. |
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | heltal | Kapitelns längd i sekunder. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | string | Namnet på kapitlet och/eller segmentet. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | heltal | Kapitelns förskjutning i innehållet (i sekunder) från början. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | heltal | Placeringen (index, heltal) av kapitlet inuti innehållet. |
| [[!UICONTROL Chapter Started]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | boolesk | Anger om kapitlet har startats eller inte. |
| [[!UICONTROL Chapter Time Played]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | heltal | Den tid som har ägnats åt kapitlet, i sekunder. |
