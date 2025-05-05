---
title: Taggkonsekvens - testreferens
description: Lär dig hur granskaren testar taggens enhetlighet i Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 1%

---

# Testreferens för taggens konsekvens

Den här referensen innehåller mer information om hur revisionsfunktionen i Adobe Experience Platform Debugger testar taggens enhetlighet.

>[!NOTE]
>
>Mer information om granskartester i Experience Platform Debugger finns i [funktionsöversikten för granskare](./overview.md).

Konsekvenskontroll av taggar söker efter inkonsekvenser på alla skannade sidor. Detta är värden eller konfigurationer som ska vara desamma på alla sidor på webbplatsen för att säkerställa korrekt datainsamling.

| Test | Bredd | Kriterier | Rekommendation |
| --- | --- | --- | --- |
| Adobe Analytics - Konsekvent kodversion | 5 | Mer än en version av Analytics-koden hittades. | Ersätt alla instanser av Analytics med den aktuella versionen.<br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=sv-SE) |

{style="table-layout:auto"}
