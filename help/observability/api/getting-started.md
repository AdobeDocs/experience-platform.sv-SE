---
keywords: Experience Platform;hem;populära ämnen;datumintervall
solution: Experience Platform
title: Getting Started with the Observability Insights API
description: Med API:t för observabilitetsinsikter kan du hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till API:t för observationer.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Komma igång med [!DNL Observability Insights] API

The [!DNL Observability Insights] Med API kan du hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till [!DNL Observability Insights] API.

## Läser exempel-API-anrop

The [!DNL Observability Insights] API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet om hur du läser exempel-API-anrop i [Felsökningsguide för Experience Platform](../../landing/troubleshooting.md).

## Obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver ett huvud som anger namnet på den sandlåda som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Nästa steg

Börja ringa samtal med [!DNL Observability Insights] API, gå vidare till [metrisk slutpunktsguide](./metrics.md).
