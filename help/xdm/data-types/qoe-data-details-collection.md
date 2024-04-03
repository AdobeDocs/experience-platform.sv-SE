---
title: QoE-datainsamling (Quality of Experience), datatyp
description: Lär dig mer om datatypen QoE (Quality of Experience) Datainsamling av typen XDM (Experience Data Model).
source-git-commit: e1c94635b691c68de6154d19e974bfdf2e250923
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Datatypen QoE (Quality of Experience) för datainsamling

[!UICONTROL QoE Data Details] Samlingen är en XDM-datatyp (Standard Experience Data Model) som ger detaljerade mått för upplevelsekvaliteten (QoE) under medieuppspelningen. Använd [!UICONTROL QoE Data Details] Samlingsdatatyp för att samla in information om till exempel bithastigheter, bildrutehastigheter, buffringshändelser, uteslutna bildrutor och så vidare. Fält för mediainsamling hämtar data och skickar dem till andra Adobe-tjänster för vidare bearbetning. Den här datatypen gör det möjligt att analysera uppspelningskvaliteten, vilket ger insikter i direktuppspelningsprestanda, användarupplevelse och eventuella problem som uppstår under uppspelningssessioner.

+++Välj för att visa datatypen QoE Data Details.
![Ett diagram över datatypen QoE (Quality of Experience) Data Details Collection.](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Varje visningsnamn innehåller en länk med mer information om dess ljud- och videoparametrar. De länkade sidorna innehåller information om videoannonser som samlats in av Adobe, implementeringsvärden, nätverksparametrar, rapporter och viktiga överväganden.

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | heltal | Nej | Bithastighetsvärdet (i kbit/s). |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | heltal | Nej | Det totala antalet bildrutor som utelämnas under uppspelningen. |
| [[!UICONTROL Frames Per Second]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | heltal | Nej | Aktuell flödeshastighet (i bildrutor per sekund). |
| [[!UICONTROL Time To Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | heltal | Nej | Varaktighet (i sekunder) mellan inläsning av video och start. |

{style="table-layout:auto"}
