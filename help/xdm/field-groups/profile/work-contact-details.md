---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individual profile;fields;schemas;schema design;mixin;mixin;work details;profile work;
solution: Experience Platform
title: Fältgrupp för arbetskontaktinformation
topic-legacy: overview
description: This document provides an overview of the Work Contact Details schema field group.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---


# [!UICONTROL Work Contact Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Work Contact Details] är en standardgrupp för schemafält för  [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Fältgruppen innehåller flera fält som samlar in yrkesinformation om en enskild person, t.ex. arbetsadress, e-post till arbetet, telefonnummer till arbetet och organisationer som personen tillhör.

![](../../images/field-groups/work-contact-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `workAddress` | [Postadress](../../data-types/postal-address.md) | Beskriver personens arbetsadress. |
| `workEmail` | [E-postadress](../../data-types/email-address.md) | Describes the person&#39;s work email address. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beskriver personens telefonnummer till arbetet. |
| `organizations` | String (Array) | En array med friformssträngar som representerar de organisationer som personen är medlem i. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
