---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;reservation;reservation details;
title: Fältgrupp för reservationsdetaljschema
description: Det här dokumentet innehåller en översikt över schemafältgruppen Reservationsdetaljer.
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---


# [!UICONTROL Reservation Details] schemafältgrupp

[!UICONTROL Reservation Details] är en standardgrupp för schemafält för den  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klass som används för att samla in information om en reservation, inklusive längd, ändring, återbetalningsstatus och antal rum.

Fältgruppen innehåller ett enskilt fält av objekttyp, `reservations`. Egenskaperna i det här objektet förklaras nedan.

![Struktur för reservationsinformation](../../images/field-groups/reservation-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `nonRefundableAmount` | [Valuta](../../data-types/currency.md) | Beloppet för reservationspriset som markerats som icke-återbetalningsbart. |
| `transaction` | [Transaktion](../../data-types/transaction.md) | Beskriver valutatransaktionen för reservationen. |
| `id` | Sträng | En unik identifierare för reservationen. |
| `cancellation` | Heltal | Det här värdet hämtas när en reservation har annullerats. |
| `confirmationNumber` | Sträng | Bekräftelsenummer eller identifierare för reservationen. |
| `created` | Heltal | Det här värdet hämtas när reservationen har skapats. |
| `currencyCode` | Sträng | ISO 4217-valutakoden som användes för att göra köpet. |
| `endDate` | DateTime | Avlämnings-, retur- eller utcheckningsdatumet för reservationen. |
| `length` | Heltal | Det totala antalet dagar för reservationen. |
| `modification` | Heltal | Det här värdet hämtas när en reservation har ändrats. |
| `modificationDate` | DateTime | Tidpunkten när reservationen senast ändrades. |
| `numberOfAdults` | Heltal | Antalet vuxna som är associerade med reservationen. |
| `numberOfChildren` | Heltal | Antalet underordnade som är associerade med reservationen. |
| `purpose` | Sträng | Syftet med reservationen, vanligtvis antingen affärsmässig eller personlig. |
| `startDate` | DateTime | Startdatum för hämtning, utgående eller incheckning av reservationen. |
| `triptype` | Sträng | Anger om reservationen gäller en enkelriktad resa, en rundtur eller en flerstadstrafik. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Branschspecifika bokningsfältgrupper

Det finns flera andra standardfältgrupper som utökar [!UICONTROL Reservation Details]-schemat för branschspecifika användningsfall. Mer information finns i följande dokumentation:

* [[!UICONTROL Dining Reservation]](./dining-reservation.md)
* [[!UICONTROL Flight Reservation]](./flight-reservation.md)
* [[!UICONTROL Lodging Reservation]](./lodging-reservation.md)