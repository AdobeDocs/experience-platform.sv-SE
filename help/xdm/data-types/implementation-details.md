---
title: Typ av implementeringsinformation
description: Det här dokumentet innehåller en översikt över datatypen Experience Data Model (XDM) för implementeringsinformation.
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '120'
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

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
