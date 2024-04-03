---
title: Informationstyp för mediahändelse
description: Läs mer om datatypen XDM (Media Event Information Experience Data Model).
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 1%

---

# [!UICONTROL Media Event Information] datatyp

[!UICONTROL Media Event Information] är en XDM-datatyp (Standard Experience Data Model) som beskriver medieinformationsinformation som rör upplevelsehändelsen.

![Ett diagram över datatypen Media Event Information.](../images/data-types/media-event-information.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Medieinformation som rör upplevelsehändelsen. Den här datatypen används för båda [mediedatainsamling](./media-collection-details.md) och [medierapporter](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL String] | Den tid då en mediahändelse inträffade. |
| `mediaEventType` | [!UICONTROL String] | Mediehändelsetypen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
