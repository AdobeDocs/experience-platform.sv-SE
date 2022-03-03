---
title: Card Actions Schema Field Group
description: This document provides an overview of the Card Actions schema field group.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 2%

---

# [!UICONTROL Card Actions]

[!UICONTROL Card Actions][[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) `personalFinances.cardActions`

![](../../images/field-groups/card-actions.png)

| Property | Data type | Beskrivning |
| --- | --- | --- |
| `cardActivated` | Integer | Tracks when the card has been successfully activated. |
| `cardActivationStart` | Integer | Tracks when the card activation process has been started. |
| `cardCancelled` | Integer | Tracks when a card has been cancelled. |
| `cardControlsLocked` | Integer | Tracks when a card&#39;s controls have been locked. |
| `cardControlsUnlocked` | Integer | Tracks when a card&#39;s controls have been unlocked. |
| `cardID` | Sträng | The identifier for the card being activated. This value might be different from the card number. |
| `cardLocked` | Integer | Tracks when a card has been locked. |
| `cardOrderNew` | Integer | Tracks when a card has been requested. |
| `cardOrderType` | Sträng | The type of card order associated with a card order event. |
| `cardType` | Sträng | The type of card. |
| `cardUnlocked` | Integer | Tracks when a card has been unlocked. |

{style=&quot;table-layout:auto&quot;}

[](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json)
