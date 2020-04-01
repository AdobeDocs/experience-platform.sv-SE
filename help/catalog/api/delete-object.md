---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ta bort ett objekt
topic: developer guide
translation-type: tm+mt
source-git-commit: 85b497d87fcfb54f390302036ce24c98c6dba6ff

---


# Ta bort ett objekt

Du kan ta bort ett Catalog-objekt genom att ange dess ID i sökvägen för en DELETE-begäran.

>[!WARNING] Var extra försiktig när du tar bort objekt, eftersom detta inte kan ångras och kan ge upphov till nya ändringar någon annanstans i Experience Platform.

**API-format**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av katalogobjekt som ska tas bort. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran tar bort en datauppsättning vars ID har angetts i sökvägen för begäran.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den borttagna datauppsättningen. Detta ID ska matcha det som skickades i DELETE-begäran. Om du utför en GET-begäran på det borttagna objektet returneras HTTP-status 404 (Hittades inte), vilket bekräftar att datauppsättningen har tagits bort.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE] Om inga katalogobjekt matchar det ID som angavs i din begäran kan du ändå få HTTP-statuskoden 200, men svarsmatrisen är tom.
