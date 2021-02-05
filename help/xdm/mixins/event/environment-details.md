---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;mixin;mixin;environment;environment details;
solution: Experience Platform
title: Blanda miljödetaljer
topic: overview
description: Det här dokumentet innehåller en översikt över ExperienceEvent-miljödetaljmixen.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---


# [!UICONTROL Environment Details] blanda

>[!NOTE]
>
>Namnen på flera blandningar har ändrats. Mer information finns i dokumentet om [uppdateringar av blandnamn](../name-updates.md).

[!UICONTROL Environment Details] är en standardblandning för den  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) klass som används för att samla in information om miljödetaljer som rör en upplevelsehändelse, t.ex. enhetsinformation, webbläsarinformation, lokal tid och annan geografisk information.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `device` | [Enhet](../../data-types/device.md) | Beskriver en identifierad enhets-, program- eller enhetsläsarinstans som kan spåras mellan sessioner, vanligtvis via cookies. |
| `environment` | [Miljö](../../data-types/environment.md) | Beskriver information om situationsförhållanden för händelseobservationen, särskilt med detaljerad information om övergångar, t.ex. nätverks- eller programversioner. |
| `placeContext` | [Montera kontext](../../data-types/place-context.md) | Beskriver de övergående omständigheter som rör händelseobservationen. Exemplen omfattar språkområdesspecifik information som väder, lokal tid, trafik, veckodag, arbetsdag kontra semester och arbetstimmar. |

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
