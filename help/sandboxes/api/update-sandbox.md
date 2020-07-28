---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Uppdatera en sandlåda
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 1%

---


# Uppdatera en sandlåda

Du kan uppdatera ett eller flera fält i en sandlåda genom att göra en PATCH-begäran som innehåller sandlådans sökväg och den egenskap som ska uppdateras i nyttolasten för begäran. `name`

>[!NOTE]
>
>För närvarande kan bara en sandlådeegenskap `title` uppdateras.

**API-format**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | Egenskapen `name` för den sandlåda som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar egenskapen `title` för sandlådan med namnet&quot;dev-2&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) med information om den nyligen uppdaterade sandlådan.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
