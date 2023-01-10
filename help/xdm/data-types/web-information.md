---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;Webbsidesinformation;datatyp;datatyp;webbsida
solution: Experience Platform
title: Webbinformationsdatatyp
description: Det här dokumentet innehåller en översikt över datatypen Experience Data Model (XDM) för webbinformation.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
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
