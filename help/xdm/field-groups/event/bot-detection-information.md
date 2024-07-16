---
title: Fältgrupp för punktidentifiering
description: Läs mer om schemafältgruppen Punktidentifiering (XDM).
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# Fältgrupp [!UICONTROL Bot Detection]

[!UICONTROL Bot Detection] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md). Fältgruppen innehåller information om robotgenererad trafik.

![Ett diagram över fältgruppen [!UICONTROL Bot Detection].](../../images/field-groups/bot-detection-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Bot Detection] | `botDetection` | object | Innehåller information om robotgenererad trafik. |
| [!UICONTROL Score] | `score` | tal | Objektens sannolikhetspoäng från noll till ett. En nollpoäng innebär att trafiken inte är en robot. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
