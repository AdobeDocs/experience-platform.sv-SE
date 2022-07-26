---
title: Typ av implementeringsinformation
description: Det här dokumentet innehåller en översikt över datatypen Experience Data Model (XDM) för implementeringsinformation.
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 3%

---

# [!UICONTROL Implementation details] datatyp

[!UICONTROL Implementation details] är en XDM-datatyp (Standard Experience Data Model) som beskriver en teknikimplementering, till exempel ett API eller en SDK.

![Datatypstruktur](../images/data-types/implementation-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `environment` | Sträng | Implementeringens miljö. |
| `name` | Sträng | Identifieraren för SDK eller slutpunkten. Alla SDK:er eller slutpunkter identifieras via en URI, inklusive tillägg. |
| `version` | Sträng | Versionen av API eller SDK. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
