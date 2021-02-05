---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontrollbehörigheter;åtkomstkontrollsresurstyper;åtkomstkontrolls-API
solution: Experience Platform
title: Referens-API-slutpunkt
topic: developer guide
description: Med åtkomstkontrollen i Adobe Experience Platform kan du hantera roller och behörigheter för olika plattformsfunktioner med Adobe Admin Console. Du kan lista namnen på alla behörigheter och resurstyper genom att göra en GET-begäran till /acl/reference-slutpunkten i åtkomstkontrolls-API:t. Dessa namn kan sedan användas i API-anrop för att visa gällande principer för den aktuella användaren.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Referensslutpunkt

Du kan lista namnen på alla behörigheter och resurstyper genom att göra en GET-begäran till `/acl/reference`-slutpunkten. Dessa namn kan sedan användas i API-anrop för att [visa gällande principer](./effective-policies.md) för den aktuella användaren.

En behörighet är en princip som hanteras via Adobe Admin Console och mappar till noll eller flera resurstypsprofiler. En resurstyp är en princip som möjliggör läsning, skrivning och/eller borttagning av funktioner för en viss typ av [!DNL Platform]-resurs (till exempel datauppsättningar eller scheman).

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

Ett godkänt svar returnerar ett `permissions`-objekt och ett `resource-types`-objekt som alla innehåller en fullständig lista med namn för åtkomstbehörigheter respektive resurstyper.

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
