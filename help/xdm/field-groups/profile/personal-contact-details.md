---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;Individuell profil;fält;scheman;scheman;personuppgifter;Schema design;fältgrupp;Fältgrupp;
solution: Experience Platform
title: Personal Contact Details Schema Field Group
topic-legacy: overview
description: This document provides an overview of the Personal Contact Details schema field group.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 1%

---


# [!UICONTROL Personal Contact Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Personal Contact Details] är en standardgrupp för schemafält för  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klassen som beskriver kontaktinformationen för en enskild person.

![](../../images/field-groups/personal-contact-details.png)

| Egenskap | Data type | Beskrivning |
| --- | --- | --- |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Describes the person&#39;s fax number. |
| `homeAddress` | [Postadress](../../data-types/postal-address.md) | Beskriver personens bostadsadress. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens telefonnummer hemma. |
| `mobilePhone` | [Phone number](../../data-types/phone-number.md) | Describes the person&#39;s mobile phone number. |
| `personalEmail` | [E-postadress](../../data-types/email-address.md) | Beskriver personens e-postadress. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
