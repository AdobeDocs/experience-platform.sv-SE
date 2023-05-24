---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;reservation;matning;
title: Fältgrupp för matreservationsschema
description: Det här dokumentet innehåller en översikt över schemafältgruppen Dining Reservation.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# [!UICONTROL Dining Reservation] schemafältgrupp

[!UICONTROL Dining Reservation] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) används för att samla in information om en matreservation.

Fältgruppen är ett tillägg till [!UICONTROL Reservation Details] fältgrupp och innehåller alla samma fält under ett enda fält av objekttyp, `reservations`. Förutom dessa allmänna fält [!UICONTROL Dining Reservation] innehåller `diningReservations` array. Den här arrayen med objekt används för att beskriva en eller flera reservationer med restaurangspecifika egenskaper.

>[!NOTE]
>
>Det här dokumentet innehåller information om `diningReservations` array. För information om andra fält som anges i `reservations` objekt, se [[!UICONTROL Reservation Details] fältgruppsreferens](./reservation-details.md).

![Reservationsstruktur för matning](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` är en array med objekt som representerar en lista med matsalternativ. Om en bokningshändelse innehåller reservationer på flera olika restauranger vid olika tidpunkter på dagen, kan exempelvis dessa reservationer listas som enskilda objekt under `diningReservations` för en enda händelse.

Strukturen för varje objekt som anges under `diningReservations` anges nedan.

![diningReservations-struktur](../../images/field-groups/dining-reservation/diningReservations.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `ID` | Sträng | Reservationsnumret eller identifieraren. |
| `cancellation` | Heltal | Det här värdet hämtas när en reservation har annullerats. |
| `confirmationNumber` | Sträng | Reservationsbekräftelsenumret eller identifieraren. |
| `created` | Heltal | Det här värdet hämtas när en reservation har skapats. |
| `cuisine` | Heltal | Typ av restaurangmateri. |
| `currencyCode` | Sträng | ISO 4217-valutakoden som användes för att göra köpet. |
| `deliveryPartners` | Sträng | Leveranspartners finns på restaurangen. |
| `diningOptions` | Sträng | Leverans och matsalternativ finns på restaurangen. |
| `groupReservation` | Boolean | Anger om reservationen görs för en grupp. |
| `length` | Heltal | Det totala antalet dagar för reservationen. |
| `loyaltyID` | Sträng | Förmånsprogram-ID för gästen som anges i reservationen. |
| `modification` | Heltal | Det här värdet hämtas när en reservation har ändrats. |
| `modificationDate` | DateTime | Tidpunkten när reservationen senast ändrades. |
| `numberOfAdults` | Heltal | Antalet vuxna som är associerade med reservationen. |
| `numberOfChildren` | Heltal | Antalet underordnade som är associerade med reservationen. |
| `numberOfRooms` | Heltal | Antalet rum som är associerade med reservationen. |
| `partySize` | Heltal | Antalet individer på matfesten. |
| `priceCategory` | Sträng | Priskategorin för reservationen som görs. |
| `purpose` | Sträng | Syftet med reservationen, vanligtvis antingen affärsmässig eller personlig. |
| `reservationTime` | DateTime | Den tidpunkt då matreservationen bokförs. |
| `restaurantID` | Sträng | En identifierare för restaurangen eller matplatsen. |
| `reservationStatus` | Sträng | Reservationens status. |
| `specialOccasion` | Boolean | Anger om reservationen görs för ett särskilt tillfälle. |
| `status` | Heltal | Status för matreservationen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
