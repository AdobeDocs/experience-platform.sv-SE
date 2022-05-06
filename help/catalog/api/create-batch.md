---
keywords: Experience Platform;hem;populära ämnen;skapa grupp;katalogtjänst;api
solution: Experience Platform
title: Skapa en grupp i API:t
topic-legacy: developer guide
description: Du kan skapa en grupp genom att göra en POST-förfrågan till slutpunkten /batches i katalog-API:t.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Skapa en batch

För att en datauppsättning ska kunna importera data måste den ha en associerad batch. Använda `id` värdet för en befintlig datauppsättning kan du skapa en batch genom att göra en begäran om POST till `/batches` slutpunkt i [!DNL Catalog] API.

**API-format**

```HTTP
POST /batches
```

**Begäran**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `datasetId` | The `id` av den datauppsättning som gruppen ska kopplas till. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och ett svarsobjekt som innehåller information om den nyligen skapade gruppen, inklusive dess `id`, en skrivskyddad, systemgenererad sträng.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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
