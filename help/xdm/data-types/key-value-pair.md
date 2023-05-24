---
title: Datatyp för nyckelvärdepar
description: Det här dokumentet innehåller en översikt över datatypen XDM (Key Value Pair Experience Data Model).
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: 1d023ce6184e54693401eb68a04ceeb1464dcaa0
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 2%

---

# [!UICONTROL Key Value Pair] datatyp

[!UICONTROL Key Value Pair] är en XDM-datatyp (Standard Experience Data Model) som samlar in information om ett generiskt nyckelvärdepar. Den här datatypen används i [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension] fältgrupp](../field-groups/event/analytics-full-extension.md) för att beskriva arrayobjekten i en listvariabel.

![Key Value Pair Structure](../images/data-types/key-value-pair.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `key` | Sträng | En nyckel (namn) för en allmän variabel eller ett allmänt värde. |
| `value` | Sträng | Variabelns värde. |

{style="table-layout:auto"}

Mer information om datatypen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
