---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för kanalinformationsschema
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen Kanalinformation.
source-git-commit: b9168052174c250810e59e403cb77419d510df3b
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# [!UICONTROL Channel Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Channel Details] är en standardgrupp för schemafält för  [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md), som används för att beskriva kanalinformation som ID, kanaltyp, medietyp och platstyp.

![](../../images/field-groups/channel-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `channel` | [Experience channel](../../data-types/experience-channel.md) | Ett objekt som beskriver produktreturer, garantiregistrering och kundvagns-/orderprocesser. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-channel.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-channel.schema.json)
