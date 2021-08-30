---
keywords: Experience Platform;hem;populära ämnen;api;API;sandlåda;sandlåda;sandlådor;sandlådor;sandlådor
solution: Experience Platform
title: Tillägg till API-handbok för sandlådor
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med sandbox-API:t.
topic-legacy: developer guide
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Sandbox API guide appendix

Det här dokumentet innehåller ytterligare information om hur du arbetar med API:t [!DNL Sandbox].

## Använda frågeparametrar {#query}

[[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) har stöd för användning av frågeparametrar för att sidvisa och filtrera resultat när sandlådor listas.

>[!NOTE]
>
>Frågeparametrarna `limit` och `offset` måste anges tillsammans. Om du bara anger ett fel returneras det. Om du anger ingen är standardgränsen 50 och förskjutningen 0.

| Parameter | Beskrivning |
| --- | --- |
| `limit` | Det maximala antalet poster som ska returneras i svaret. |
| `offset` | Antalet enheter från den första posten att starta (förskjuta) svarslistan från. |
