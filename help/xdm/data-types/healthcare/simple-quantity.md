---
title: Enkel datatyp för kvantitet
description: Läs mer om datatypen XDM (Simple Quantity Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Datatypen [!UICONTROL Simple Quantity]

[!UICONTROL Simple Quantity] är en XDM-datatyp (Standard Experience Data Model) som ger en mätt eller mätbar mängd. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Enkel datatypstruktur för kvantitet](../../images/data-types/healthcare/simple-quantity.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Sträng | Enhetens kodade form. |
| [!UICONTROL System] | `system` | Sträng | Det system som definierar kodad enhetsform, som representeras som en URI. |
| [!UICONTROL Unit] | `unit` | Sträng | Representationen av enheten. |
| [!UICONTROL Value] | `value` | Dubbel | Det numeriska värdet. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
