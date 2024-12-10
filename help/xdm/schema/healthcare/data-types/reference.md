---
title: Referensdatatyp
description: Läs mer om datatypen XDM (Reference Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: eb724dbb-2918-43b5-8e50-c8aabfe6e96c
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Datatypen [!UICONTROL Reference]

[!UICONTROL Reference] är en XDM-datatyp (Standard Experience Data Model) som ger en referens från en resurs till en annan. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Referensdatatypstruktur](../../../images/healthcare/data-types/reference.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Identifier] | `identifier` | [[!UICONTROL Identifier]](../data-types/identifier.md) | Den logiska referensen när den litterala referensen inte är känd. |
| [!UICONTROL Display] | `display` | Sträng | Textalternativet för referensen. |
| [!UICONTROL Reference] | `reference` | Sträng | Den literala referensen, relativ, intern eller absolut URL. |
| [!UICONTROL Type] | `type` | Sträng | Den typ som referensen refererar till, angiven som en URI. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
