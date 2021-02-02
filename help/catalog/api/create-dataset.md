---
keywords: Experience Platform;hem;populära ämnen;datauppsättning;datauppsättning;skapa en datauppsättning;skapa datauppsättning;aktivera datauppsättning
solution: Experience Platform
title: Skapa en datauppsättning
topic: developer guide
description: I det här dokumentet beskrivs hur du skapar ett datauppsättningsobjekt i Katalog.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Skapa en datauppsättning

Om du vill skapa en datauppsättning med API:t [!DNL Catalog] måste du känna till `$id`-värdet för det [!DNL Experience Data Model] (XDM)-schema som datauppsättningen ska baseras på. När du har ett schema-ID kan du skapa en datauppsättning genom att göra en POST-förfrågan till `/datasets`-slutpunkten i [!DNL Catalog]-API:t.

>[!NOTE]
>
>Det här dokumentet innehåller bara information om hur du skapar ett datauppsättningsobjekt i [!DNL Catalog]. Fullständiga anvisningar om hur du skapar, fyller i och övervakar en datauppsättning finns i följande [självstudiekurs](../datasets/create.md).

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
| `schemaRef.id` | URI-värdet `$id` för XDM-schemat som datamängden baseras på. |

>[!NOTE]
>
>I det här exemplet används filformatet [Apache Parquet](https://parquet.apache.org/documentation/latest/) för egenskapen `containerFormat`. Ett exempel som använder JSON-filformatet finns i [Utvecklarhandbok för gruppfrågor](../../ingestion/batch-ingestion/api-overview.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och ett svarsobjekt som består av en array som innehåller ID:t för den nyskapade datauppsättningen i formatet `"@/datasets/{DATASET_ID}"`. Datauppsättnings-ID är en skrivskyddad, systemgenererad sträng som används för att referera till datauppsättningen i API-anrop.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
