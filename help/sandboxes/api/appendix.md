---
keywords: Experience Platform;hem;populära ämnen;api;API;sandlåda;sandlåda;sandlådor;sandlådor;sandlådor
solution: Experience Platform
title: Tillägg till API-handbok för sandlådor
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med sandbox-API:t.
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Sandbox API guide appendix

Det här dokumentet innehåller ytterligare information om hur du arbetar med [!DNL Sandbox] API.

## Använda frågeparametrar {#query}

The [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) har stöd för användning av frågeparametrar för att sidan och filtrera resultat när sandlådor listas.

>[!NOTE]
>
>The `limit` och `offset` frågeparametrar måste anges tillsammans. Om du bara anger ett fel returneras det. Om du anger ingen är standardgränsen 50 och förskjutningen 0.

| Parameter | Beskrivning |
| --- | --- |
| `limit` | Det maximala antalet poster som ska returneras i svaret. |
| `offset` | Antalet enheter från den första posten att starta (förskjuta) svarslistan från. |
