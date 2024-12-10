---
title: Anteckningsdatatyp
description: Läs mer om datatypen XDM (Annotation Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Datatypen [!UICONTROL Annotation]

[!UICONTROL Annotation] är en XDM-datatyp (Standard Experience Data Model) som innehåller en textnod med attribut till författaren. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Anteckningens datatypstruktur](../../../images/healthcare/data-types/annotation.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Author Reference] | `authorReference` | [[!UICONTROL Reference]](../data-types/reference.md) | En referens till författaren. |
| [!UICONTROL Author] | `authorString` | Sträng | Den person som är ansvarig för anteckningen. |
| [!UICONTROL Text] | `text` | Sträng | Innehållet i anteckningen. |
| [!UICONTROL Time] | `time` | DateTime | När anteckningen gjordes. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
