---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;interaction;point of interest;point-of-interest;datatype;data-type;data type;
solution: Experience Platform
title: Datatyp för intresseinteraktion
topic: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen Point of Interest Interaction.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# [!UICONTROL Point of interest interaction] datatyp

[!UICONTROL Point of interest interaction] är en standard-XDM-datatyp som beskriver den trådlösa enheten som kommunicerar identitetsinformation till mobilprogram när mobila enheter finns inom räckhåll.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `poiDetail` | [!UICONTROL Point of interest details](./poi-details.md) | Beskriver information om det POI som orsakade händelsen. |
| `poiEntries` | Objekt | Beskriver hur många gånger en person har angett POI. Innehåller två egenskaper: <ul><li>`id`: En unik identifierare för måttet.</li><li>`value`: Åtgärdens kvantifierbara värde.</li></ul> |
| `poiExits` | Objekt | Beskriver hur många gånger en person har lämnat POI. Innehåller två egenskaper: <ul><li>`id`: En unik identifierare för måttet.</li><li>`value`: Åtgärdens kvantifierbara värde.</li></ul> |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
