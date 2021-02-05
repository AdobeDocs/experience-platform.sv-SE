---
keywords: Experience Platform;hem;populära ämnen;datumintervall
solution: Experience Platform
title: Getting Started with the Observability Insights API
topic: developer guide
description: Med API:t för observabilitetsinsikter kan du hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till API:t för observationer.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Komma igång med API:t [!DNL Observability Insights]

Med API:t [!DNL Observability Insights] kan du hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t [!DNL Observability Insights].

## Läser exempel-API-anrop

API-dokumentationen för [!DNL Observability Insights] innehåller exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet om hur du läser exempel-API-anrop i [felsökningsguiden för Experience Platform](../../landing/troubleshooting.md).

## Obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Observability Insights] går du till [metrics endpoint guide](./metrics.md).