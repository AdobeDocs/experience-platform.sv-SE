---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visa tillgängliga namnutrymmen
topic: API guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 3%

---


# Visa tillgängliga namnutrymmen

**API-format**

```http
GET /idnamespace/identities
```

**Begäran**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller en array med objekt, där varje objekt representerar ett tillgängligt namnutrymme. Namnutrymmen med värdet &quot;[!UICONTROL custom]&quot; för &quot;[!UICONTROL false]&quot; är standardnamnutrymmen, medan de med värdet &quot;[!UICONTROL custom]&quot; för &quot;[!UICONTROL true]&quot; är namnutrymmen som din organisation har skapat.

>[!NOTE] Svaret har trunkerats för utrymme.

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## Nästa steg

Gå till nästa självstudiekurs för att [skapa ett anpassat namnutrymme](./create-custom-namespace.md)