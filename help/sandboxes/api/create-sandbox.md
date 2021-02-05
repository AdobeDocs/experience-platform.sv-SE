---
keywords: Experience Platform;hem;populära ämnen;Sandlåda;sandlåda
solution: Experience Platform
title: Skapa en sandlåda i API:t
topic: developer guide
description: Du kan skapa en ny sandlåda genom att göra en POST-förfrågan till slutpunkten "/sandbox".
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Skapa en sandlåda i API:t

Du kan skapa en ny sandlåda genom att göra en POST-förfrågan till `/sandboxes`-slutpunkten.

**API-format**

```http
POST /sandboxes
```

**Begäran**

Följande begäran skapar en ny utvecklingssandlåda med namnet&quot;dev-3&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Den identifierare som ska användas för att komma åt sandlådan i framtida begäranden. Detta värde måste vara unikt och det bästa sättet är att göra det så beskrivande som möjligt. Får inte innehålla blanksteg eller versala bokstäver. |
| `title` | Ett läsbart namn som används för visning i användargränssnittet för plattformen. |
| `type` | Den typ av sandlåda som ska skapas. För närvarande kan endast sandlådor av typen&quot;utveckling&quot; skapas av en organisation. |

**Svar**

Ett lyckat svar returnerar informationen om den nyligen skapade sandlådan, vilket visar att `state` är &quot;creating&quot;.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Det tar cirka 15 minuter att tilldela sandlådor av systemet, varefter deras `state` blir&quot;aktiva&quot; eller&quot;misslyckades&quot;.
