---
keywords: Experience Platform;hem;populära ämnen;lissandlådor
solution: Experience Platform
title: Lista över sandlådetyper som stöds i API:t
topic-legacy: developer guide
description: Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-begäran till slutpunkten /sandboxTypes.
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '81'
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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
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
