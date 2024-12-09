---
title: Datatyp för tillgänglighet
description: Läs mer om datatypen XDM (Availability Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Datatypen [!UICONTROL Availability]

[!UICONTROL Availability] är en XDM-datatyp (Standard Experience Data Model) som beskriver tillgänglighetsdata för ett objekt. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypsstruktur för tillgänglighet](../../images/data-types/healthcare/availability/availability.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Available Time] | `availableTime` | Array med objekt | De tider som artikeln är tillgänglig. Mer information finns i avsnittet [nedan](#available-time). |
| [!UICONTROL Not Available Time] | `notAvailableTime` | Sträng | De tider som artikeln inte är tillgänglig, med en angiven orsak. Mer information finns i avsnittet [nedan](#not-available-time). |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.schema.json)

## `availableTime` {#available-time}

`availableTime` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Tillgänglig tidsstruktur](../../images/data-types/healthcare/availability/available-time.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL All Day] | `allDay` | Boolean | Ett booleskt värde som anger om objektet alltid är tillgängligt. |
| [!UICONTROL Available End Time] | `availableEndTime` | Sträng | Den tid på dagen som objektet inte längre är tillgängligt. Detta ignoreras om `allDay` är `true`. |
| [!UICONTROL Available Start Time] | `availableStartTime` | Sträng | Den tid på dagen då objektet börjar vara tillgängligt. Detta ignoreras om `allDay` är `true`. |
| [!UICONTROL Days Of Week] | `daysOfWeek` | Array med strängar | En array med strängar som anger vilka dagar som är tillgängliga. Värdena för den här egenskapen måste vara lika med ett eller flera av följande kända enum-värden. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |

## `notAvailableTime` {#not-available-time}

`notAvailableTime` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Inte tillgänglig tidsstruktur](../../images/data-types/healthcare/availability/not-available-time.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL During] | `during` | [[!UICONTROL Period]](../healthcare/period.md) | Den tidsperiod som objektet inte längre är tillgängligt. |
| [!UICONTROL Description] | `description` | Sträng | Orsaken till att artikeln inte är tillgänglig. |
