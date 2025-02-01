---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data type;data type;
solution: Experience Platform
title: Geo Circle, datatyp
description: Läs mer om datatypen Geo Circle XDM.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Datatypen [!UICONTROL Geo Circle]

[!UICONTROL Geo Circle] är en standard-XDM-datatyp som beskriver den cirkulära geografiska regionen, med en viss radie centrerad på en viss uppsättning koordinater. Den här datatypen baseras på den offentliga specifikationen som dokumenteras på [schema.org](https://schema.org/GeoCircle).

![](../images/data-types/geo-circle.png){width=400}

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beskriver de geografiska koordinaterna för cirkelns mitt. |
| `_schema.description` | Sträng | En beskrivning av vad cirkeln innehåller. |
| `_schema.radius` | Dubbel | Längden på cirkelns radie. Det här värdet överensstämmer med datumet [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) och mäts i meter. |
| `_id` | Sträng | Ett unikt, systemgenererat ID för cirkeln. |
