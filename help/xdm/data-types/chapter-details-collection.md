---
title: Datatyp för insamling av kapitelinformation
description: Lär dig mer om datatypen Kapitel Details Collection Experience Data Model (XDM).
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# [!UICONTROL Chapter Details] Samlingsdatatyp

[!UICONTROL Chapter Details]-samlingen är en XDM-datatyp (Standard Experience Data Model) som beskriver olika attribut relaterade till kapitel eller segment i medieinnehållet. Använd datatypen [!UICONTROL Chapter Details] Samling för att hämta information som kapitelnamn, förskjutning, varaktighet och kapitelindex. Fält för mediainsamling hämtar data och skickar dem till andra Adobe-tjänster för vidare bearbetning.

![Ett diagram över datatypen för kapitelinformationsinsamlingen.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Varje visningsnamn innehåller en länk med mer information om dess ljud- och videoparametrar. De länkade sidorna innehåller information om videoannonser som samlats in av Adobe, implementeringsvärden, nätverksparametrar, rapporter och viktiga överväganden.

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | heltal | Ja | Kapitelns längd i sekunder. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | string | Nej | Namnet på kapitlet och/eller segmentet. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | heltal | Ja | Kapitelns förskjutning i innehållet (i sekunder) från början. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | heltal | Ja | Placeringen (index, heltal) av kapitlet inuti innehållet. |

{style="table-layout:auto"}
