---
title: Identifierardatatyp
description: Läs mer om datatypen XDM (Identifier Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Datatypen [!UICONTROL Identifier]

[!UICONTROL Identifier] är en XDM-datatyp (Standard Experience Data Model) som ger en identifierare som är avsedd för beräkning. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Identifierarens datatypstruktur](../../images/data-types/healthcare/identifier.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../healthcare/period.md) | Den tidsperiod då ID:t är eller var giltigt för användning. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | Beskrivning av identifieraren. |
| [!UICONTROL Assigner] | `assigner` | Sträng | Organisationen som utfärdade ID:t. |
| [!UICONTROL System] | `system` | Sträng | Namnutrymmet för identifierarvärdet, representerat som en URI. |
| [!UICONTROL Use] | `use` | Sträng | Användning av identifieraren. Värdena för den här egenskapen måste vara lika med ett eller flera av följande kända enum-värden. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL Value] | `value` | Sträng | ID:ts unika värde. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)
