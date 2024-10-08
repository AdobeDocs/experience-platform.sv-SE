---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;telecom;prenumeration;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Datatypen Telecom Subscription
description: Läs mer om datatypen XDM (Telecom Subscription Experience Data Model).
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Datatypen [!UICONTROL Telecom Subscription]

[!UICONTROL Telecom Subscription] är en XDM-datatyp (Standard Experience Data Model) som beskriver information för specifika prenumerationstyper för telekommunikation, till exempel Internet, mobil, media eller landlinje.

>[!NOTE]
>
>Det här dokumentet beskriver datatypen. För fältgruppen med samma namn, se [[!UICONTROL Telecom Subscription]-referenshandboken för fältgruppen ](../field-groups/profile/telecom-subscription.md).
>
>Om du beskriver en prenumerationstyp som inte har med telekommunikationsbranschen att göra, ska du använda den generiska datatypen [[!UICONTROL Subscription] ](./subscription.md) i stället.

![Telecom Subscription structure](../images/data-types/telecom-subscription/structure.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `devices` | Array med objekt | Beskriver en lista över enheter och/eller tillbehör som är kopplade till planen. I avsnittet [nedan](#devices) finns mer information om den förväntade strukturen för varje arrayobjekt. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beskriver prenumerationens ägare. |
| `ID` | Sträng | En unik identifierare för prenumerationsinstansen. |
| `billingPeriod` | Sträng | Varaktigheten mellan faktureringar. |
| `billingStartDate` | Datum | Datumet då faktureringsperioden börjar. Datumformatet (utan tid) ska följa standarden [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `chargeMethod` | Sträng | Hur faktureringen är konfigurerad för att debitera kunden. |
| `contractID` | Sträng | Unikt ID för det kontrakt som styr den här prenumerationen. |
| `country` | Sträng | Landet som prenumerationsvillkoren och avtalsvillkoren är rotade i. |
| `endDate` | Datum | Det datum som den aktuella prenumerationsperioden upphör. Datumformatet (utan tid) ska följa standarden [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentDueDate` | Datum | Datumet då prenumerationsbetalningen förfaller. Datumformatet (utan tid) ska följa standarden [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Sträng | Betalningsmetoden för återkommande betalningar. |
| `paymentStatus` | Sträng | Kontots betalningsstatus. |
| `planName` | Sträng | Prenumerationens läsbara namn. |
| `reason` | Sträng | Medlemmens allmänna avsikt är att använda prenumerationen. |
| `renew` | Sträng | Det överenskomna sättet att fortsätta prenumerationen efter slutdatumet. |
| `startDate` | Datum | Det datum då prenumerationen börjar. Datumformatet (utan tid) ska följa standarden [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Sträng | Prenumerationens aktuella status. |
| `subscriptionCategory` | Sträng | Huvudkategorisering på högsta nivå av den här typen av prenumeration. |
| `subscriptionSKU` | Sträng | Lagerhållningsenheten (SKU) för prenumerationen. |
| `subscriptionSubCategory` | Sträng | Den specifika underkategoriseringen av prenumerationen. |
| `term` | Heltal | Det numeriska värdet för prenumerationsperioden. |
| `termUnitOfTime` | Sträng | Tidsenhet för löptiden. |
| `topUp` | Sträng | Beskriver de överenskomna villkoren för hur konsumerbara delar av en prenumeration återköps under en faktureringsperiod. |
| `type` | Sträng | Rättighetens omfattning i förhållande till hur många personer som omfattas av prenumerationen. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` är en array med objekt, där varje objekt beskriver en enhet eller tillbehör som är associerad med prenumerationen.

![Struktur för enhetsmatris](../images/data-types/telecom-subscription/devices.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `deviceFees` | Objekt | Ett objekt som fångar eventuella enhetsavgifter för objekt som routrar, modem och mottagare. Följande egenskaper förväntas:<ul><li>`amount`: Det monetära beloppet som representeras av `currencyCode`.</li><li>`conversionDate`: Det datum då valutakonverteringen gjordes.</li><li>`currencyCode`: Valutakoden [ ISO 4217 ](https://www.iso.org/iso-4217-currency-codes.html) för `amount`.</li></ul> |
| `ID` | Sträng | Ett unikt ID för enheten. |
| `OS` | Sträng | Enhetens operativsystem. |
| `deviceInsurance` | Sträng | Anger om en kund har anmält sig till försäkringen för den här enheten. |
| `manufacturer` | Sträng | Enhetstillverkaren. |
| `name` | Sträng | Ett namn för enheten. |
| `paymentOptions` | Sträng | Anger om enheten ska betalas i avbetalningar eller i detaljhandelspris. |
| `serialNumber` | Sträng | Enhetens serienummer. |
| `status` | Sträng | Enhetsstatus. |
| `storageCapacity` | Sträng | Enhetens lagringskapacitet. |
| `type` | Sträng | Enhetstypen. |

{style="table-layout:auto"}
