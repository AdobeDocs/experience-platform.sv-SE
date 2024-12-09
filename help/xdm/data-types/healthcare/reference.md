---
title: Referensdatatyp
description: Läs mer om datatypen XDM (Reference Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Datatypen [!UICONTROL Reference]

[!UICONTROL Reference] är en XDM-datatyp (Standard Experience Data Model) som ger en referens från en resurs till en annan. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Referensdatatypstruktur](../../images/data-types/healthcare/reference.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Identifier] | `identifier` | [[!UICONTROL Identifier]](../healthcare/identifier.md) | Den logiska referensen när den litterala referensen inte är känd. |
| [!UICONTROL Display] | `display` | Sträng | Textalternativet för referensen. |
| [!UICONTROL Reference] | `reference` | Sträng | Den literala referensen, relativ, intern eller absolut URL. |
| [!UICONTROL Type] | `type` | Sträng | Den typ som referensen refererar till, angiven som en URI. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
