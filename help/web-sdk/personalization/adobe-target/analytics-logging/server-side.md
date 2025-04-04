---
title: Logga A4T-data på serversidan i Experience Platform Web SDK
description: Lär dig hur du aktiverar serverloggning för Adobe Analytics for Target (A4T) med Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;log;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Logga A4T-data på serversidan i Experience Platform Web SDK

Med Adobe Experience Platform Web SDK kan du implementera Adobe Analytics for Target-funktioner (A4T) i Experience Platform Edge Network. När loggning på serversidan är aktiverat utökas alla Analytics-träffar som skickas via Edge Network med Target-information på serversidan, utan att någon process för träffsammanfogning behöver utföras.

Loggning på serversidan för Analytics aktiveras när Analytics är aktiverat i datastream-konfigurationen:

![Dataströmskonfiguration för analys har aktiverats](../assets/enable-analytics-datastream.png)

I följande diagram visas hur data flödar genom systemet när Analytics-loggning på serversidan är aktiverat:

![Loggningsflöde på serversidan](../assets/analytics-server-side-logging.png)

## Nästa steg

Den här guiden täcker serverloggning av A4T-data i Web SDK. Mer information om hur du hanterar A4T-data på klientsidan finns i handboken om [klientloggning](./client-side.md).
