---
title: Typ av doseringsdata
description: Läs mer om datatypen XDM (Dosage Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 56eda38b-a7f7-40da-af08-73cfe9db0c7e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Datatypen [!UICONTROL Dosage]

[!UICONTROL Dosage] är en XDM-datatyp (Standard Experience Data Model) som beskriver hur medicineringen tas/ska tas. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Struktur för doseringsdatatyp](../../../images/healthcare/data-types/dosage/dosage.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Additional Instructions] | `additionalInstruction` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Ytterligare instruktioner eller varningar till patienten. |
| [!UICONTROL As Needed For] | `asNeededFor` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beskriver vilket ämne läkemedlet ska tas i vid behov. |
| [!UICONTROL Dose And Rate] | `doseAndRate` | Array med objekt | Den mängd läkemedel som administreras, ska administreras eller den typiska mängd som ska administreras. Mer information finns i avsnittet [nedan](#dose-and-rate) |
| [!UICONTROL Max Dose Per Administration] | `maxDosePerAdministration` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | Den övre gränsen för medicinering per administrering. |
| [!UICONTROL Max Dose Per Lifetime] | `maxDosePerLifetime` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | Den övre gränsen för medicinering per patientens livstid. |
| [!UICONTROL Max Dose Per Period] | `maxDosePerPeriod` | Array med [[!UICONTROL Ratio]](../data-types/ratio.md) | Den övre gränsen för medicinering per tidsenhet. |
| [!UICONTROL Method] | `method` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Metoden för administrering av läkemedlet. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Hur läkemedlet ska komma in i kroppen. |
| [!UICONTROL Body Site] | `site` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Kroppsstället för att administrera läkemedlet. |
| [!UICONTROL Timing] | `timing` | [[!UICONTROL Timing]](../data-types/timing.md) | När medicinering skall ges. |
| [!UICONTROL As Needed] | `asNeeded` | Boolean | En indikator för om läkemedlet ska tas efter behov. |
| [!UICONTROL Patient Instructions] | `patientInstruction` | Sträng | Instruktioner som ska förstås av patienten eller konsumenten. |
| [!UICONTROL Sequence] | `Integer` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Dosinstruktionernas ordning. |
| [!UICONTROL Text] | `text` | Sträng | Planera textredoseringsanvisningar. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![dos- och frekvensstruktur](../../../images/healthcare/data-types/dosage/dose-and-rate.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Dose Quantity] | `doseQuantity` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | Mängden läkemedel per dos. |
| [!UICONTROL Dose Range] | `doseRange` | [[!UICONTROL Range]](../data-types/range.md) | Mängden läkemedel per dos. |
| [!UICONTROL Rate Quantity] | `rateQuantity` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | Mängden läkemedel per tidsenhet. |
| [!UICONTROL Rate Range] | `rateRange` | [[!UICONTROL Range]](../data-types/range.md) | Mängden läkemedel per tidsenhet. |
| [!UICONTROL Rate Ratio] | `rateRatio` | [[!UICONTROL Ratio]](../data-types/ratio.md) | Mängden läkemedel per tidsenhet. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Den typ av dos eller hastighet som anges. |
