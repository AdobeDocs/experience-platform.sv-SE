---
title: Upprepa datatyp
description: Läs mer om datatypen XDM (Repeat Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 9d40bc1d-33d1-4c33-a143-13fdcf8dc255
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Datatypen [!UICONTROL Repeat]

[!UICONTROL Repeat] är en XDM-datatyp (Standard Experience Data Model) som tillhandahåller en uppsättning regler som beskriver när en händelse är schemalagd. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Upprepa datatypsstruktur](../../../images/healthcare/data-types/reference.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Bound Period] | `boundsPeriod` | [[!UICONTROL Period]](../data-types/period.md) | Start- och sluttider. |
| [!UICONTROL Bound Range] | `boundsRange` | [[!UICONTROL Range]](../data-types/range.md) | Intervallgränsen. |
| [!UICONTROL Bound Duration] | `boundsDuration` | [[!UICONTROL Duration]](../data-types/duration.md) | Tidsgränsen. |
| [!UICONTROL Count] | `count` | Heltal | Antalet gånger som ska upprepas, med ett minimivärde på `0`. |
| [!UICONTROL Maximum Count] | `countMax` | Heltal | Maximalt antal gånger som ska upprepas, med ett minimivärde på `0`. |
| [!UICONTROL Day Of Week] | `dayOfWeek` | Array med strängar | En array med strängar som anger vilka dagar som är tillgängliga. Värdena för den här egenskapen måste vara lika med ett eller flera av följande kända enum-värden. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Duration] | `duration` | Dubbel | Tidslängden. |
| [!UICONTROL Maximum Duration] | `durationMax` | Dubbel | Maximal tid. |
| [!UICONTROL Duration Unit] | `durationUnit` | Sträng | Varaktighetsenheten. Värdena för den här egenskapen måste vara lika med ett eller flera av följande kända enum-värden. <li> `s` (sekunder) </li> <li> `min` (minuter) </li> <li> `h` (timme) </li> <li> `d` (dagligen) </li>  <li> `wk` (varje vecka) </li> <li> `mo` (månadsvis) </li> <li> `a` (årlig)</li> |
| [!UICONTROL Frequency] | `frequency` | Dubbel | Antalet upprepningar som ska inträffa inom en period, med ett minsta värde på `0`. |
| [!UICONTROL Maximum Frequency] | `frequencyMax` | Dubbel | Det maximala antalet upprepningar som ska inträffa med en punkt, med ett minsta värde på `0`. |
| [!UICONTROL Offset] | `offset` | Heltal | Minut(er) till händelsen (före eller efter). |
| [!UICONTROL Period] | `period` | Dubbel | Den varaktighet under vilken frekvensen gäller. |
| [!UICONTROL Maximum Period] | `periodMax` | Dubbel | Periodens övre gräns. |
| [!UICONTROL Period Unit] | `periodUnit` | Sträng | Tidsenheten. Värdena för den här egenskapen måste vara lika med ett eller flera av följande kända enum-värden. <li> `s` (sekunder) </li> <li> `min` (minuter) </li> <li> `h` (timme) </li> <li> `d` (dagligen) </li>  <li> `wk` (varje vecka) </li> <li> `mo` (månadsvis) </li> <li> `a` (årlig)</li> |
| [!UICONTROL Time Of Day] | `timeOfDay` | Array med strängar | Tidpunkten på dagen då åtgärden ska utföras. |
| [!UICONTROL When] | `when` | Array med strängar | Koden för åtgärdens tidsperiod. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
