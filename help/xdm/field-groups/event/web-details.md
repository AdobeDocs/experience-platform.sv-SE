---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för webbinformationsschema
description: Läs mer om schemafältgruppen Webbinformation.
exl-id: eb42606b-ade4-4d72-b601-c560009c98e8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Web Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Web Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att beskriva information om webbinformationshändelser som interaktion, sidinformation och referent.

![](../../images/field-groups/web-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `web` | [Webbinformation](../../data-types/web-information.md) | Beskriver länkklick, webbsidesinformation, referensinformation och webbläsarinformation. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.schema.json)
