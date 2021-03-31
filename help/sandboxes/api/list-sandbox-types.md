---
keywords: Experience Platform;hem;populära ämnen;lissandlådor
solution: Experience Platform
title: Lista över sandlådetyper som stöds i API:t
topic: utvecklarhandbok
description: Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-begäran till slutpunkten /sandboxTypes.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Visa sandlådetyper som stöds i API

Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-begäran till `/sandboxTypes`-slutpunkten.

**API-format**

```http
GET /sandboxTypes
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett lyckat svar returnerar en lista med sandlådetyper som stöds för din organisation.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
