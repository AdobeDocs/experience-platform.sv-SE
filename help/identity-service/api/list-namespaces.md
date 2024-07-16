---
keywords: Experience Platform;hem;populära ämnen;namnutrymmeslista;namnlista
solution: Experience Platform
title: Lista tillgängliga identitetsnamnutrymmen
description: Visa alla tillgängliga namnutrymmen.
role: Developer
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 0%

---

# Visa tillgängliga identitetsnamnutrymmen

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller en array med objekt, där varje objekt representerar ett tillgängligt namnutrymme. Namnutrymmen med värdet [!UICONTROL custom] för [!UICONTROL false] är standardnamnutrymmen, medan de med värdet [!UICONTROL custom] för [!UICONTROL true] är namnutrymmen som din organisation har skapat.

>[!NOTE]
>
>Svaret har trunkerats för utrymme.

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
