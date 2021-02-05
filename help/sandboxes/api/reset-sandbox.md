---
keywords: Experience Platform;hem;populära ämnen;återställ sandlåda
solution: Experience Platform
title: Återställ en sandlåda i API:t
topic: developer guide
description: Utvecklingssandlådor har en "fabriksåterställningsfunktion" som tar bort alla icke-standardresurser från en sandlåda. Du kan återställa en sandlåda genom att göra en PUT-begäran som innehåller sandlådans namn i sökvägen för begäran.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Återställ en sandlåda i API:t

Utvecklingssandlådor har en &quot;fabriksåterställningsfunktion&quot; som tar bort alla icke-standardresurser från en sandlåda. Du kan återställa en sandlåda genom att göra en PUT-begäran som innehåller sandlådans `name` i sökvägen för begäran.

**API-format**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | Egenskapen `name` för den sandlåda som du vill återställa. |

**Begäran**

Följande begäran återställer en sandlåda med namnet&quot;dev-2&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `action` | Den här parametern måste anges med värdet &quot;reset&quot; i nyttolasten för begäran för att sandlådan ska kunna återställas. |

**Svar**

Ett lyckat svar returnerar informationen om den uppdaterade sandlådan, vilket visar att `state` är &quot;återställa&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>När en sandlåda har återställts tar det ca 15 minuter att etablera den av systemet. När sandlådan har etablerats blir den `state`&quot;aktiv&quot; eller&quot;misslyckades&quot;.