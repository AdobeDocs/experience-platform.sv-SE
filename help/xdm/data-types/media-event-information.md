---
title: Informationstyp för mediahändelse
description: Läs mer om datatypen XDM (Media Event Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 1%

---

# [!UICONTROL Media event information] datatyp

[!UICONTROL Media Event Information] är en XDM-datatyp (Standard Experience Data Model) som beskriver medieinformationsinformation som rör upplevelsehändelsen.

![Ett diagram över datatypen Media Event Information.](../images/data-types/media-event-information.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | Medieinformation som rör upplevelsehändelsen. |
| `mediaEventTimestamp` | [!UICONTROL String] | Den tid då en mediahändelse inträffade. |
| `mediaEventType` | [!UICONTROL String] | Mediehändelsetypen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
