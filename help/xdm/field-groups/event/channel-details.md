---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för kanalinformationsschema
topic-legacy: overview
description: This document provides an overview of the Channel Details schema field group.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# [!UICONTROL Channel Details] schemafältgrupp

>[!NOTE]
>
>The names of several schema field groups have changed. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Channel Details] is a standard schema field group for the [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), used to describe channel information such as ID, channel type, media type, and location type.

![](../../images/field-groups/channel-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `channel` | [Experience channel](../../data-types/experience-channel.md) | An object that describes product returns, warranty registration, and shopping cart/order processes. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
