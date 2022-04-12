---
title: Loggning på serversidan för A4T-data i Platform Web SDK
description: Lär dig hur du aktiverar loggning på serversidan för Adobe Analytics for Target (A4T) med Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;log;
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
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
