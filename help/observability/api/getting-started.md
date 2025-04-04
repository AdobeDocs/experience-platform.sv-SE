---
keywords: Experience Platform;hem;populära ämnen;datumintervall
solution: Experience Platform
title: Getting Started with the Observability Insights API
description: Med API:t för observabilitetsinsikter kan du hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till API:t för observationer.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Komma igång med [!DNL Observability Insights]-API:t

Med API:t [!DNL Observability Insights] kan du hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t [!DNL Observability Insights].

## Läser exempel-API-anrop

API-dokumentationen för [!DNL Observability Insights] innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet om hur du läser exempel-API-anrop i [Experience Platform felsökningsguide](../../landing/troubleshooting.md).

## Obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Observability Insights] går du till [metrisk slutpunktshandbok](./metrics.md).
