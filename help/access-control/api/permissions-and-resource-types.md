---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontrollbehörigheter;åtkomstkontrollsresurstyper;åtkomstkontrolls-API
solution: Experience Platform
title: Referens-API-slutpunkt
description: Med referensslutpunkten i API:t för åtkomstkontroll kan du visa namnen på tillgängliga behörigheter och resurstyper, som sedan kan användas för att visa effektiva åtkomstkontrollprinciper för den aktuella användaren.
role: Developer
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Referensslutpunkt

>[!NOTE]
>
>Om en användartoken skickas måste användaren av token ha rollen&quot;org admin&quot; för den begärda organisationen.

Du kan lista namnen på alla behörigheter och resurstyper genom att göra en GET-förfrågan till slutpunkten `/acl/reference`. Dessa namn kan sedan användas i API-anrop för att [visa effektiva åtkomstkontrollprinciper](./effective-policies.md) för den aktuella användaren.

En behörighet är en princip som hanteras via Adobe Admin Console och mappar till noll eller flera resurstypsprofiler. En resurstyp är en princip som aktiverar läs-, skriv- och/eller borttagningsfunktioner för en viss typ av [!DNL Platform]-resurs (till exempel datauppsättningar eller scheman).

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

Ett godkänt svar returnerar ett `permissions`-objekt och ett `resource-types`-objekt, där vart och ett innehåller en fullständig lista med namn för åtkomstbehörigheter respektive resurstyper.

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
