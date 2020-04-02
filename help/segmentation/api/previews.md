---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Förhandsvisningar
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Utvecklarhandbok för förhandsvisningar

intro

- Skapa en ny förhandsgranskning
- Hämta resultat från en viss förhandsvisning
- Avbryt eller ta bort en viss förhandsgranskning

## Komma igång

API-slutpunkterna som används i den här guiden ingår i segmenterings-API:t. Läs utvecklarhandboken för [segmentering innan du fortsätter](./getting-started.md).

Avsnittet [](./getting-started.md#getting-started) Komma igång i utvecklarhandboken för segmentering innehåller länkar till relaterade ämnen, en guide till hur du läser exempelanropen för API i dokumentet och viktig information om vilka huvuden som krävs för att anropa något Experience Platform-API.

## Skapa en ny förhandsgranskning

Du kan skapa en ny förhandsgranskning genom att göra en POST-begäran till `/preview` slutpunkten.

**API-format**

```http
POST /preview
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

brödinformation

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) med information om den nya förhandsgranskningen.

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

svarsinformation, x-location finns inte.

## Hämta resultat från en viss förhandsvisning

Du kan hämta detaljerad information om en viss förhandsgranskning genom att göra en GET-begäran till `/preview` slutpunkten och ange förhandsgranskningens `id` värde i sökvägen för begäran.

**API-format**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: Värdet `id` för den förhandsgranskning som du vill hämta.

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna förhandsgranskningen.

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## Avbryt eller ta bort en viss förhandsgranskning

Du kan ta bort en viss förhandsgranskning genom att göra en DELETE-begäran till `/preview` slutpunkten och ange förhandsgranskningens `id` värde i begärandesökvägen.

**API-format**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` Värdet `id` för den förhandsvisning som du vill ta bort.

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med följande meddelande:

```json
{
  "status": true,
  "message": "KILLED"
}
```

## Nästa steg
