---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för kampanjmarknadsföringsinformation
description: Det här dokumentet innehåller en översikt över schemafältgruppen Campaign Marketing Details.
exl-id: be08b38b-68a0-4a74-9b8f-0344a0637395
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# [!UICONTROL Campaign Marketing Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL Campaign Marketing Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), som används för att beskriva marknadsföringskampanjinformation som kampanjgrupp, namn och spårningskod.

![](../../images/field-groups/campaign-marketing-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `marketing` | [Marknadsföring](../../data-types/marketing.md) | Ett objekt som beskriver information om marknadsföringskampanjer, till exempel kampanjgrupp, namn och spårningskod. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
