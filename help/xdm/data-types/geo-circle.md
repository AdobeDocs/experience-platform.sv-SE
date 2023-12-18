---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data type;data type;
solution: Experience Platform
title: Geo Circle, datatyp
description: Läs mer om datatypen Geo Circle XDM.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# [!UICONTROL Geo Circle] datatyp

[!UICONTROL Geo Circle] är en standard-XDM-datatyp som beskriver den cirkelformade geografiska regionen, givet en viss radie centrerad på en viss uppsättning koordinater. Denna datatyp bygger på den allmänna specifikation som dokumenterats på [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beskriver de geografiska koordinaterna för cirkelns mitt. |
| `_schema.description` | Sträng | En beskrivning av vad cirkeln innehåller. |
| `_schema.radius` | Dubbel | Längden på cirkelns radie. Detta värde motsvarar [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) Datum och mäts i meter. |
| `_id` | Sträng | Ett unikt, systemgenererat ID för cirkeln. |
