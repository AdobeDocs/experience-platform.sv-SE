---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;Individuell profil;fält;scheman;scheman;personuppgifter;Schema design;fältgrupp;Fältgrupp;
solution: Experience Platform
title: Schemafältgrupp för personlig kontaktinformation
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen Personlig kontaktinformation.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 1%

---


# [!UICONTROL Personal Contact Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Personal Contact Details] är en standardgrupp för schemafält för  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klassen som beskriver kontaktinformationen för en enskild person.

![](../../images/field-groups/personal-contact-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens faxnummer. |
| `homeAddress` | [Postadress](../../data-types/postal-address.md) | Beskriver personens bostadsadress. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens telefonnummer hemma. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens mobiltelefonnummer. |
| `personalEmail` | [E-postadress](../../data-types/email-address.md) | Beskriver personens e-postadress. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
