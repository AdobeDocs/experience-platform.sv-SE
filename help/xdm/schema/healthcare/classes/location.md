---
title: Platsklass
description: Läs mer om klassen Location i Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1d100981-49fb-4f02-b2c6-324f9c541f76
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# klassen [!UICONTROL Location]

I Experience Data Model (XDM) hämtar klassen [!UICONTROL Location] platsinformation för live-händelser, till exempel en resehall eller sportarenor.

![Struktur för platsklass](../../../images/healthcare/classes/location.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Identifier] | `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet är systemgenererat behöver det inte anges något explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| [!UICONTROL Location Identifier] | `locationID` | [!UICONTROL String] | En unik identifierare för platsen. |
| [!UICONTROL Location Name] | `locationName` | [!UICONTROL String] | Namnet på platsen. |

Klassen kan utökas med fältgruppen [[!UICONTROL Location] ](../field-groups/location.md) för att beskriva mer information om en plats.
