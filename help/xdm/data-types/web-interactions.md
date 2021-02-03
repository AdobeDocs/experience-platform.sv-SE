---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;webbinaktion;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Webbinteraktionsdatatyp
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen Experience Data Model (XDM) för webbinteraktion.
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 2%

---


# [!UICONTROL Web interaction] datatyp

[!UICONTROL Web interaction] är en XDM-datatyp (Standard Experience Data Model) som beskriver information om interaktioner som inträffade på en webbsida efter att den första sidinläsningen slutfördes. Den är avsedd för inspelning av interaktioner i webbprogram som inte aktiverar en ny sidinläsning, t.ex. ett webbprogram (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Measure]](./measure.md) | Ett mått som spårar klickningen på en webblänk. |
| `URL` | Sträng | Den faktiska länken eller URL-adressen som används för den här webbinteraktionen. |
| `name` | Sträng | Det normativa namn som används för den här webblänken. Detta används i klassificeringssyfte. |
| `type` | Sträng | Länktypen. Den här egenskapen måste vara lika med ett av följande enum-värden: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)