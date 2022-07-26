---
title: Plan, klass
description: Det här dokumentet innehåller en översikt över klassen Plan i Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# [!UICONTROL Plan] class

I Experience Data Model (XDM) är [!UICONTROL Plan] klassen innehåller den minsta uppsättning egenskaper som definierar en plan, till exempel en hälsoplan eller en försäkringsplan.

![Klassstruktur](../images/classes/plan.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `planId` | [!UICONTROL String] | En unik identifierare för planen. |
| `planName` | [!UICONTROL String] | Namnet på planen. |

{style=&quot;table-layout:auto&quot;}

Klassen kan utökas med [[!UICONTROL Healthcare Plan Details] fältgrupp](../field-groups/plan/healthcare-plan-details.md) Beskriv närmare uppgifter om en sjukförsäkringsplan.
