---
title: Datatyp för personnamn
description: Läs mer om datatypen XDM (Human Name Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Datatypen [!UICONTROL Human Name]

[!UICONTROL Human Name] är en XDM-datatyp (Standard Experience Data Model) som ger information om namnet på en mänsklig eller annan levande enhet. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypstruktur för personnamn](../../images/data-types/healthcare/human-name.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../healthcare/period.md) | Den tidsperiod då namnet används eller används. |
| [!UICONTROL Family] | `family` | Sträng | Familjen eller efternamnet. |
| [!UICONTROL Given] | `given` | Array med strängar | Det angivna namnet, inklusive eventuella mellannamn. |
| [!UICONTROL Prefix] | `prefix` | Array med strängar | Alla delar av namnet före det angivna namnet eller förnamnet. |
| [!UICONTROL Suffix] | `suffix` | Array med strängar | Alla delar av namnet efter familjen eller efternamnet. |
| [!UICONTROL Text] | `text` | Sträng | Den rena textrepresentationen av det fullständiga namnet. |
| [!UICONTROL Use] | `use` | Sträng | Användning av namnet. Värdena för den här egenskapen måste vara lika med ett eller flera av följande kända enum-värden. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
