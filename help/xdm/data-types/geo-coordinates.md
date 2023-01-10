---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;schemas;scheman;geo;koordinater;datatyp;datatyp;datatyp;
solution: Experience Platform
title: Geo-koordinatens datatyp
description: Det här dokumentet innehåller en översikt över XDM-datatypen Geo Coordinates.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 2%

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
