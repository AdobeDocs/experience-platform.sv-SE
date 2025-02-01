---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;schemas;scheman;geo;koordinater;datatyp;datatyp;datatyp;
solution: Experience Platform
title: Geo-koordinatens datatyp
description: Läs mer om datatypen Geo Coordinates XDM.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Datatypen [!UICONTROL Geo Coordinates]

[!UICONTROL Geo Coordinates] är en standard-XDM-datatyp som beskriver platsens geografiska koordinater. Den här datatypen baseras på den offentliga specifikationen som dokumenteras på [schema.org](https://schema.org/GeoCoordinates).

![](../images/data-types/geo-coordinates.png){width=400}

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_schema.description` | Sträng | En beskrivning av vad koordinaterna identifierar. |
| `_schema.elevation` | Dubbel | Den specifika höjden för den definierade koordinaten. Värdet måste överensstämma med datumet [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) och mäts i meter. |
| `_schema.latitude` | Dubbel | Den signerade lodräta koordinaten för den geografiska punkten. |
| `_schema.longitude` | Dubbel | Den signerade vågräta koordinaten för den geografiska punkten. |
| `_id` | Sträng | Ett unikt, systemgenererat ID för koordinaterna. |
