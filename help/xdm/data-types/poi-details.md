---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fält;scheman;scheman;scheman;poi;poi details;punkt of interest;point of interest details;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Datatyp för intressepunktsinformation
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen Point of Interest Details.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---

# [!UICONTROL Point of interest details] datatyp

[!UICONTROL Point of interest details] är en standard-XDM-datatyp som beskriver geografiska data där en händelse observerades.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Beskriver de beacon-detaljer som är aktiva för POI-interaktionen. |
| `geoInteractionDetails` | [[!UICONTROL Geo interaction details]](./geo-interaction-details.md) | Beskriver de geografiska detaljer som är aktiva för POI-interaktionen. |
| `category` | Sträng | En allmän kategori som tilldelats för att organisera POI-poster av administratören för POI-definitioner. |
| `distanceToPOICenter` | Dubbel | Det beräknade avståndet från POI-centret i meter. |
| `locatingType` | Sträng | Mekanismen som används för att fastställa plats. Godkända värden är: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Sträng | Ett namn som POI får. |
| `poiID` | Sträng | En unik identifierare för POI. |
| `type` | Sträng | Den allmänna typen av POI med ett typningsschema som valts av administratören för POI-definitionerna. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
