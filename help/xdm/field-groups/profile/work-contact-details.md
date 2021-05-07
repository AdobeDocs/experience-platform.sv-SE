---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individual profile;fields;schemas;schema design;mixin;mixin;work details;profile work;
solution: Experience Platform
title: Fältgrupp för arbetskontaktinformation
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen Arbetskontaktinformation.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# [!UICONTROL Work Contact Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Work Contact Details] är en standardgrupp för schemafält för  [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Fältgruppen innehåller flera fält som samlar in yrkesinformation om en enskild person, t.ex. arbetsadress, e-post till arbetet, telefonnummer till arbetet och organisationer som personen tillhör.

![](../../images/field-groups/work-contact-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `workAddress` | [Postadress](../../data-types/postal-address.md) | Beskriver personens arbetsadress. |
| `workEmail` | [E-postadress](../../data-types/email-address.md) | Beskriver personens e-postadress till arbetet. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens telefonnummer till arbetet. |
| `organizations` | String (Array) | En array med friformssträngar som representerar de organisationer som personen är medlem i. |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
