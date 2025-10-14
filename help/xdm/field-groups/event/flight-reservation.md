---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;reservation;flight;
title: Fältgrupp för flygbokningsschema
description: Läs mer om schemafältgruppen Flight Reservation.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Flight Reservation]

[!UICONTROL Flight Reservation] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att hämta information om en flygreservation.

Fältgruppen är ett tillägg till fältgruppen [!UICONTROL Reservation Details] och innehåller alla samma fält under ett enskilt fält av objekttyp, `reservations`. Förutom dessa generiska fält innehåller [!UICONTROL Flight Reservation] även `flightReservations`-matris. Den här objektmatrisen används för att beskriva en eller flera reservationer med egenskaper som är unika för flygresor.

>[!NOTE]
>
>Det här dokumentet innehåller information om arrayen `flightReservations`. Mer information om de andra fälten under objektet `reservations` finns i [[!UICONTROL Reservation Details] fältgruppsreferensen &#x200B;](./reservation-details.md).

![Flight Reservation-struktur](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` är en array med objekt som representerar en lista med flygreservationer. Om en reservationshändelse innehåller reservationer för flera anslutningsflygningar på en resa, kan till exempel dessa reservationer listas som enskilda objekt under `flightReservations` för en enda händelse.

Strukturen för varje objekt som anges under `flightReservations` anges nedan.

![struktur för flightReservations](../../images/field-groups/flight-reservation/flightReservations.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `flightCheckIn` | Objekt | Hämtar information om incheckningen av flygningen. Objektet innehåller följande egenskaper:<ul><li>`arrivalAirportCode`: (String) Ankomststadens flygplatskod.</li><li>`boardingGroup`: (Sträng) Den flygspecifika indikatorn för boardationsorder.</li><li>`checkInMethod`: (String) Den metod som används för incheckning, till exempel räknare, online, kioskdator eller självbetjäning.</li><li>`checkedBags`: (heltal) Antalet påsar som har kontrollerats för flygningen.</li><li>`checkedPassengers`: (heltal) Antalet passagerare som checkas in för flygningen, om det finns flera passagerare för samma reservationsnummer.</li><li>`confirmationNumber`: (Sträng) Reservationsbekräftelsenumret eller identifieraren.</li><li>`departureAirportCode`: (String) Avgångsstadens flygplatskod.</li><li>`flightNumber`: (String) Flightnumret för den flygning som reserveras.</li></ul> |
| `flightStatusSearch` | Objekt | Hämtar de uppgifter som returneras när flygningens status genomsöks. Objektet innehåller följande egenskaper:<ul><li>`arrivalAirportCode`: (String) Ankomststadens flygplatskod.</li><li>`boardingGroup`: (Sträng) Den flygspecifika indikatorn för boardationsorder.</li><li>`departureAirportCode`: (String) Avgångsstadens flygplatskod.</li><li>`departureDate`: (DateTime) Avgångsdatumet för den flygning som reserveras.</li><li>`flightNumber`: (String) Flightnumret för den flygning som reserveras.</li><li>`searchCount`: (heltal) Antalet gånger som statusen för den reserverade flygningen har sökts efter.</li></ul> |
| `agentID` | Sträng | Ombudet eller bokgivaren som är ansvarig för bokningen av reservationen, om tillämpligt. |
| `aircraftID` | Sträng | En identifierare för luftfartyget. |
| `aircraftType` | Sträng | Typ av luftfartyg. |
| `arrivalAirportCode` | Sträng | Ankomststadens flygplatskod. |
| `arrivalDate` | DateTime | Ankomstdatumet för den flygning som reserveras. |
| `cancellation` | Heltal | Det här värdet hämtas när en reservation har annullerats. |
| `confirmationNumber` | Sträng | Reservationsbekräftelsenummer eller identifierare. |
| `created` | Sträng | Det här värdet hämtas när en reservation har skapats. |
| `currencyCode` | Sträng | ISO 4217-valutakoden som användes för att göra köpet. |
| `departureAirportCode` | Sträng | Avgångsstadens flygplatskod. |
| `departureDate` | DateTime | Avgångsdatumet för den flygning som reserveras. |
| `fareClass` | Sträng | Flygningens biljettklass som reserveras. |
| `flightNumber` | Sträng | Flygnumret för den flygning som reserveras. |
| `length` | Heltal | Det totala antalet dagar för reservationen. |
| `loyaltyID` | Sträng | Förmåns- eller belöningsprogram-ID för den passagerare som anges i reservationen. |
| `modification` | Heltal | Det här värdet hämtas när en reservation har ändrats. |
| `modificationDate` | DateTime | Tidpunkten när reservationen senast ändrades. |
| `numberOfAdults` | Heltal | Antalet vuxna som är associerade med reservationen. |
| `numberOfChildren` | Heltal | Antalet underordnade som är associerade med reservationen. |
| `passengerID` | Sträng | Passagerarinformation som är associerad med reservationen. |
| `purpose` | Sträng | Syftet med reservationen, vanligtvis antingen affärsmässig eller personlig. |
| `salesChannel` | Sträng | Försäljningskanalen som reservationen bokförts från. |
| `securityScreening` | Sträng | Den typ av säkerhetskontroll som passageraren omfattas av. |
| `status` | Sträng | Status för flygreservationen. |
| `ticketNumber` | Sträng | Reservationsnummer eller identifierare. |
| `tripType` | Sträng | Anger om reservationen gäller en enkelriktad resa, en rundtur eller en flerstadstrafik. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
