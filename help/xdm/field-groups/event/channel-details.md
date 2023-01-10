---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för kanalinformationsschema
description: Det här dokumentet innehåller en översikt över schemafältgruppen Kanalinformation.
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# [!UICONTROL Channel Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL Channel Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), används för att beskriva kanalinformation som ID, kanaltyp, medietyp och platstyp.

![](../../images/field-groups/channel-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `channel` | [Experience channel](../../data-types/experience-channel.md) | Ett objekt som beskriver produktreturer, garantiregistrering och kundvagns-/orderprocesser. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
