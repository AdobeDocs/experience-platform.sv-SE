---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Blanda profilarbetsdetaljer
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 2%

---


# [!UICONTROL Profile work details] blanda

[!UICONTROL Profile work details] är en standardblandning för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Mixin innehåller flera fält som samlar in yrkesinformation om en enskild person, t.ex. arbetsadress, e-post till arbetet, telefonnummer till arbetet och organisationer som personen tillhör.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `workAddress` | [Postadress](../../data-types/postal-address.md) | Beskriver personens arbetsadress. |
| `workEmail` | [E-postadress](../../data-types/email-address.md) | Beskriver personens e-postadress till arbetet. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens telefonnummer till arbetet. |
| `organizations` | String (Array) | En array med friformssträngar som representerar de organisationer som personen är medlem i. |

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)