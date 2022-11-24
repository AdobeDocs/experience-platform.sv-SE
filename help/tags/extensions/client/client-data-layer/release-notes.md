---
title: Versionsinformation för tillägget Adobe Client Data Layer
description: Den senaste versionsinformationen för taggtillägget Adobe Client Data Layer i Adobe Experience Platform.
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 1%

---

# Versionsinformation om tillägget Adobe Client Data Layer

## Version 2.0.2

* Läsa in ACDL Core-biblioteket (version 2.0.2)
* Version 2.0.0 av ACDL:s huvudbibliotek eliminerade möjligheten att återanvända event.beforeState och event.afterState. Därför har vi ändrat dessa objekt så att de alltid returnerar tomma objekt. Implementeringar som är beroende av den här funktionen måste uppdateras när du går över till den här versionen.

## Version 1.1.3

* Läsa in ACDL Core-biblioteket (version 1.1.3)

## Version 1.1.2

Följande funktionalitet finns i tillägget i den första versionen:

* Läsa in ACDL Core-biblioteket (version 1.1.1)
* Byta namn på datalagret i Adobe
* Händelser:
   * Lyssna på alla händelser
   * Lyssna efter alla data som skickats
   * Lyssna efter en viss händelse som har skickats
   * Alla event kan spelas upp på olika omfång
* Dataelement:
   * Beräknat tillstånd: Globalt eller specifikt läge
   * Datalagerstorlek
* Instruktioner:
   * Återställ datalagrets storlek (med det senaste beräknade läget)
   * Flytta objekt till datalagret
