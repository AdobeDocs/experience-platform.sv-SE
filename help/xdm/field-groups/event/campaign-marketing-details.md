---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för kampanjmarknadsföringsinformation
description: Läs mer om schemafältgruppen för kampanjmarknadsföringsinformation.
exl-id: be08b38b-68a0-4a74-9b8f-0344a0637395
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Campaign Marketing Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Campaign Marketing Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att beskriva marknadsföringskampanjinformation, till exempel kampanjgrupp, namn och spårningskod.

![](../../images/field-groups/campaign-marketing-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `marketing` | [Marknadsföring](../../data-types/marketing.md) | Ett objekt som beskriver information om marknadsföringskampanjer, till exempel kampanjgrupp, namn och spårningskod. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
