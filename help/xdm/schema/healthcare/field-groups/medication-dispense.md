---
title: Fältgrupp för medicineringsdispens
description: Läs mer om schemafältgruppen för medicineringsundantag.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e897c4e0-23ad-4d79-834f-cfbe2dbec771
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Medication Dispense]

[!UICONTROL Medication Dispense] är en standardschemafältgrupp för [[!DNL Medication] klass](../../../classes/medication.md), [[!DNL XDM Individual Profile] klass](../../../classes/individual-profile.md) och [[!DNL Provider class]](../../../classes/provider.md). Det tillhandahåller ett enskilt objekttypsfält `healthcareMedicationDispense` som samlar in information om ett läkemedel som ska eller har lämnats ut för en namngiven person/patient.

![Fältgruppsstruktur](../../../images/healthcare/field-groups/medication-dispense/medication-dispense.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Authorizing Prescription] | `authorizingPrescription` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Beställningen som tillåter utlämnande av receptet. |
| [!UICONTROL Based On] | `basedOn` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Planen för utlämning av läkemedlet baseras på. |
| [!UICONTROL Category] | `category` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Den kategori som medicinen lämnas ut tillhör, t.ex. den rättsliga kategorin för medicinen eller läkemedelsklassificeringen. |
| [!UICONTROL Days Supply] | `daysSupply` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | Det antal dagar patienten ska få behandling med läkemedlet. |
| [!UICONTROL Destintation] | `destination` | [[!UICONTROL Reference]](../data-types/reference.md) | Anläggningen eller platsen dit medicineringen levererades eller kommer att levereras som en del av utlösningshändelsen. |
| [!UICONTROL Dosage Instruction] | `dosageInstruction` | Array med [[!UICONTROL Dosage]](../data-types/dosage.md) | Beskriver hur patienten ska använda läkemedlet. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Reference]](../data-types/reference.md) | Den upptäckter som anger kontexten för den här händelsen. |
| [!UICONTROL Event History] | `eventHistory` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | En sammanfattning av de händelser som inträffade runt dispensionen. |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | Identifierare som är associerade med utdelningen. Identifierarna ska definieras av affärsprocesser och/eller användas för att referera till dem när en direkt URL-referens inte är lämplig. |
| [!UICONTROL Location] | `location` | [[!UICONTROL Reference]](../data-types/reference.md) | Den huvudsakliga fysiska platsen där läkemedlet lämnas ut. |
| [!UICONTROL Medication] | `medication` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Identifierar det läkemedel som begärs. Detta bör vara en länk till en resurs som representerar detaljer om medicineringen, eller en kod som identifierar medicineringen. |
| [!UICONTROL Not Performed Reason] | `notPerformedReason` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Orsaken till varför läkemedlet inte lämnas ut. |
| [!UICONTROL Note] | `note` | Array med [[!UICONTROL Annotation]](../data-types/annotation.md) | Ytterligare information om utskänkningen. |
| [!UICONTROL Part Of] | `partOf` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Det förfarande eller den medicineringsbegäran som utlöste dispensionen. |
| [!UICONTROL Performer] | `performer` | Array med objekt | Anger vem eller vad som utförde dispeneringshändelsen. Mer information finns i avsnittet [nedan](#performer). |
| [!UICONTROL Quantity] | `quantity` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | Mängden läkemedel som har uteslutits, inklusive måttenhet. |
| [!UICONTROL Receiver] | `receiver` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Identifierar den person som tog upp medicineringen eller platsen där medicineringen levererades. |
| [!UICONTROL Subject] | `subject` | [[!UICONTROL Reference]](../data-types/reference.md) | En länk till en resurs som representerar den person eller grupp som läkemedlet ska ges till. |
| [!UICONTROL Substitution] | `substitution` | Objekt | Anger om ersättning gjordes som en del av rabatten eller inte. Innehåller fyra egenskaper: <li>`wasSubstituted`: Ett booleskt värde som är true om behållaren begärde en ersättning.</li> <li>`type`: Ett [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md)-värde som innehåller en kod som anger om en ersättning har gjorts.</li> <li>`reason`: En array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) värden som innehåller orsaken/orsakerna till ersättningen.</li> <li>`responsibleParty`: Ett [[!UICONTROL Reference]](../data-types/reference.md)-värde som anger den person eller part som är ansvarig för ersättningen. </li> |
| [!UICONTROL Supporting Information] | `supportingInformation` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Ytterligare information som stödjer läkemedlet som lämnas ut. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beskriver den typ av utgivningshändelse som utförs, t.ex. en nödfyllning eller delvis ifyllning. |
| [!UICONTROL Recorded] | `recorded` | DateTime | Det datum och den tid då utdelningsaktiviteten startades om `whenPrepared` eller `whenHandedOver` inte fylls i. |
| [!UICONTROL Rendered Dosage Instruction] | `renderedDosageInstruction` | Sträng | En fullständig representation av dosen finns i alla doseringsanvisningar. Ska användas när flera doseringsanvisningar ingår för att representera komplex dosering såsom dosökning eller nedtrappning. |
| [!UICONTROL Status] | `status` | Sträng | Status för utskänkningen. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Status Changed] | `statusChanged` | DateTime | Datum och tid då utdelningspostens status ändrades. |
| [!UICONTROL When Handed Over] | `whenHandedOver` | DateTime | Datum och tid då läkemedlet gavs till patienten. |
| [!UICONTROL When Prepared] | `whenPrepared` | DateTime | Datum och tid då läkemedlet förpackades och granskades. |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![utförarstruktur](../../../images/healthcare/field-groups/medication-dispense/performer.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | [[!UICONTROL Reference]](../data-types/reference.md) | Den behandlare (eller liknande) som utförde åtgärden. Man bör anta att skådespelaren är läkemedelsbehållaren. |
| [!UICONTROL Function] | `function` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Typ av utförare i dispositionen, t.ex. datumangivelse, paketerare eller slutlig kontroll. |
