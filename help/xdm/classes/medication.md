---
title: Medicinaklass
description: Läs mer om klassen Medication i Experience Data Model (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# [!UICONTROL Medication] class

I Experience Data Model (XDM) är [!UICONTROL Medication] Klassen innehåller den minsta uppsättning egenskaper som definierar en substans som används för medicinsk behandling, särskilt ett läkemedel eller läkemedel.

![Klassstruktur](../images/classes/medication.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `medicationId` | [!UICONTROL String] | En unik identifierare för medicineringen. |
| `medicationName` | [!UICONTROL String] | Läkemedlets namn. |

{style="table-layout:auto"}

Klassen kan utökas med [[!UICONTROL Healthcare medication] fältgrupp](../field-groups/medication/healthcare-medication.md) för att beskriva mer ingående detaljer om läkemedlet eller läkemedlet.
