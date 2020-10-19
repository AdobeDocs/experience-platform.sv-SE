---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data-type;data type;
solution: Experience Platform
title: Datatypen Geo Circle
topic: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen Geo Circle.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 2%

---


# [!UICONTROL Geo Circle] datatyp

[!UICONTROL Geo Circle] är en standard-XDM-datatyp som beskriver den cirkelformade geografiska regionen, givet en viss radie centrerad på en viss uppsättning koordinater. Den här datatypen baseras på den allmänna specifikationen som finns på [schema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beskriver de geografiska koordinaterna för cirkelns mitt. |
| `_schema.description` | Sträng | En beskrivning av vad cirkeln innehåller. |
| `_schema.radius` | Dubbel | Längden på cirkelns radie. Detta värde motsvarar [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) -datumet och mäts i meter. |
| `_id` | Sträng | Ett unikt, systemgenererat ID för cirkeln. |
