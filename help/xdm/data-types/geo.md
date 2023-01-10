---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;geo;datatype;data type;data type;
solution: Experience Platform
title: Geo-datatyp
description: Det här dokumentet innehåller en översikt över datatypen Geo XDM.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 3%

---

# [!UICONTROL Geo] datatyp

[!UICONTROL Geo] är en standard-XDM-datatyp som beskriver det geografiska område där en händelse observerades.

<img src="../images/data-types/geo.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beskriver platsens geografiska koordinater. |
| `_id` | Sträng | Ett unikt, systemgenererat ID för koordinaterna. |
| `city` | Sträng | Namnet på staden. |
| `countryCode` | Sträng | De två tecknen <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> landskoden. |
| `dmaID` | Heltal | Nielsens medieforskning har utsett ett marknadsområde. |
| `msaID` | Heltal | Det statistiska storstadsområdet i Förenta staterna där observationen gjordes. |
| `postalCode` | Sträng | Postnumret för platsen. Postnummer är inte tillgängliga för alla länder. I vissa länder innehåller detta endast en del av postnumret. |
| `stateProvince` | Sträng | Delstaten eller provinsdelen av observationen. Formatet följer [ISO 3166-2 (land och delområde)](https://www.unece.org/cefact/locode/subdivisions.html) standard. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
