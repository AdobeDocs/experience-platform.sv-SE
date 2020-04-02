---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Uppskattningar
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# Uppskattningar

intro

- Hämta resultaten från ett specifikt uppskattningsjobb

## Komma igång

API-slutpunkterna som används i den här guiden ingår i segmenterings-API:t. Läs utvecklarhandboken för [segmentering innan du fortsätter](./getting-started.md).

Avsnittet [](./getting-started.md#getting-started) Komma igång i utvecklarhandboken för segmentering innehåller länkar till relaterade ämnen, en guide till hur du läser exempelanropen för API i dokumentet och viktig information om vilka huvuden som krävs för att anropa något Experience Platform-API.

## Hämta resultaten från ett specifikt uppskattningsjobb

Du kan hämta information om ett specifikt uppskattningsjobb genom att göra en GET-begäran till `/estimate` slutpunkten och ange uppskattningsjobbets `id` värde i begärandesökvägen.

**API-format**

```http
GET /estimate/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: Värdet `id` för uppskattningsjobbet som du vill hämta.

**Begäran**

Följande begäran hämtar resultatet av ett specifikt uppskattningsjobb.

//måste hämta ett förhandsgransknings-ID

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/{PREVIEW_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om uppskattningsjobbet.

```json
{
  "estimatedSize": 0,
  "numRowsToRead": 1,
  "state": "RESULT_READY",
  "profilesReadSoFar": 1,
  "standardError": 0,
  "error": {
    "description": "",
    "traceback": ""
  },
  "profilesMatchedSoFar": 0,
  "totalRows": 1,
  "confidenceInterval": "95%",
  "_links": {
    "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
  }
}
```

## Nästa steg

Nu när du vet hur man hämtar uppskattningsjobbresultat kan du bättre