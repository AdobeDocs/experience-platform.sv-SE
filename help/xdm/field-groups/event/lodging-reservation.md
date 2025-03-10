---
keywords: Experience Platform;hem;populära ämnen;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;reservation;placing;
title: Fältgruppen Bokningsreservationsschema
description: Läs mer om schemafältgruppen Bokningsreservation.
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Lodging Reservation]

[!UICONTROL Lodging Reservation] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att samla in information om en reservation för inkvartering.

Fältgruppen är ett tillägg till fältgruppen [!UICONTROL Reservation Details] och innehåller alla samma fält under ett enskilt fält av objekttyp, `reservations`. Förutom dessa generiska fält innehåller [!UICONTROL Lodging Reservation] även `lodgingReservations`-matris. Den här arrayen med objekt används för att beskriva en eller flera reservationer med egenskaper som är unika för inlämning.

>[!NOTE]
>
>Det här dokumentet innehåller information om arrayen `lodgingReservations`. Mer information om de andra fälten under objektet `reservations` finns i [[!UICONTROL Reservation Details] fältgruppsreferensen ](./reservation-details.md).

![Bokföringsreservationsstruktur](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` är en array med objekt som representerar en lista över bokningar. Om en reservationshändelse innehåller reservationer på flera olika hotell längs vägen för en resa, kan till exempel dessa reservationer listas som enskilda objekt under `lodgingReservations` för en enda händelse.

Strukturen för varje objekt som anges under `lodgingReservations` anges nedan.

![placingReservations-struktur](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Currency]](../../data-types/currency.md) | Det genomsnittliga dagspriset för hotellrummet. |
| `lodgingCheckIn` | Objekt | Ett objekt som beskriver incheckningsdetaljer. Innehåller följande värden:<ul><li>`digitalKey`: (heltal) Anger när en gäst väljer att använda en digital nyckel vid incheckning.</li><li>`earlyCheckInRequested`: (heltal) Anger när en gäst begär att checkas in tidigare än de normala incheckningstimmarna.</li><li>`lateCheckInRequested`: (heltal) Anger när en gäst begär att checkas in senare än de normala incheckningstimmarna.</li><li>`noRoomCheckIn`: (heltal) Det här värdet hämtas när en gäst har checkat in när det inte finns några rum tillgängliga vid den tidpunkten.</li><li>`oneRoomCheckIn`: (heltal) Det här värdet hämtas när en gäst har checkat in när det bara finns ett rum tillgängligt vid den tidpunkten.</li><li>`roomKeys`: (heltal) Antalet standardrumstangenter som anges vid incheckning.</li><li>`userSelectedRoom`: (Boolean) Anger om gästen har valt sitt rum vid incheckning.</li></ul> |
| `rackrate` | [[!UICONTROL Currency]](../../data-types/currency.md) | Kostnaden för en reservation samma dag utan föregående bokningsarrangemang. |
| `ID` | Sträng | Reservationsnummer eller identifierare. |
| `agentID` | Sträng | Det agent-ID som är kopplat till hotellbokningen. |
| `basePrice` | Sträng | Baskursen innan några rabatter läggs till. |
| `bookingID` | Sträng | Boknings-ID som hör till hotellbokningen. |
| `cancellation` | Heltal | Det här värdet hämtas när en reservation har annullerats. |
| `checkInDate` | DateTime | Incheckningsdatumet för rumsreservationen. |
| `checkOutDate` | DateTime | Utcheckningsdatumet för rumsreservationen. |
| `confirmationNumber` | Sträng | Reservationsbekräftelsenummer eller identifierare. |
| `couponCode` | Sträng | En kupongkod som är kopplad till hotellbokningen. |
| `created` | Heltal | Det här värdet hämtas när en reservation har skapats. |
| `currencyCode` | Sträng | ISO 4217-valutakoden som användes för att göra köpet. |
| `discountPercent` | Dubbel | Rabattprocenten som är associerad med bokningen. |
| `freeCancelation` | Boolean | Anger om rummet har en princip för kostnadsfri annullering. |
| `guestID` | Sträng | Gäst-ID som är associerat med hotellbokningen. |
| `length` | Heltal | Det totala antalet dagar för reservationen. |
| `loyaltyID` | Sträng | Förmånsprogram-ID för gästen som anges i reservationen. |
| `modification` | Heltal | Det här värdet hämtas när en reservation har ändrats. |
| `modificationDate` | DateTime | Tidpunkten när reservationen senast ändrades. |
| `numberOfAdults` | Heltal | Antalet vuxna som är associerade med reservationen. |
| `numberOfChildren` | Heltal | Antalet underordnade som är associerade med reservationen. |
| `numberOfRooms` | Heltal | Antalet rum som är associerade med reservationen. |
| `propertyID` | Sträng | En identifierare för hotellet eller en hotell för bokningen. |
| `propertyName` | Sträng | Namnet på hotellet eller orten för bokningen. |
| `purpose` | Sträng | Syftet med reservationen, vanligtvis antingen affärsmässig eller personlig. |
| `ratePlan` | Sträng | Kursen som rummet såldes på. |
| `refundable` | Boolean | Anger om rummet är återbetalningsbart. |
| `reservationStatus` | Sträng | Reservationens status. |
| `roomAccessibilityType` | Sträng | Rummets hjälpmedelstyp, till exempel mobilitet, hörsel eller annat. |
| `roomCapacity` | Heltal | Antalet personer som hotellrummet innehåller. |
| `roomType` | Sträng | Typ av rum som reserveras. |
| `smoking` | Boolean | Anger om rummet tillåter rökning. |
| `tripType` | Sträng | Anger om reservationen gäller en enkelriktad resa, en rundtur eller en flerstadstrafik. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
