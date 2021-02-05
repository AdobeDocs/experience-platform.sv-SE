---
keywords: Experience Platform;hem;populära ämnen;ta bort ett objekt;katalogtjänst;api
solution: Experience Platform
title: Ta bort ett objekt i API:t
topic: developer guide
description: Du kan ta bort ett Catalog-objekt genom att ange dess ID i sökvägen till en DELETE-begäran.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Ta bort ett objekt i API:t

Du kan ta bort ett [!DNL Catalog]-objekt genom att ange dess ID i sökvägen för en DELETE-begäran.

>[!WARNING]
>
>Var extra försiktig när du tar bort objekt, eftersom detta inte kan ångras och kan leda till brytningsändringar någon annanstans i [!DNL Experience Platform].

**API-format**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Slutpunkten `DELETE /batches/{ID}` har tagits bort. Om du vill ta bort en grupp bör du använda [API för gruppinmatning](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska tas bort. Giltiga objekt är: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

Ett lyckat svar returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den borttagna datauppsättningen. Detta ID ska matcha det som skickades i DELETE-begäran. Om en GET-begäran utförs på det borttagna objektet returneras HTTP-status 404 (Hittades inte), vilket bekräftar att datauppsättningen har tagits bort.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Om inga [!DNL Catalog]-objekt matchar det ID som angavs i din begäran kan du ändå få HTTP-statuskoden 200, men svarsmatrisen är tom.
