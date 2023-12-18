---
title: Fältgrupp för punktidentifiering
description: Läs mer om schemafältgruppen Punktidentifiering (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# [!UICONTROL Bot Detection] fältgrupp

[!UICONTROL Bot Detection] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller information om robotgenererad trafik.

![Ett diagram över [!UICONTROL Bot Detection] fältgrupp.](../../images/field-groups/bot-detection-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Bot Detection] | `botDetection` | object | Innehåller information om robotgenererad trafik. |
| [!UICONTROL Score] | `score` | tal | Objektens sannolikhetspoäng från noll till ett. En nollpoäng innebär att trafiken inte är en robot. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)

