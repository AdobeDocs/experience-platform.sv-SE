---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Arbetskontaktdetaljer, blandning
topic: overview
description: Det här dokumentet innehåller en översikt över mixen Arbetskontaktinformation.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---


# [!UICONTROL Work Contact Details] blanda

>[!NOTE]
>
>Namnen på flera blandningar har ändrats. Mer information finns i dokumentet om uppdatering [av](../name-updates.md) blandade namn.

[!UICONTROL Work Contact Details] är en standardblandning för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Mixin innehåller flera fält som samlar in yrkesinformation om en enskild person, t.ex. arbetsadress, e-post till arbetet, telefonnummer till arbetet och organisationer som personen tillhör.

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