---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontrollbehörigheter;åtkomstkontrollsresurstyper;åtkomstkontrolls-API
solution: Experience Platform
title: Referens-API-slutpunkt
topic-legacy: developer guide
description: Med referensslutpunkten i API:t för åtkomstkontroll kan du visa namnen på tillgängliga behörigheter och resurstyper, som sedan kan användas för att visa effektiva åtkomstkontrollprinciper för den aktuella användaren.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Referensslutpunkt

Du kan visa namnen på alla behörigheter och resurstyper genom att göra en GET-förfrågan till `/acl/reference` slutpunkt. Dessa namn kan sedan användas i API-anrop till [visa effektiva åtkomstkontrollprinciper](./effective-policies.md) för den aktuella användaren.

En behörighet är en princip som hanteras via Adobe Admin Console och mappar till noll eller flera resurstypsprofiler. En resurstyp är en princip som möjliggör läsning, skrivning och/eller borttagning av funktioner för en viss typ av [!DNL Platform] resurs (t.ex. datauppsättningar eller scheman).

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett godkänt svar returnerar ett `permissions` objekt och `resource-types` -objekt som vart och ett innehåller en fullständig lista med namn för åtkomstbehörigheter eller resurstyper.

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
