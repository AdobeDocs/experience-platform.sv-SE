---
title: Fältgrupp för kortåtgärdsschema
description: Läs mer om schemafältgruppen för kortåtgärder.
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# [!UICONTROL Card Actions] schemafältgrupp

[!UICONTROL Card Actions] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller en `personalFinances.cardActions` till ett schema, som innehåller information om en kortåtgärd som korttyp, aktiveringsstatus och låsstatus.

![](../../images/field-groups/card-actions.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `cardActivated` | Heltal | Spårar när kortet har aktiverats. |
| `cardActivationStart` | Heltal | Spårar när kortaktiveringen har startats. |
| `cardCancelled` | Heltal | Spårar när ett kort har annullerats. |
| `cardControlsLocked` | Heltal | Spårar när ett korts kontroller har låsts. |
| `cardControlsUnlocked` | Heltal | Spårar när ett kort har låsts upp. |
| `cardID` | Sträng | Identifieraren för kortet som aktiveras. Detta värde kan skilja sig från kortnumret. |
| `cardLocked` | Heltal | Spårar när ett kort har låsts. |
| `cardOrderNew` | Heltal | Spårar när ett kort har begärts. |
| `cardOrderType` | Sträng | Den typ av kortorder som är associerad med en kortorderhändelse. |
| `cardType` | Sträng | Typ av kort. |
| `cardUnlocked` | Heltal | Spårar när ett kort har låsts upp. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
