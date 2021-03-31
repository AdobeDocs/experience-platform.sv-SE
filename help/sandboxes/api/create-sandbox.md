---
keywords: Experience Platform;hem;populära ämnen;Sandlåda;sandlåda
solution: Experience Platform
title: Skapa en sandlåda i API:t
topic: utvecklarhandbok
description: Du kan skapa en ny sandlåda genom att göra en POST-förfrågan till slutpunkten "/sandbox".
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Skapa en sandlåda i API:t

Du kan skapa en utvecklings- eller produktionssandlåda genom att göra en POST-förfrågan till `/sandboxes`-slutpunkten.

## Skapa en utvecklingssandlåda

Om du vill skapa en utvecklingssandlåda gör du en POST till `/sandboxes`-slutpunkten och anger värdet `development` för egenskapen `type`.

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Den identifierare som ska användas för att komma åt sandlådan i framtida begäranden. Detta värde måste vara unikt och det bästa sättet är att göra det så beskrivande som möjligt. Värdet får inte innehålla blanksteg eller specialtecken. |
| `title` | Ett läsbart namn som används för visning i användargränssnittet för plattformen. |
| `type` | Den typ av sandlåda som ska skapas. Värdet för egenskapen `type` kan vara antingen utveckling eller produktion. |

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

## Skapa en produktionssandlåda

>[!NOTE]
>
>Funktionen Flera produktionssandlådor är i betaversion.

Om du vill skapa en produktionssandlåda gör du en POST till `/sandboxes`-slutpunkten och anger värdet `production` för egenskapen `type`.

**API-format**

```http
POST /sandboxes
```

**Begäran**

Följande begäran skapar en ny produktionssandlåda med namnet&quot;test-prod-sandbox&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Den identifierare som ska användas för att komma åt sandlådan i framtida begäranden. Detta värde måste vara unikt och det bästa sättet är att göra det så beskrivande som möjligt. Värdet får inte innehålla blanksteg eller specialtecken. |
| `title` | Ett läsbart namn som används för visning i användargränssnittet för plattformen. |
| `type` | Den typ av sandlåda som ska skapas. Värdet för egenskapen `type` kan vara antingen utveckling eller produktion. |

**Svar**

Ett lyckat svar returnerar informationen om den nyligen skapade sandlådan, vilket visar att `state` är &quot;creating&quot;.

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
