---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fält;scheman;scheman;poi;interaktion;intressepunkt;datatyp;datatyp;datatyp;datatyp;
solution: Experience Platform
title: Datatyp för intressepunktsinteraktion
description: Det här dokumentet innehåller en översikt över XDM-datatypen Point of Interest Interaction.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '176'
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

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
