---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;environment;environment details;
solution: Experience Platform
title: Fältgrupp för miljöinformationsschema
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen ExperienceEvent Environment Details.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# [!UICONTROL Environment Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Environment Details] är en standardgrupp för schemafält för den  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klass som används för att samla in information om miljödetaljer som rör en upplevelsehändelse, t.ex. enhetsinformation, webbläsarinformation, lokal tid och annan geografisk information.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Property | Datatyp | Beskrivning |
| --- | --- | --- |
| `device` | [Enhet](../../data-types/device.md) | Beskriver en identifierad enhets-, program- eller enhetsläsarinstans som kan spåras mellan sessioner, vanligtvis via cookies. |
| `environment` | [Miljö](../../data-types/environment.md) | Beskriver information om situationsförhållanden för händelseobservationen, särskilt med detaljerad information om övergångar, t.ex. nätverks- eller programversioner. |
| `placeContext` | [Place context](../../data-types/place-context.md) | Beskriver de övergående omständigheter som rör händelseobservationen. Examples include locale-specific information such as weather, local time, traffic, day of the week, workday vs. holiday, and working hours. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
