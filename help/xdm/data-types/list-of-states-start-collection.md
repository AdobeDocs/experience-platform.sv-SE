---
title: Lista över lägen, startsamlingens datatyp
description: Läs mer om datatypen List of states Start Data Type Experience Data Model (XDM).
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Datatypen [!UICONTROL List of States Start]

Datatypen [!UICONTROL List of States Start] är en XDM-datatyp (Experience Data Model) som utformats för att representera information som relaterar till startläget för olika spelarattribut. Den innehåller egenskaperna [!UICONTROL Player State Name] som anger det specifika attributtillståndet (till exempel &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Den här datatypen används för att hämta och beskriva de ursprungliga villkoren för olika spelarlägen.

![Ett diagram med datatypen [!UICONTROL List of States Start].](../images/data-types/list-of-states-start-collection.png)

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Nej | Namnet på spelarläget. Uppräknade: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; med respektive innebörd. |

{style="table-layout:auto"}
