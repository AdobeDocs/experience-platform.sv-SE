---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: Blanda personliga kontaktuppgifter
topic: overview
description: Det här dokumentet innehåller en översikt över blandningen Personlig kontaktinformation.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 2%

---


# [!UICONTROL Personal Contact Details] blanda

>[!NOTE]
>
>Namnen på flera blandningar har ändrats. Mer information finns i dokumentet om uppdatering [av](../name-updates.md) blandade namn.

[!UICONTROL Personal Contact Details] är en standardblandning för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md) som beskriver kontaktinformationen för en enskild person.

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
