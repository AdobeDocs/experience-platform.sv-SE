---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för kampanjmarknadsföringsinformation
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen Campaign Marketing Details.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# [!UICONTROL Campaign Marketing Details] schemafältgrupp

>[!NOTE]
>
>The names of several schema field groups have changed. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Campaign Marketing Details] is a standard schema field group for the [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), used to describe marketing campaign information such as campaign group, name, and tracking code.

![](../../images/field-groups/campaign-marketing-details.png)

| Property | Datatyp | Beskrivning |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Ett objekt som beskriver information om marknadsföringskampanjer, till exempel kampanjgrupp, namn och spårningskod. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
