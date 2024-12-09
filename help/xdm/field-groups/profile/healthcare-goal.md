---
title: Målschemafältgrupp
description: Läs mer om målschemafältgruppen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 68fa7ea5de1629886cc9ba3d5c8efd4e5d57d4b3
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Goal]

[!UICONTROL Goal] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md) och [[!DNL Provider class]](../../classes/provider.md). Det tillhandahåller ett enskilt objekttypsfält `healthcareGoal` som beskriver det avsedda målet/de avsedda målen för en patient, grupp eller organisationsvård.

![Fältgruppsstruktur](../../images/field-groups/healthcare-goal/goal.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Achievment Status] | `achievementStatus` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Beskriver utvecklingen, eller bristen på dem, mot målet mot målet. |
| [!UICONTROL Addresses] | `addresses` | Array med [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De villkor och andra hälsoregisterelement som målet är avsett att hantera. |
| [!UICONTROL Category] | `category` | Array med [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Anger en kategori som målet finns i, till exempel kost eller beteende. |
| [!UICONTROL Description] | `description` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Koden eller texten som beskriver målet. |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Affärsidentifierare som tilldelats detta mål av utföraren eller andra system som förblir konstanta när resursen uppdateras och sprids från server till server. |
| [!UICONTROL Note] | `note` | Array med [[!UICONTROL Annotation]](../../data-types/healthcare/annotation.md) | Kommentarer om målet. |
| [!UICONTROL Outcome] | `outcome` | Array med [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Identifierar ändringen (eller brist på förändring) när målets status bedöms. |
| [!UICONTROL Priority] | `priority` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Identifierar den ömsesidigt överenskomna prioritetsnivå som är kopplad till att uppnå eller upprätthålla målet. |
| [!UICONTROL Source] | `source` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Anger källan till målet, t.ex. patienten eller behandlaren. |
| [!UICONTROL Start Codeable Concept] | `startCodeableConcept` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Den händelse efter vilken målet ska övertalas. |
| [!UICONTROL Subject |]`subject` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Identifierar den patient, grupp eller organisation som målet ska fastställas för. |
| [!UICONTROL Target] | `target` | Array med objekt | Anger tidslinjen för specifika steg i målet. Mer information finns i avsnittet [nedan](#target). |
| [!UICONTROL Continous] | `continous` | Boolean | Anger om det efter att målet har uppnåtts krävs en pågående aktivitet för att upprätthålla målet. |
| [!UICONTROL Lifecycle Status] | `lifecycleStatus` | Sträng | Status för målets livscykel. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL Start Date] | `startDate` | Datum | Det datum efter vilket målet ska börja eftersträvas. |
| [!UICONTROL Status Date] | `statusDate` | Datum | Identifierar när statusen skapades. |
| [!UICONTROL Status Reason] | `statusReason` | Sträng | Hämtar orsaken till den aktuella statusen. |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![målstruktur](../../images/field-groups/healthcare-goal/target.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Detail Codeable Concept] | `detailCodeableConcept` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Den målkod som ska uppnås för att ange att målet har uppfyllts. |
| [!UICONTROL Detail Quantity] | `detailQuantity` | [[!UICONTROL Quantity]](../../data-types/healthcare/quantity.md) | Den målkvantitet som ska uppnås för att ange att målet har uppfyllts. |
| [!UICONTROL Detail Range] | `detailRange` | [[!UICONTROL Range]](../../data-types/healthcare/range.md) | Det målintervall som ska uppnås för att ange att målet har uppnåtts. |
| [!UICONTROL Detail Ratio] | `detailRatio` | [[!UICONTROL Ratio]](../../data-types/healthcare/ratio.md) | Den målkvot som ska uppnås för att ange att målet har uppnåtts. |
| [!UICONTROL Measure] | `measure` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Parametern som är ett värde spåras. |
| [!UICONTROL Detail Boolean] | `detailBoolean` | Boolean | Anger att målet har uppfyllts. |
| [!UICONTROL Detail Integer] | `detailInteger` | Heltal | Det målnummer som ska uppnås för att ange att målet har uppnåtts. |
| [!UICONTROL Detail String] | `detailString` | Sträng | Det målvärde som ska uppnås för att ange att målet har uppnåtts. |
| [!UICONTROL Due Date] | `dueDate` | Datum | Det datum då målet ska vara uppfyllt. |
