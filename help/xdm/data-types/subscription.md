---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;prenumeration;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Typ av prenumerationsdata
description: Det här dokumentet innehåller en översikt över datatypen XDM (Subscription Experience Data Model).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 8%

---

# [!UICONTROL Subscription] datatyp

[!UICONTROL Subscription] är en XDM-datatyp (Standard Experience Data Model) som beskriver licensierade rättigheter till programvara, tjänster eller varor som används baserat på tid eller användning.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `device` | [[!UICONTROL Device]](./device.md) | Beskriver information om enheten som är länkad till prenumerationen. |
| `environment` | [[!UICONTROL Environment]](./environment.md) | Innehåller information om den omgivande situation som händelseobservationen inträffade, med detaljerad information om övergångar, t.ex. nätverks- eller programversioner. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beskriver en enskild person. Detta kan även representera en person som agerar i olika roller, till exempel en kund, kontakt eller ägare. |
| `SKU` | Sträng | Lagerhållningsenheten (SKU), en unik identifierare för en produkt. |
| `billingPeriod` | Sträng | Varaktigheten mellan faktureringar. |
| `billingStartDate` | Datum | Datumet då den första fakturan förfaller. Datumformatet (utan tid) ska följa [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `category` | Sträng | Huvudkategorisering på högsta nivå av den här typen av prenumeration. |
| `chargeMethod` | Sträng | Hur faktureringen är konfigurerad för att debitera kunden. |
| `contractID` | Sträng | Unikt ID för det kontrakt som styr den här prenumerationen. |
| `country` | Sträng | Landet som prenumerationsvillkoren och avtalsvillkoren är rotade i. |
| `endDate` | Datum | Det datum som den aktuella prenumerationsperioden upphör. Datumformatet (utan tid) ska följa [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `paymentMethod` | Sträng | Betalningsmetoden för återkommande betalningar. |
| `paymentStatus` | Sträng | Kontots betalningsstatus. |
| `planName` | Sträng | Prenumerationens läsbara namn. |
| `reason` | Sträng | Medlemmens allmänna avsikt är att använda prenumerationen. |
| `renew` | Sträng | Det överenskomna sättet att fortsätta prenumerationen efter slutdatumet. |
| `revision` | Sträng | Identifieringen mellan prenumerationer med samma namn och kategorihierarki. |
| `startDate` | Datum | Det datum då prenumerationen börjar. Datumformatet (utan tid) ska följa [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `status` | Sträng | Prenumerationens aktuella status. |
| `subCategory` | Sträng | Den specifika underkategoriseringen av prenumerationen. |
| `term` | Heltal | Det numeriska värdet för prenumerationsperioden. |
| `termUnitOfTime` | Sträng | Tidsenhet för löptiden. |
| `topUp` | Sträng | Beskriver de överenskomna villkoren för hur förbrukningsaspekter av en prenumeration återköps under en faktureringsperiod. |
| `type` | Sträng | Rättighetens omfattning i förhållande till hur många personer som omfattas av prenumerationen. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
