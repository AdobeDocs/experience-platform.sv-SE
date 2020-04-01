---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en datauppsättning
topic: developer guide
translation-type: tm+mt
source-git-commit: a25ca22fb8ec9eb95f74e4fd76a7f18e87343085

---


# Skapa en batch

För att en datauppsättning ska kunna importera data måste den ha en associerad batch. Med hjälp av `id` värdet för en befintlig datauppsättning kan du skapa en batch genom att göra en POST-begäran till `/batches` slutpunkten i katalog-API:t.

**API-format**

```HTTP
POST /batches
```

**Begäran**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `datasetId` | Den datauppsättning som gruppen ska kopplas `id` till. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och ett svarsobjekt som innehåller information om den nyligen skapade gruppen, inklusive dess `id`skrivskyddade, systemgenererade sträng.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
