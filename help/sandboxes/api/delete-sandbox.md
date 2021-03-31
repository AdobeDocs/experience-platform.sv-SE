---
keywords: Experience Platform;hem;populära ämnen;ta bort sandlåda
solution: Experience Platform
title: Ta bort en sandlåda i API:t
topic: utvecklarhandbok
description: Du kan ta bort en sandlåda genom att göra en DELETE-begäran som innehåller sandlådans namn i sökvägen för begäran.
translation-type: tm+mt
source-git-commit: e7a80dbfdd2d59e4997f6e227b5c2cf336e5a0f6
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Ta bort en sandlåda i API:t

Du kan ta bort en sandlåda genom att göra en DELETE-begäran som innehåller sandlådans `name` i sökvägen för begäran.

>[!NOTE]
>
>Om du gör det här API-anropet uppdateras sandlådans `status`-egenskap till &quot;removed&quot; och inaktiveras. GET-begäranden kan fortfarande hämta sandlådans information efter att den har tagits bort.

**API-format**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | `name` för den sandlåda som du vill ta bort. |

**Begäran**

Följande begäran tar bort en sandlåda med namnet&quot;dev-2&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett lyckat svar returnerar sandlådans uppdaterade information, vilket visar att dess `state` är &quot;borttagen&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
