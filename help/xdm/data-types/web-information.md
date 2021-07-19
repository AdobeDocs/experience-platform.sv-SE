---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;Webbsidesinformation;datatyp;datatyp;webbsida
solution: Experience Platform
title: Webbinformationsdatatyp
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över datatypen Experience Data Model (XDM) för webbinformation.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# [!UICONTROL Web information] datatyp

[!UICONTROL Web information] är en XDM-datatyp (Standard Experience Data Model) som beskriver information som spelats in via en Experience Event som är specifik för webbkanalen, inklusive webbsidan, referenten och/eller länken som relaterar till interaktionen på sidan.

![](../images/data-types/web-information.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Web interaction]](./web-interaction.md) | Beskriver informationen om den webblänk eller URL som motsvarar interaktionen. |
| `webPageDetails` | [[!UICONTROL Web page details]](./webpage-details.md) | Beskriver information om webbsidan där webbinteraktionen inträffade. |
| `webReferrer` | [!UICONTROL Object] | Beskriver referenten till en webbinteraktion, vilket är den URL som en besökare kom från omedelbart innan den aktuella webbinteraktionen spelades in. Innehåller följande underegenskaper: <ul><li>`URL`: Referentens-URL.</li><li>`type`: Referenstypen.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
