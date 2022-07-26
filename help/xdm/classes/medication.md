---
title: Medicinaklass
description: Det här dokumentet innehåller en översikt över klassen Medication i Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# [!UICONTROL Medication] class

I Experience Data Model (XDM) är [!UICONTROL Medication] Klassen innehåller den minsta uppsättning egenskaper som definierar ett ämne som används för medicinsk behandling, särskilt ett läkemedel eller läkemedel.

![Klassstruktur](../images/classes/medication.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `medicationId` | [!UICONTROL String] | En unik identifierare för medicineringen. |
| `medicationName` | [!UICONTROL String] | Läkemedlets namn. |

{style=&quot;table-layout:auto&quot;}

Klassen kan utökas med [[!UICONTROL Healthcare medication] fältgrupp](../field-groups/medication/healthcare-medication.md) för att beskriva mer ingående detaljer om läkemedlet eller läkemedlet.
