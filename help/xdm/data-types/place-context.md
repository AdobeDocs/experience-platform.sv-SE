---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;place context;placeContext;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Montera kontextdatatyp
description: Läs mer om datatypen Place Context XDM.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Datatypen [!UICONTROL Place context]

[!UICONTROL Place context] är en standard-XDM-datatyp som beskriver platsen för en observerad händelse, inklusive intressepunktsinformation och geografiska koordinater.

![](../images/data-types/place-context.png){width=500}

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Beskriver information om POI-interaktionen (point-of-interest). |
| `activePOIs` | Array med [[!UICONTROL Point of interest details]](./poi-details.md) | Beskriver de POI:er som orsakade händelsen. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beskriver den geografiska plats där upplevelsen levererades. |
| `localTime` | DateTime | En tidsstämpel i formatet [RFC 339](https://tools.ietf.org/html/rfc3339) som anger lokal tid med en angiven tidszonsförskjutning. Formateringsmönstret är `yyyy-MM-dd'T'HH:mm:ssXXX` (till exempel `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Heltal | Den aktuella lokala tidszonsförskjutningen i minuter från UTC för värdet `localTime`. Detta bör inkludera aktuell DST-förskjutning om tillämpligt. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
