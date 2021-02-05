---
keywords: Experience Platform;hem;populära ämnen;namnutrymmeslista;namnlista
solution: Experience Platform
title: Lista tillgängliga identitetsnamnutrymmen
topic: API guide
description: Visa alla tillgängliga namnutrymmen.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 2%

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Gå vidare till nästa självstudiekurs för att [skapa ett anpassat namnutrymme](./create-custom-namespace.md)