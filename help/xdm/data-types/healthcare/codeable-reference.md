---
title: Kodad referensdatatyp
description: Läs mer om datatypen XDM (Codeable Reference Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 1%

---

# Datatypen [!UICONTROL Codeable Reference]

[!UICONTROL Codeable Reference] är en XDM-datatyp (Standard Experience Data Model) som beskriver en referens till en resurs eller ett koncept. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypsstruktur för kodningsbar referens](../../images/data-types/healthcare/codeable-reference.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Concept] | `concept` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | En referens till ett koncept (efter klass). |
| [!UICONTROL Reference] | `reference` | [[!UICONTROL Reference]](../healthcare/reference.md) | En referens till en resurs. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
