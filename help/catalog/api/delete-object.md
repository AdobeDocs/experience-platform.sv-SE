---
keywords: Experience Platform;hem;populära ämnen;ta bort ett objekt;katalogtjänst;api
solution: Experience Platform
title: Ta bort ett objekt i API:t
description: Du kan ta bort ett Catalog-objekt genom att ange dess ID i sökvägen till en DELETE-begäran.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Ta bort ett objekt i API:t

Du kan ta bort en [!DNL Catalog] genom att ange dess ID i sökvägen för en DELETE-begäran.

>[!WARNING]
>
>Var extra försiktig när du tar bort objekt, eftersom det inte går att ångra och kan ge upphov till ändringar på andra ställen i [!DNL Experience Platform].

**API-format**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>The `DELETE /batches/{ID}` slutpunkten har tagits bort. Om du vill ta bort en grupp bör du använda [API för gruppinmatning](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska tas bort. Giltiga objekt är: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran tar bort en datauppsättning vars ID har angetts i sökvägen för begäran.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den borttagna datauppsättningen. Detta ID ska matcha det som skickades i DELETE-begäran. Om en GET-begäran utförs på det borttagna objektet returneras HTTP-status 404 (Hittades inte), vilket bekräftar att datauppsättningen har tagits bort.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Om nej [!DNL Catalog] -objekt matchar det ID som anges i din begäran. Du kan fortfarande få HTTP-statuskod 200, men svarsmatrisen är tom.
