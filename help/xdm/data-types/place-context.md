---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;place context;placeContext;datatype;data-type;data type;
solution: Experience Platform
title: Datatypen Montera kontext
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen Place Context XDM.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 3%

---


# [!UICONTROL Place context] datatyp

[!UICONTROL Place context] är en standard-XDM-datatyp som beskriver platsen för en observerad händelse, inklusive intressepunktsinformation och geografiska koordinater.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Beskriver information om POI-interaktionen (point-of-interest). |
| `activePOIs` | Array med [[!UICONTROL Point of interest details]](./poi-details.md) | Beskriver de POI:er som orsakade händelsen. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beskriver den geografiska plats där upplevelsen levererades. |
| `localTime` | DateTime | En tidsstämpel i [RFC 339](https://tools.ietf.org/html/rfc3339) -format som anger lokal tid med en angiven tidszonsförskjutning. Formateringsmönstret är `yyyy-MM-dd'T'HH:mm:ssXXX` (till exempel `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Heltal | Den aktuella lokala tidszonsförskjutningen i minuter från UTC för `localTime` värdet. Detta bör inkludera aktuell DST-förskjutning om tillämpligt. |

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)