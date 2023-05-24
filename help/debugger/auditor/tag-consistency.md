---
title: Taggkonsekvens - testreferens
description: Lär dig hur granskaren testar taggens enhetlighet i Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 3%

---

# Testreferens för taggens konsekvens

Den här referensen innehåller mer information om hur revisionsfunktionen i Adobe Experience Platform Debugger testar taggens enhetlighet.

>[!NOTE]
>
>Mer information om granskartester i Platform Debugger finns i [översikt över funktioner](./overview.md).

Konsekvenskontroll av taggar söker efter inkonsekvenser på alla skannade sidor. Detta är värden eller konfigurationer som ska vara desamma på alla sidor på webbplatsen för att säkerställa korrekt datainsamling.

| Test | Bredd | Kriterier | Rekommendation |
| --- | --- | --- | --- |
| Adobe Analytics - Enhetlig kodversion | 5 | Mer än en version av Analytics-koden hittades. | Ersätt alla instanser av Analytics med den aktuella versionen.<br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |

{style="table-layout:auto"}
