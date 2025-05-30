---
title: Fältgrupp för medicinschema
description: Lär dig mer om schemafältgruppen Medication.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1f53ff8-3079-4b2f-9e73-31a773907a63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Medication]

[!UICONTROL Medication] är en standardschemafältgrupp för [[!DNL Medication] klassen](../../../classes/medication.md). Det tillhandahåller ett enskilt objekttypsfält `healthcareMedication` som hämtar information om en medicin.

![Fältgruppsstruktur](../../../images/healthcare/field-groups/medication/medication.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| ---|  --- | --- | --- |
| [!UICONTROL Batch] | `batch` | Objekt | Information om paketerad medicin. Innehåller två egenskaper: <li>`lotNumber`: Ett strängvärde för identifieraren som tilldelats till gruppen.</li> <li>`expirationDate`: Ett DateTime-värde för när batchen upphör att gälla.</li> |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Koden som identifierar detta läkemedel. |
| [!UICONTROL Definition] | `definition` | [[!UICONTROL Reference]](../data-types/reference.md) | Definitionen av läkemedlet. |
| [!UICONTROL Dose Form] | `doseForm` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beskriver doseringsformen av läkemedlet, såsom tabletter eller kapslar. |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | En identifierare för medicineringen. |
| [!UICONTROL Ingredient] | `ingredient` | Array med objekt | Beskriver information om ingredienser i läkemedlet. Mer information finns i avsnittet [nedan](#ingredient). |
| [!UICONTROL Marketing Authorization Holder] | `marketingAuthorizationHolder` | [[!UICONTROL Reference]](../data-types/reference.md) | Organisationen som har tillstånd att marknadsföra läkemedlet. |
| [!UICONTROL Total Volume] | `totalVolume` | [[!UICONTROL Quantity]](../data-types/quantity.md) | Mängden produkt som anges i läkemedlet när produktkoden inte avspeglar en förpackningsstorlek. |
| [!UICONTROL Status] | `status` | Sträng | Läkemedlets status. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.schema.json)

## `ingredient` {#ingredient}

`ingredient` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![komponentstruktur](../../../images/healthcare/field-groups/medication/ingredient.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Item] | `item` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Den ingrediens som beskrivs. |
| [!UICONTROL Strength Codeable Concept] | `strengthCodeableConcept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Mängden ingrediens som finns, uttryckt i en systemdefinierad terminologi. |
| [!UICONTROL Strength Quantity] | `strengthQuantity` | [[!UICONTROL Quantity]](../data-types/quantity.md) | Mängden ingrediens som finns. |
| [!UICONTROL Strength Ratio] | `strengthRatio` | [[!UICONTROL Ratio]](../data-types/ratio.md) | Förhållandet mellan beståndsdelen. |
| [!UICONTROL Is Active] | `isActive` | Boolean | Anger om ingrediensen är aktiv. |
