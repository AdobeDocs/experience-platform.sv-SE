---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;environment;environment details;
solution: Experience Platform
title: Fältgrupp för miljöinformationsschema
description: Läs mer om schemafältgruppen ExperienceEvent Environment Details.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Schemafältgruppen [!UICONTROL Environment Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Environment Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att samla in information om miljödetaljer som rör en upplevelsehändelse, till exempel enhetsinformation, webbläsarinformation, lokal tid och annan geografisk information.

![](../../images/field-groups/environment-details.png){width=500}

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `device` | [Enhet](../../data-types/device.md) | Beskriver en identifierad enhets-, program- eller enhetsläsarinstans som kan spåras mellan sessioner, vanligtvis via cookies. |
| `environment` | [Miljö](../../data-types/environment.md) | Beskriver information om situationsförhållanden för händelseobservationen, särskilt med detaljerad information om övergångar, t.ex. nätverks- eller programversioner. |
| `placeContext` | [Montera kontext](../../data-types/place-context.md) | Beskriver de övergående omständigheter som rör händelseobservationen. Exemplen omfattar språkområdesspecifik information som väder, lokal tid, trafik, veckodag, arbetsdag kontra semester och arbetstimmar. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
