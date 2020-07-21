---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Listnamn på behörigheter och resurstyper
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '123'
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
