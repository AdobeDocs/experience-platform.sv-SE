---
keywords: Experience Platform;home;popular topics;access control permissions;access control resource types;access control api
solution: Experience Platform
title: Listnamn på behörigheter och resurstyper
topic: developer guide
description: Med åtkomstkontrollen i Adobe Experience Platform kan du hantera roller och behörigheter för olika plattformsfunktioner med Adobe Admin Console. Du kan lista namnen på alla behörigheter och resurstyper genom att göra en GET-begäran till /acl/reference-slutpunkten. Dessa namn kan sedan användas i API-anrop för att visa gällande principer för den aktuella användaren.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Listnamn på behörigheter och resurstyper

Du kan lista namnen på alla behörigheter och resurstyper genom att göra en GET-begäran till `/acl/reference` slutpunkten. Dessa namn kan sedan användas i API-anrop för att [visa gällande principer](./effective-policies.md) för den aktuella användaren.

En **behörighet** är en princip som hanteras via Adobe Admin Console och mappar till noll eller flera resurstypsprofiler. En **resurstyp** är en princip som möjliggör funktioner för att läsa, skriva och/eller ta bort en viss typ av [!DNL Platform] resurs (till exempel datauppsättningar eller scheman).

**API-format**

```http
GET /acl/reference
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Svar**

Ett lyckat svar returnerar ett `permissions` objekt och ett `resource-types` objekt som vart och ett innehåller en fullständig lista med namn för åtkomstbehörigheter respektive resurstyper.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
