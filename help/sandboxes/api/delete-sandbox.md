---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ta bort en sandlåda
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 1%

---


# Ta bort en sandlåda

Du kan ta bort en sandlåda genom att göra en DELETE-begäran som innehåller sandlådans `name` i begärandesökvägen.

>[!NOTE]
>
>Om du gör det här API-anropet uppdateras sandlådeegenskapen till&quot;Borttagen&quot; och den inaktiveras. `status` GET-begäranden kan fortfarande hämta sandlådans information efter att den har tagits bort.

**API-format**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | Den sandlåda `name` som du vill ta bort. |

**Begäran**

Följande begäran tar bort en sandlåda med namnet&quot;dev-2&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar sandlådans uppdaterade information, vilket visar att den `state` &quot;har tagits bort&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
