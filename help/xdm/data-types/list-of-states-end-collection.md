---
title: List of states End Collection datatyp
description: Läs mer om datatypen List of states End Collection Data Type Experience Data Model (XDM).
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Datatypen [!UICONTROL List of States End]

Datatypen List of states End Collection är en XDM-datatyp (Experience Data Model) som utformats för att representera information som relaterar till slutläget för olika spelarattribut. Den innehåller egenskaperna [!UICONTROL Player State Name] som anger det specifika attributtillståndet (till exempel &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Den här datatypen används för att hämta och beskriva de ursprungliga villkoren för olika spelarlägen.

![Ett diagram över datatypen List of States End Collection.](../images/data-types/list-of-states-end-collection.png)

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Nej | Namnet på spelarläget. Uppräknade: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; med respektive innebörd. |

{style="table-layout:auto"}
