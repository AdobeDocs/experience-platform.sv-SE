---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Komma igång med API:t för observabilitetsinsikter
topic: developer guide
description: Med API:t för observabilitetsinsikter kan du hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till API:t för observationer.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Getting started with the [!DNL Observability Insights] API

Med API:t kan du [!DNL Observability Insights] hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna till innan du försöker anropa [!DNL Observability Insights] API:t.

## Läser exempel-API-anrop

API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. [!DNL Observability Insights] Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet om hur du läser exempel-API-anrop i felsökningsguiden för [Experience Platform](../../landing/troubleshooting.md).

## Obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Nästa steg

Om du vill börja ringa anrop med [!DNL Observability Insights] API:t går du vidare till [metrisk slutpunktshandbok](./metrics.md).