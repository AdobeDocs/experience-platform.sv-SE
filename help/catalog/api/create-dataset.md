---
keywords: Experience Platform;hem;populära ämnen;datauppsättning;datauppsättning;skapa en datauppsättning;skapa datauppsättning;aktivera datauppsättning
solution: Experience Platform
title: Skapa en datauppsättning i API:t
description: Det här dokumentet beskriver hur du skapar ett datauppsättningsobjekt i katalogtjänstens API.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Skapa en datauppsättning i API:t

För att skapa en datauppsättning med [!DNL Catalog] API, du måste känna till `$id` värdet på [!DNL Experience Data Model] (XDM)-schema som datauppsättningen ska baseras på. När du har ett schema-ID kan du skapa en datauppsättning genom att göra en POST-förfrågan till `/datasets` slutpunkt i [!DNL Catalog] API.

>[!NOTE]
>
>Det här dokumentet innehåller bara information om hur du skapar ett datauppsättningsobjekt i [!DNL Catalog]. För fullständiga steg om hur du skapar, fyller i och övervakar en datauppsättning, se följande [självstudiekurs](../datasets/create.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på datauppsättningen som ska skapas. |
| `schemaRef.id` | URI `$id` värdet för XDM-schemat som datauppsättningen baseras på. |
| `schemaRef.contentType` | Anger schemats format och version. Se avsnittet om [schemaversion](../../xdm/api/getting-started.md#versioning) i XDM API-guiden för mer information. |

>[!NOTE]
>
>I det här exemplet används [Apache Parquet](https://parquet.apache.org/docs/) filformat för dess `containerFormat` -egenskap. Ett exempel som använder JSON-filformatet finns i [Utvecklarhandbok för batchintag](../../ingestion/batch-ingestion/api-overview.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och ett svarsobjekt som består av en array som innehåller ID:t för den nyskapade datauppsättningen i formatet `"@/datasets/{DATASET_ID}"`. Datauppsättnings-ID är en skrivskyddad, systemgenererad sträng som används för att referera till datauppsättningen i API-anrop.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
