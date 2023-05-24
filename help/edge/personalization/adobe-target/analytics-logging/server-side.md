---
title: Loggning på serversidan för A4T-data i Platform Web SDK
description: Lär dig hur du aktiverar loggning på serversidan för Adobe Analytics for Target (A4T) med Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;log;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: 38d54b2c793c9dcb1a45ec4acbb9016d1e927d23
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Loggning på serversidan för A4T-data i Platform Web SDK

Med Adobe Experience Platform Web SDK kan du implementera Adobe Analytics for Target-funktioner (A4T) på Platform Edge Network. När loggning på serversidan är aktiverat utökas alla Analytics-träffar som skickas via Edge Network med Target-information på serversidan, utan att någon träffsammanfogningsprocess behöver utföras.

Loggning på serversidan för Analytics aktiveras när Analytics är aktiverat i datastream-konfigurationen:

![Analysdataströmskonfiguration har aktiverats](../assets/enable-analytics-datastream.png)

I följande diagram visas hur data flödar genom systemet när Analytics-loggning på serversidan är aktiverat:

![Loggningsflöde på serversidan](../assets/analytics-server-side-logging.png)

## Nästa steg

Den här guiden täcker serverloggning av A4T-data i Web SDK. Se guiden [loggning på klientsidan](./client-side.md) om du vill ha mer information om hur du hanterar A4T-data på klientsidan.
