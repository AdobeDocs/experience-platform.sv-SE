---
keywords: Experience Platform;hem;populära ämnen;api;API;sandlåda;sandlåda;sandlådor;sandlådor;sandlådor
solution: Experience Platform
title: Tillägg till API-handbok för sandlådor
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med sandbox-API:t.
topic-legacy: developer guide
source-git-commit: e4067f79e9da106fe2d2a86fa0024c2e5fe5d0ba
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Sandbox API guide appendix

Det här dokumentet innehåller ytterligare information om hur du arbetar med API:t [!DNL Sandbox].

## Använda frågeparametrar {#query}

[[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) har stöd för användning av frågeparametrar för att sidvisa och filtrera resultat när sandlådor listas.

>[!NOTE]
>
>Frågeparametrarna `limit` och `offset` måste anges tillsammans. Om du bara anger ett fel returneras det. Om du anger ingen är standardgränsen 50 och förskjutningen 0.

| Parameter | Beskrivning |
| --- | --- |
| `limit` | Det maximala antalet poster som ska returneras i svaret. |
| `offset` | Antalet enheter från den första posten att starta (förskjuta) svarslistan från. |
