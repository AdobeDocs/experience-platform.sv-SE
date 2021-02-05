---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;geo;geo shape;datatype;data type;data type;
solution: Experience Platform
title: Geo, formdatatyp
topic: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen Geo Shape.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 1%

---


# [!UICONTROL Geo Shape] datatyp

[!UICONTROL Geo Shape] är en standard-XDM-datatyp som beskriver formen på ett geografiskt område. Den här datatypen baseras på den offentliga specifikationen som dokumenteras i [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_schema.box` | Matris med [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beskriver ett geografiskt område som omges av en rektangel som består av två koordinater. Den första koordinaten är rektangelns nedre hörn och den andra koordinaten är det övre hörnet. |
| `_schema.circle` | Matris med [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beskriver ett cirkelformat område med en viss radie centrerad på en geografisk koordinat. |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | En serie med fyra eller fler koordinater där de första och sista koordinaterna är identiska. |
| `_schema.description` | Sträng | En beskrivning av vad formen definierar. |
| `_schema.elevation` | Dubbel | Formens specifika eller lägsta höjd. Detta värde motsvarar [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-datumet och mäts i meter. I kombination med `ceiling` kan den här egenskapen användas för att uttrycka en tredimensionell begränsningsram för en plats. |
| `_id` | Sträng | En unik systemgenererad identifierare för formen. |
| `ceiling` | Dubbel | Formens maximala höjd. Den här egenskapen är bara giltig när den används i kombination med `elevation`. Värdet överensstämmer med [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-datumet och mäts i meter. I kombination med `elevation` kan den här egenskapen användas för att uttrycka en tredimensionell begränsningsram för en plats. |
