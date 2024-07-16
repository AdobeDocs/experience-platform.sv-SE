---
title: Typ av implementeringsinformation
description: Lär dig mer om implementeringsinformation, datatypen Experience Data Model (XDM).
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 1%

---

# Datatypen [!UICONTROL Implementation details]

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
