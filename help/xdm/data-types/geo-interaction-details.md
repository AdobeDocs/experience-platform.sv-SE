---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;beacon;interaktionsinformation;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Datatyp för info om geo-interaktion
topic: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen Geo Interaction Details.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '148'
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

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
