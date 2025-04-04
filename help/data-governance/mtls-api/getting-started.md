---
title: Komma igång med MTLS Service API
description: Det här dokumentet innehåller ytterligare information som du behöver känna till för att kunna arbeta med MTLS API.
role: Developer
exl-id: db5978cf-fe47-4b76-86ba-c8ea1ee6b12f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Komma igång med MTLS Service API {#getting-started}

Med API:t för MTLS-tjänsten kan du på ett säkert sätt hämta och verifiera de offentliga certifikat som utfärdas av Adobe.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna arbeta med MTLS-tjänstens API.

## Läser exempel-API-anrop

API-dokumentationen för MTLS-tjänsten innehåller ett exempel-API-anrop som visar hur du formaterar dina begäranden. Detta inkluderar sökväg, nödvändiga huvuden och korrekt formaterad nyttolast för begäran. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa Experience Platform-slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i Experience Platform API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

## Nästa steg

Om du vill ringa anrop med MTLS-tjänstens API väljer du slutpunktsguiderna antingen med vänster navigering eller i översikten för [utvecklarhandboken](./overview.md)
