---
title: Intervalldatatyp
description: Läs mer om datatypen XDM (Range Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# Datatypen [!UICONTROL Range]

[!UICONTROL Range] är en XDM-datatyp (Standard Experience Data Model) som tillhandahåller en uppsättning värden som är bundna av låga och höga värden. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Struktur för intervalldatatyp](../../images/data-types/healthcare/range.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL High] | `high` | [[!UICONTROL Simple Quantity]](../healthcare/simple-quantity.md) | Den högsta gränsen. |
| [!UICONTROL Low] | `low` | [[!UICONTROL Simple Quantity]](../healthcare/simple-quantity.md) | Den lägsta gränsen. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)
