---
title: Kodad referensdatatyp
description: Läs mer om datatypen XDM (Codeable Reference Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 1%

---

# Datatypen [!UICONTROL Codeable Reference]

[!UICONTROL Codeable Reference] är en XDM-datatyp (Standard Experience Data Model) som beskriver en referens till en resurs eller ett koncept. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypsstruktur för kodningsbar referens](../../../images/healthcare/data-types/codeable-reference.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Concept] | `concept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | En referens till ett koncept (efter klass). |
| [!UICONTROL Reference] | `reference` | [[!UICONTROL Reference]](../data-types/reference.md) | En referens till en resurs. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
