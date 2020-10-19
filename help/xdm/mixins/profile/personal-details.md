---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: Blanda personliga profiluppgifter
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 2%

---


# [!UICONTROL Profile personal details] blanda

[!UICONTROL Profile personal details] är en standardblandning för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Mixin tillhandahåller ett `person` objekt på rotnivå, vars underfält beskriver kontaktinformation om en enskild person.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens faxnummer. |
| `homeAddress` | [Postadress](../../data-types/postal-address.md) | Beskriver personens bostadsadress. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens telefonnummer hemma. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens mobiltelefonnummer. |
| `personalEmail` | [E-postadress](../../data-types/email-address.md) | Beskriver personens e-postadress. |

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
