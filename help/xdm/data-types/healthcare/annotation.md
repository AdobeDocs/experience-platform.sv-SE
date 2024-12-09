---
title: Anteckningsdatatyp
description: Läs mer om datatypen XDM (Annotation Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Datatypen [!UICONTROL Annotation]

[!UICONTROL Annotation] är en XDM-datatyp (Standard Experience Data Model) som innehåller en textnod med attribut till författaren. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Anteckningens datatypstruktur](../../images/data-types/healthcare/annotation.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Author Reference] | `authorReference` | [[!UICONTROL Reference]](../healthcare/reference.md) | En referens till författaren. |
| [!UICONTROL Author] | `authorString` | Sträng | Den person som är ansvarig för anteckningen. |
| [!UICONTROL Text] | `text` | Sträng | Innehållet i anteckningen. |
| [!UICONTROL Time] | `time` | DateTime | När anteckningen gjordes. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
