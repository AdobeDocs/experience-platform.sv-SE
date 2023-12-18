---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;schemas;scheman;geo;koordinater;datatyp;datatyp;datatyp;
solution: Experience Platform
title: Geo-koordinatens datatyp
description: Läs mer om datatypen Geo Coordinates XDM.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# [!UICONTROL Geo Coordinates] datatyp

[!UICONTROL Geo Coordinates] är en standard-XDM-datatyp som beskriver platsens geografiska koordinater. Denna datatyp bygger på den allmänna specifikation som dokumenterats på [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_schema.description` | Sträng | En beskrivning av vad koordinaterna identifierar. |
| `_schema.elevation` | Dubbel | Den specifika höjden för den definierade koordinaten. Värdet måste överensstämma med [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) Datum och mäts i meter. |
| `_schema.latitude` | Dubbel | Den signerade lodräta koordinaten för den geografiska punkten. |
| `_schema.longitude` | Dubbel | Den signerade vågräta koordinaten för den geografiska punkten. |
| `_id` | Sträng | Ett unikt, systemgenererat ID för koordinaterna. |
