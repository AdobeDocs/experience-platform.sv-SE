---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över Adobe Experience Platform batchmatning
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# Översikt över batchintag

Med API:t för gruppinmatning kan du importera data till Adobe Experience Platform som gruppfiler. Data som importeras kan vara profildata från en platt fil i ett CRM-system (till exempel en parquet-fil) eller data som följer ett känt schema i XDM-registret (Experience Data Model).

API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) datainmatning innehåller ytterligare information om dessa API-anrop.

I följande diagram visas batchintagsprocessen:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Använda API

Med API:t för datainmatning kan du importera data som grupper (en dataenhet som består av en eller flera filer som ska importeras som en enda enhet) till Experience Platform i tre grundläggande steg:

1. Skapa en ny batch.
2. Överför filer till en angiven datauppsättning som matchar datans XDM-schema.
3. Signalera slutet av gruppen.


### Krav för datainmatning

- Data som ska överföras måste vara i något av formaten Parquet eller JSON.
- En datauppsättning som skapats i [katalogtjänsterna](../../catalog/home.md).
- Innehållet i parquet-filen måste matcha en delmängd av schemat i den datauppsättning som överförs till.
- Ha din unika åtkomsttoken efter autentisering.

### Bästa praxis för gruppkonsumtion

- Den rekommenderade batchstorleken är mellan 256 MB och 100 GB.
- Varje grupp bör innehålla högst 1 500 filer.

Om du vill överföra en fil som är större än 512 MB måste filen delas upp i mindre segment. Instruktioner om hur du överför en stor fil finns [här](#large-file-upload---create-file).

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla förfrågningar till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

### Skapa en batch

Innan data kan läggas till i en datauppsättning måste de länkas till en batch, som senare överförs till en angiven datauppsättning.

```http
POST /batches
```

**Begäran**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `datasetId` | ID:t för datauppsättningen som filerna ska överföras till. |

**Svar**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | ID för den batch som precis skapades (används i efterföljande begäranden). |
| `relatedObjects.id` | ID:t för datauppsättningen som filerna ska överföras till. |

## Filöverföring

När du har skapat en ny batch för överföring kan filer sedan överföras till en viss datauppsättning.

Du kan överföra filer med API:t för överföring av **liten fil**. Om filerna är för stora och gatewaygränsen överskrids (t.ex. utökade tidsgränser, begäranden om kroppsstorlek överskrids och andra begränsningar) kan du växla till API:t för **stor filöverföring**. Denna API överför filen i segment och sammanfogar data med API-anropet **Large File Upload Complete** .

>[!NOTE]
>
>Exemplen nedan använder [filformatet parquet](https://parquet.apache.org/documentation/latest/) . Ett exempel som använder JSON-filformatet finns i utvecklarhandboken för [batchimport](./api-overview.md).

### Liten filöverföring

När en batch har skapats kan data överföras till en befintlig datauppsättning.  Filen som överförs måste matcha det refererade XDM-schemat.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | Batchens ID. |
| `{DATASET_ID}` | ID för datauppsättningen som ska överföras. |
| `{FILE_NAME}` | Namnet på filen så som den kommer att visas i datauppsättningen. |

**Begäran**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Sökvägen till och filnamnet på filen som ska överföras till datauppsättningen. |

**Svar**

```JSON
#Status 200 OK, with empty response body
```

### Stor filöverföring - skapa fil

Om du vill överföra en stor fil måste filen delas upp i mindre segment och överföras en åt gången.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | Batchens ID. |
| `{DATASET_ID}` | ID:t för datauppsättningen som importerar filerna. |
| `{FILE_NAME}` | Namnet på filen så som den kommer att visas i datauppsättningen. |

**Begäran**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Svar**

```JSON
#Status 201 CREATED, with empty response body
```

### Stor filöverföring - överför efterföljande delar

När filen har skapats kan alla efterföljande segment överföras genom upprepade PATCH-begäranden, en för varje avsnitt i filen.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | Batchens ID. |
| `{DATASET_ID}` | ID:t för datauppsättningen som filerna ska överföras till. |
| `{FILE_NAME}` | Namnet på filen så som den kommer att visas i datauppsättningen. |

**Begäran**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Sökvägen till och filnamnet på filen som ska överföras till datauppsättningen. |

**Svar**

```JSON
#Status 200 OK, with empty response
```

## Slutförande av signalbatch

När alla filer har överförts till gruppen kan gruppen signaleras för slutförande. På så sätt skapas **Catalog DataSetFile** -posterna för de slutförda filerna och kopplas till den grupp som genereras ovan. Katalogbatchen markeras sedan som lyckad, vilket utlöser flödesomgångar för att importera tillgängliga data.

**Begäran**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | ID för den batch som ska överföras till datauppsättningen. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Svar**

```JSON
#Status 200 OK, with empty response
```

## Kontrollera batchstatus

I väntan på att filerna ska överföras till gruppen kan batchens status kontrolleras för att se dess förlopp.

**API-format**

```http
GET /batch/{BATCH_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | ID för den batch som kontrolleras. |

**Begäran**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Svar**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{USER_ID}` | ID för den användare som skapade eller uppdaterade gruppen. |

Fältet `"status"` visar den aktuella statusen för den begärda batchen. Batcherna kan ha något av följande lägen:

## Status för batchförbrukning

| Status | Beskrivning |
| ------ | ----------- |
| Övergiven | Batchen har inte slutförts inom den förväntade tidsramen. |
| Avbruten | En avbrottsåtgärd har **explicit** anropats (via API:t för gruppinmatning) för den angivna gruppen. När batchen är i ett **inläst** tillstånd kan den inte avbrytas. |
| Aktiv | Batchen har befordrats och är tillgänglig för nedladdning. Den här statusen kan användas utan **fel**. |
| Borttagen | Data för batchen har tagits bort helt. |
| Misslyckades | Ett terminaltillstånd som antingen beror på felaktig konfiguration och/eller felaktiga data. Data för en misslyckad batch visas **inte** . Den här statusen kan användas utan **fel**. |
| Inaktiv | Batchen befordrades men har återförts eller gått ut. Batchen är inte längre tillgänglig för nedströmsförbrukning. |
| Inläst | Data för batchen har slutförts och batchen är klar för befordran. |
| Läser in | Data för den här batchen överförs och batchen är **inte** klar att befordras. |
| Försöker igen | Data för den här batchen bearbetas. På grund av ett system- eller övergående fel misslyckades dock batchen. Detta innebär att batchen provas igen. |
| Mellanlagrad | Mellanlagringsfasen av befordringsprocessen för en batch är slutförd och åtkomsten har körts. |
| Mellanlagring | Data för batchen bearbetas. |
| Stängd | Data för batchen bearbetas. Batchkampanjen har dock avstannat efter ett antal försök. |