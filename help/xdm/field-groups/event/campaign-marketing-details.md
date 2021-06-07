---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för kampanjmarknadsföringsinformation
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen Campaign Marketing Details.
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# [!UICONTROL Campaign Marketing Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Campaign Marketing Details] är en standardgrupp för schemafält för  [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md), som används för att beskriva marknadsföringskampanjinformation som kampanjgrupp, namn och spårningskod.

![](../../images/field-groups/campaign-marketing-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `marketing` | [Marknadsföring](../../data-types/marketing.md) | Ett objekt som beskriver information om marknadsföringskampanjer, till exempel kampanjgrupp, namn och spårningskod. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.schema.json)
