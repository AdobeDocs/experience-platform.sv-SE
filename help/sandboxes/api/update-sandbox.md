---
keywords: Experience Platform;hem;populära ämnen;uppdateringssandlåda
solution: Experience Platform
title: Uppdatera en sandlåda i API:t
topic: developer guide
description: Du kan uppdatera ett eller flera fält i en sandlåda genom att göra en PATCH-begäran som innehåller sandlådans namn i sökvägen för begäran och egenskapen som ska uppdateras i nyttolasten för begäran.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Uppdatera en sandlåda i API:t

Du kan uppdatera ett eller flera fält i en sandlåda genom att göra en PATCH-begäran som innehåller sandlådans `name` i sökvägen för begäran och egenskapen som ska uppdateras i nyttolasten för begäran.

>[!NOTE]
>
>För närvarande kan bara egenskapen `title` för en sandlåda uppdateras.

**API-format**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | Egenskapen `name` för den sandlåda som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar egenskapen `title` för sandlådan med namnet &quot;dev-2&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) med information om den nyligen uppdaterade sandlådan.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
