---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;datatype;data-type;data type;
solution: Experience Platform
title: Geo, datatyp
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen Geo XDM.
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '176'
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
| `countryCode` | Sträng | Den tvåsiffriga <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> -koden för landet. |
| `dmaID` | Heltal | Nielsens medieforskning har utsett ett marknadsområde. |
| `msaID` | Heltal | Det statistiska storstadsområdet i Förenta staterna där observationen gjordes. |
| `postalCode` | Sträng | Postnumret för platsen. Postnummer är inte tillgängliga för alla länder. I vissa länder innehåller detta endast en del av postnumret. |
| `stateProvince` | Sträng | Delstaten eller provinsdelen av observationen. Formatet följer standarden [ISO 3166-2 (land och delområde)](http://www.unece.org/cefact/locode/subdivisions.html) . |

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)