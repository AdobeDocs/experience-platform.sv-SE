---
title: Datatyp för nyckelvärdepar
description: Det här dokumentet innehåller en översikt över datatypen XDM (Key Value Pair Experience Data Model).
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 2%

---

# [!UICONTROL Key Value Pair] datatyp

[!UICONTROL Key Value Pair] är en XDM-datatyp (Standard Experience Data Model) som samlar in information om ett generiskt nyckelvärdepar. Den här datatypen används i [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension] fältgrupp](../field-groups/event/analytics-full-extension.md) för att beskriva arrayobjekten i en listvariabel.

![Key Value Pair Structure](../images/data-types/key-value-pair.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `key` | Sträng | En nyckel (namn) för en allmän variabel eller ett allmänt värde. |
| `value` | Sträng | Variabelns värde. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
