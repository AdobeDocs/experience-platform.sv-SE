---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fält;scheman;scheman;poi;interaktion;intressepunkt;datatyp;datatyp;datatyp;datatyp;
solution: Experience Platform
title: Datatyp för intressepunktsinteraktion
topic: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen Point of Interest Interaction.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# [!UICONTROL Point of interest interaction] datatyp

[!UICONTROL Point of interest interaction] är en standard-XDM-datatyp som beskriver den trådlösa enheten som kommunicerar identitetsinformation till mobilprogram när mobila enheter finns inom räckhåll.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | Beskriver information om det POI som orsakade händelsen. |
| `poiEntries` | Objekt | Beskriver hur många gånger en person har angett POI. Innehåller två egenskaper: <ul><li>`id`: En unik identifierare för måttet.</li><li>`value`: Åtgärdens kvantifierbara värde.</li></ul> |
| `poiExits` | Objekt | Beskriver hur många gånger en person har lämnat POI. Innehåller två egenskaper: <ul><li>`id`: En unik identifierare för måttet.</li><li>`value`: Åtgärdens kvantifierbara värde.</li></ul> |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
