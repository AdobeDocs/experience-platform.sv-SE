---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;reservation;matning;
title: Fältgrupp för matreservationsschema
description: Läs mer om schemafältgruppen Dining Reservation.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Dining Reservation]

[!UICONTROL Dining Reservation] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att hämta information om en matningsreservation.

Fältgruppen är ett tillägg till fältgruppen [!UICONTROL Reservation Details] och innehåller alla samma fält under ett enskilt fält av objekttyp, `reservations`. Förutom dessa generiska fält innehåller [!UICONTROL Dining Reservation] även `diningReservations`-matris. Den här arrayen med objekt används för att beskriva en eller flera reservationer med restaurangspecifika egenskaper.

>[!NOTE]
>
>Det här dokumentet innehåller information om arrayen `diningReservations`. Mer information om de andra fälten under objektet `reservations` finns i [[!UICONTROL Reservation Details] fältgruppsreferensen ](./reservation-details.md).

![Reservationsstruktur vid matning](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` är en array med objekt som representerar en lista med matsalternativ. Om en reservationshändelse innehåller reservationer på flera olika restauranger vid olika tidpunkter på dagen, kan till exempel dessa reservationer listas som enskilda objekt under `diningReservations` för en enda händelse.

Strukturen för varje objekt som anges under `diningReservations` anges nedan.

![struktur för diningReservations](../../images/field-groups/dining-reservation/diningReservations.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `ID` | Sträng | Reservationsnummer eller identifierare. |
| `cancellation` | Heltal | Det här värdet hämtas när en reservation har annullerats. |
| `confirmationNumber` | Sträng | Reservationsbekräftelsenummer eller identifierare. |
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
