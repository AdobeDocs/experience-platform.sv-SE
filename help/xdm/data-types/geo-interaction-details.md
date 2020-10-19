---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Datatyp för geografisk interaktionsinformation
topic: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen Geo Interaction Details.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '130'
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
