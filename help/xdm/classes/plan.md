---
title: Plan, klass
description: Det här dokumentet innehåller en översikt över klassen Plan i Experience Data Model (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '141'
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

{style="table-layout:auto"}

Klassen kan utökas med [[!UICONTROL Healthcare Plan Details] fältgrupp](../field-groups/plan/healthcare-plan-details.md) Beskriv närmare uppgifter om en sjukförsäkringsplan.
