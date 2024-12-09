---
title: Platsklass
description: Läs mer om klassen Location i Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# klassen [!UICONTROL Location]

I Experience Data Model (XDM) hämtar klassen [!UICONTROL Location] platsinformation för live-händelser, till exempel en resehall eller sportarenor.

![Struktur för platsklass](../images/classes/location.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Identifier] | `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet är systemgenererat behöver det inte anges något explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| [!UICONTROL Location Identifier] | `locationID` | [!UICONTROL String] | En unik identifierare för platsen. |
| [!UICONTROL Location Name] | `locationName` | [!UICONTROL String] | Namnet på platsen. |

Klassen kan utökas med fältgruppen [[!UICONTROL Location] ](../field-groups/location/healthcare-location.md) för att beskriva mer information om en plats.
