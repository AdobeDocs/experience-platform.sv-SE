---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: Visa sandlådetyper som stöds
topic: developer guide
description: Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-begäran till slutpunkten /sandboxTypes.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 0%

---


# Visa sandlådetyper som stöds

Du kan hämta en lista över sandlådetyper som stöds för din organisation genom att göra en GET-förfrågan till `/sandboxTypes` slutpunkten.

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
