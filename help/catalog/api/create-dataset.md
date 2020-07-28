---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en datauppsättning
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Skapa en datauppsättning

Om du vill skapa en datauppsättning med [!DNL Catalog] API måste du känna till `$id` värdet för det [!DNL Experience Data Model] (XDM)-schema som datauppsättningen ska baseras på. När du har ett schema-ID kan du skapa en datauppsättning genom att göra en POST-förfrågan till `/datasets` slutpunkten i [!DNL Catalog] API:t.

>[!NOTE]
>
>Det här dokumentet innehåller bara information om hur du skapar ett datauppsättningsobjekt i [!DNL Catalog]. Mer information om hur du skapar, fyller i och övervakar en datauppsättning finns i följande [självstudiekurs](../datasets/create.md).

**API-format**

```HTTP
POST /dataSets
```

**Begäran**

Följande begäran skapar en datauppsättning som refererar till ett tidigare definierat schema.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på datauppsättningen som ska skapas. |
| `schemaRef.id` | URI- `$id` värdet för XDM-schemat som datamängden baseras på. |

>[!NOTE]
>
>I det här exemplet används [parquet](https://parquet.apache.org/documentation/latest/) -filformatet för dess `containerFormat` egenskap. Ett exempel som använder JSON-filformatet finns i utvecklarhandboken för [batchimport](../../ingestion/batch-ingestion/api-overview.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och ett svarsobjekt som består av en array som innehåller ID:t för den nyskapade datauppsättningen i formatet `"@/datasets/{DATASET_ID}"`. Datauppsättnings-ID är en skrivskyddad, systemgenererad sträng som används för att referera till datauppsättningen i API-anrop.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
