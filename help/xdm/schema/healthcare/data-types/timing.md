---
title: Datatyp för timing
description: Läs mer om datatypen XDM (Timing Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Datatypen [!UICONTROL Timing]

[!UICONTROL Timing] är en XDM-datatyp (Standard Experience Data Model) som beskriver ett timingschema som ger information om en händelse som kan inträffa flera gånger. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypsstruktur för timing](../../../images/healthcare/data-types/timing.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Event] | `event` | Matris med DateTime | När händelsen inträffar. |
| [!UICONTROL Repeat] | `repeat` | [[!UICONTROL Repeat]](../data-types/repeat.md) | Information om när händelsen inträffar. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Koden som relaterar till händelsen. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
