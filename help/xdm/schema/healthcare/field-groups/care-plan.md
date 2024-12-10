---
title: Fältgrupp för vårdplansschema
description: Läs mer om fältgruppen för schemat för serviceplan.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e6cbf44f-6c39-42bd-b083-a975860a64db
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Care Plan]

[!UICONTROL Care Plan] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../../classes/individual-profile.md). Det tillhandahåller ett enskilt objekttypsfält `healthcareCarePlan` som fångar en vårdplan för en patient eller grupp.

![Fältgruppsstruktur](../../../images/healthcare/field-groups/care-plan/care-plan.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Activity] | `activity` | Array med objekt | Identifierar en åtgärd som har inträffat eller planeras inträffa som en del av planen. Mer information finns i avsnittet [nedan](#activity). |
| [!UICONTROL Addresses] | `addresses` | Array med [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Identifierar villkoren eller bekymren som vårdplanen hanterar. |
| [!UICONTROL Based On] | `basedOn` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | En begäranderesurs på högre nivå som helt eller delvis fullföljs av denna vårdplan. |
| [!UICONTROL Care Team] | `careTeam` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Identifierar alla personer och organisationer som förväntas delta i den vård som avses i den här planen. |
| [!UICONTROL Category] | `category` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Identifierar vilken typ av plan detta är för att stödja differentiering mellan flera samtidiga planer. |
| [!UICONTROL Contributor] | `contributor` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Identifierar den eller de personer, organisationer eller enheter som tillhandahöll innehållet i vårdplanen. |
| [!UICONTROL Custodian] | `custodian` | [[!UICONTROL Reference]](../data-types/reference.md) | När det är ifyllt är förvaringsinstitutet ansvarigt för och hänfört till vårdplanen. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Reference]](../data-types/reference.md) | Den upptäckt under vilken vårdplanen skapades. |
| [!UICONTROL Goal] | `goal` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Planens syfte eller syften. |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | Affärsidentifierare som tilldelats den här vårdplanen av utföraren eller andra system som förblir konstanta när resursen uppdateras och sprids från server till server. |
| [!UICONTROL Note] | `note` | Array med [[!UICONTROL Annotation]](../data-types/annotation.md) | Allmänna anmärkningar om vårdplanen som inte ingår i andra attribut. |
| [!UICONTROL Part Of] | `partOf` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Den större vårdplan där denna särskilda vårdplan är en komponent eller ett steg. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Anger när planen trädde i kraft (eller är avsedd att träda i kraft) och när den upphör. |
| [!UICONTROL Replaces] | `replaces` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Den färdiga eller avslutade vårdplan vars funktion övertas av denna vårdplan. |
| [!UICONTROL Subject] | `subject` | [[!UICONTROL Reference]](../data-types/reference.md) | Identifierar den patient eller grupp vars tänkta vård beskrivs i planen. |
| [!UICONTROL Supporting Info] | `supportingInfo` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Identifierar delar av patientens register som påverkade planens utformning. Det kan vara storheter, nyligen använda procedurer, begränsningar eller nyligen gjorda bedömningar. |
| [!UICONTROL Created] | `created` | DateTime | Representerar när den här vårdplanen skapades i systemet, vilket ofta är ett systemgenererat datum. |
| [!UICONTROL Description] | `description` | Sträng | En beskrivning av planens omfattning och karaktär. |
| [!UICONTROL Instantiates Canonical] | `instantiatesCanonical` | Array med strängar | Den URL som pekar på ett FHIR-definierat protokoll, riktlinjer, enkät eller annan definition som helt eller delvis följs av denna plan. |
| [!UICONTROL Instantiates Uri] | `instantiatesUri` | Array med strängar | Den URL som pekar på ett externt underhållet protokoll, riktlinjer, frågeformulär eller någon annan definition som helt eller delvis följs av den här planen, representeras som en URI. |
| [!UICONTROL Intent] | `intent` | Sträng | Vårdplanens syfte. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL Status] | `status` | Sträng | Vårdplanens status. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL Title] | `title` | Sträng | Vårdplanens namn. |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![aktivitetsstruktur](../../../images/healthcare/field-groups/care-plan/activity.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Performed Activity] | `performedActivity` | Array med [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Resultatet av aktiviteten, till exempel ett möte eller ett förfarande. |
| [!UICONTROL Planned Activity Reference] | `plannedActivityReference` | [[!UICONTROL Reference]](../data-types/reference.md) | Detaljerad information om den föreslagna aktiviteten. |
| [!UICONTROL Progress] | `progress` | Array med [[!UICONTROL Annotation]](../data-types/annotation.md) | Anteckningar om aktivitetens följsamhet, status eller förlopp. |
