---
keywords: Experience Platform;hem;populära ämnen;hitta sandlåda;leta upp en sandlåda
solution: Experience Platform
title: Söka efter en sandlåda i API:t
topic: utvecklarhandbok
description: Du kan söka efter en enskild sandlåda genom att göra en GET-begäran som innehåller sandlådans name-egenskap i sökvägen för begäran.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Söka efter en sandlåda i API:t

Du kan söka efter en enskild sandlåda genom att göra en GET-begäran som innehåller sandlådans `name`-egenskap i sökvägen för begäran.

**API-format**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | Egenskapen `name` för den sandlåda som du vill söka efter. |

**Begäran**

Följande begäran hämtar en sandlåda med namnet &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar informationen om sandlådan, inklusive dess `name`, `title`, `state` och `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på sandlådan. Används för uppslagssyften i API-anrop. |
| `title` | Visningsnamnet för sandlådan. |
| `state` | Sandlådans aktuella bearbetningstillstånd. En sandlådestatus kan vara något av följande: <ul><li>**skapa**: Sandlådan har skapats, men etableras fortfarande av systemet.</li><li>**aktiv**: Sandlådan skapas och är aktiv.</li><li>**misslyckades**: På grund av ett fel kunde sandlådan inte etableras av systemet och är inaktiverad.</li><li>**borttagen**: Sandlådan har inaktiverats manuellt.</li></ul> |
| `type` | Sandlådetypen, antingen &quot;development&quot; eller &quot;production&quot;. |
| `isDefault` | En boolesk egenskap som anger om den här sandlådan är standardsandlådan för organisationen. Vanligtvis är det här produktionssandlådan. |
| `eTag` | En identifierare för en specifik version av sandlådan. Detta värde används för versionskontroll och cachelagring av effektivitet och uppdateras varje gång en ändring görs i sandlådan. |