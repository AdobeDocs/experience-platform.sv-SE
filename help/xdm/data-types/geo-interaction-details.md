---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;beacon;interaktionsinformation;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Datatyp för info om geo-interaktion
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen Geo Interaction Details.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# [!UICONTROL Geo interaction details] datatyp

[!UICONTROL Geo interaction details] är en standard-XDM-datatyp som beskriver det aktuella läget för inkludering i ett geografiskt definierat område.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo Shape]](./geo-shape.md) | Beskriver den geografiska formen för det område som interagerar med. Det här fältet kan beskriva en ruta, en cirkel eller en polygon. |
| `deviceGeoAccuracy` | Dubbel | Noggrannheten hos geomätningsanordningen eller -mekanismen, mätt i meter. |
| `distanceToCenter` | Dubbel | Avståndet till geocentrum i fråga om en geocirkel, mätt i meter. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
