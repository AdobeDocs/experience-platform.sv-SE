---
title: Datatypen Förhållande
description: Läs mer om datatypen XDM (Ratio Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Datatypen [!UICONTROL Ratio]

[!UICONTROL Ratio] är en XDM-datatyp (Standard Experience Data Model) som ger en kvot på två [[!UICONTROL Quantity]](../healthcare/quantity.md)-värden genom en täljare och en nämnare. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Struktur för datatypen Ratio](../../images/data-types/healthcare/ratio.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Denominator] | `denominator` | [[!UICONTROL Simple Quantity]](../healthcare/simple-quantity.md) | Nämnarens värde. |
| [!UICONTROL Numerator] | `numerator` | [[!UICONTROL Quantity]](../healthcare/quantity.md) | Täljarens värde. |

>[!NOTE]
>
> `denominator` och `numerator` har olika datatyper på grund av den specifikation som skapades enligt HL7 FHIR version 5.

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
