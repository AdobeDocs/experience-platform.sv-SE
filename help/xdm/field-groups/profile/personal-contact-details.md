---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;Individuell profil;fält;scheman;scheman;personuppgifter;Schema design;fältgrupp;Fältgrupp;
solution: Experience Platform
title: Schemafältgrupp för personlig kontaktinformation
description: Läs mer om schemafältgruppen Personlig kontaktinformation.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# [!UICONTROL Personal Contact Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL Personal Contact Details] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) som beskriver kontaktinformationen för en enskild person.

![](../../images/field-groups/personal-contact-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens faxnummer. |
| `homeAddress` | [Postadress](../../data-types/postal-address.md) | Beskriver personens bostadsadress. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens telefonnummer hemma. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens mobiltelefonnummer. |
| `personalEmail` | [E-postadress](../../data-types/email-address.md) | Beskriver personens e-postadress. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
