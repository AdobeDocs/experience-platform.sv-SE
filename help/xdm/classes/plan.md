---
title: Plan, klass
description: Läs mer om klassen Plan i Experience Data Model (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# klassen [!UICONTROL Plan]

I Experience Data Model (XDM) hämtar klassen [!UICONTROL Plan] den minsta uppsättningen egenskaper som definierar en plan, till exempel en hälsoplan eller en försäkringsplan.

![Klassstruktur](../images/classes/plan.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet är systemgenererat anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `planId` | [!UICONTROL String] | En unik identifierare för planen. |
| `planName` | [!UICONTROL String] | Namnet på planen. |

{style="table-layout:auto"}

Klassen kan utökas med fältgruppen [[!UICONTROL Healthcare Plan Details] ](../field-groups/plan/healthcare-plan-details.md) för att beskriva mer information om en sjukförsäkringsplan.
