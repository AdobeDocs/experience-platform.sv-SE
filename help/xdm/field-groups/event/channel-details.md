---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för kanalinformationsschema
description: Läs mer om schemafältgruppen Kanaldetaljer.
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Channel Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Channel Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att beskriva kanalinformation som ID, kanaltyp, medietyp och platstyp.

![](../../images/field-groups/channel-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `channel` | [Upplevelsekanal](../../data-types/experience-channel.md) | Ett objekt som beskriver produktreturer, garantiregistrering och kundvagns-/orderprocesser. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
