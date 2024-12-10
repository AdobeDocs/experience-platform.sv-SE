---
title: Kodbar koncept, datatyp
description: Läs mer om datatypen XDM (Codeable Concept Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 1%

---

# Datatypen [!UICONTROL Codeable Concept]

[!UICONTROL Codeable Concept] är en XDM-datatyp (Standard Experience Data Model) som beskriver en referens från en resurs till en annan. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Struktur för datatypen Codeable Concept](../../../images/healthcare/data-types/codeable-concept.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Coding] | `coding` | Array med [[!UICONTROL Coding]](../data-types/coding.md) | Kod definierad av ett terminologiskt system. |
| [!UICONTROL Text] | `text` | Sträng | Konceptets rena textbeteckning. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
