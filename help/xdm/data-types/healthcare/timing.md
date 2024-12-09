---
title: Datatyp för timing
description: Läs mer om datatypen XDM (Timing Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 0640d0c2daab67ad7a77d3265ccae45851ba45b8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Datatypen [!UICONTROL Timing]

[!UICONTROL Timing] är en XDM-datatyp (Standard Experience Data Model) som beskriver ett timingschema som ger information om en händelse som kan inträffa flera gånger. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypsstruktur för timing](../../images/data-types/healthcare/timing.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Event] | `event` | Matris med DateTime | När händelsen inträffar. |
| [!UICONTROL Repeat] | `repeat` | [[!UICONTROL Repeat]](../healthcare/repeat.md) | Information om när händelsen inträffar. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | Koden som relaterar till händelsen. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
