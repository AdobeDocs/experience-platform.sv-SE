---
title: Datatyp för pengar
description: Läs mer om datatypen XDM (Money Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 1%

---

# Datatypen [!UICONTROL Money]

[!UICONTROL Money] är en XDM-datatyp (Standard Experience Data Model) som ger ett ekonomiskt värde i en viss erkänd valuta. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypsstruktur för pengar](../../images/data-types/healthcare/money.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Currency] | `currency` | Sträng | ISO 4217-valutakoden. |
| [!UICONTROL Value] | `value` | Dubbel | Det numeriska värdet. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)
