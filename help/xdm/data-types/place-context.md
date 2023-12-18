---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;place context;placeContext;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Montera kontextdatatyp
description: Läs mer om datatypen Place Context XDM.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# [!UICONTROL Place context] datatyp

[!UICONTROL Place context] är en standard-XDM-datatyp som beskriver platsen för en observerad händelse, inklusive intressepunktsinformation och geografiska koordinater.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Beskriver information om POI-interaktionen (point-of-interest). |
| `activePOIs` | Array med [[!UICONTROL Point of interest details]](./poi-details.md) | Beskriver de POI:er som orsakade händelsen. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beskriver den geografiska plats där upplevelsen levererades. |
| `localTime` | DateTime | En tidsstämpel i [RFC 3339](https://tools.ietf.org/html/rfc3339) format, som anger lokal tid med en angiven tidszonsförskjutning. Formateringsmönstret är `yyyy-MM-dd'T'HH:mm:ssXXX` (till exempel `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Heltal | Aktuell lokal tidszonsförskjutning i minuter från UTC för `localTime` värde. Detta bör inkludera aktuell DST-förskjutning om tillämpligt. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
