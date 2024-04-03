---
title: Lista över lägen, startsamlingens datatyp
description: Läs mer om datatypen List of states Start Data Type Experience Data Model (XDM).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# [!UICONTROL List of States Start] datatyp

The [!UICONTROL List of States Start] datatypen är en XDM-datatyp (Experience Data Model) som utformats för att representera information som relaterar till startläget för olika spelarattribut. Den innehåller [!UICONTROL Player State Name] egenskaper som anger det specifika attributtillståndet (till exempel &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Den här datatypen används för att hämta och beskriva de ursprungliga villkoren för olika spelarlägen.

![Ett diagram över [!UICONTROL List of States Start] datatyp.](../images/data-types/list-of-states-start-collection.png)

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Nej | Namnet på spelarläget. Uppräknade: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; med respektive innebörd. |

{style="table-layout:auto"}
