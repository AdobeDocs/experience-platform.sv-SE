---
keywords: Experience Platform;hem;populära ämnen;batchingång;batchingösning;ingift;utvecklarguide;api guide;upload;ingest Parquet;ingest json;
solution: Experience Platform
title: API-guide för gruppinmatning
description: Det här dokumentet innehåller en omfattande guide för utvecklare som arbetar med API:er för gruppimport för Adobe Experience Platform.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '2412'
ht-degree: 1%

---

# Utvecklarhandbok för batchintag

Det här dokumentet innehåller en omfattande guide till hur du använder [API-slutpunkter för batchimport](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) i Adobe Experience Platform. En översikt över API:er för gruppinmatning, inklusive förutsättningar och bästa praxis, får du om du börjar med att läsa [API-översikt över batchimport](overview.md).

I bilagan till det här dokumentet finns information om [formatera data som ska användas för förtäring](#data-transformation-for-batch-ingestion), inklusive exempel på CSV- och JSON-datafiler.

## Komma igång

API-slutpunkterna som används i den här handboken är en del av [API för gruppinmatning](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Gruppinmatning tillhandahålls via en RESTful API där du kan utföra grundläggande CRUD-åtgärder mot de objekttyper som stöds.

Läs igenom [API-översikt över batchimport](overview.md) och [komma igång-guide](getting-started.md).

## Importera JSON-filer

>[!NOTE]
>
>Följande steg gäller för små filer (256 MB eller mindre). Om du råkar ut för en timeout för gatewayen eller begär fel i brödstorlek måste du växla till stor filöverföring.

### Skapa batch

För det första måste du skapa en batch med JSON som indataformat. När du skapar gruppen måste du ange ett datauppsättnings-ID. Du måste också se till att alla filer som överförs som en del av gruppen följer XDM-schemat som är länkat till den angivna datauppsättningen.

>[!NOTE]
>
>Exemplen nedan är för enradig JSON. Om du vill importera flerradig JSON, `isMultiLineJson` flagga måste anges. Mer information finns i [felsökningsguide för batchöverföring](./troubleshooting.md).

**API-format**

```http
POST /batches
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | ID för referensdatauppsättningen. |

**Svar**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |

### Överför filer

Nu när du har skapat en batch kan du använda batch-ID:t från svaret när gruppen skapades för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

>[!NOTE]
>
>I avsnittet Bilaga finns en [exempel på en korrekt formaterad JSON-datafil](#data-transformation-for-batch-ingestion).

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. Se till att du använder ett unikt filnamn så att det inte hamnar i konflikt med en annan fil för gruppen med filer som skickas. |

**Begäran**

>[!NOTE]
>
>API:t stöder överföring till en del. Kontrollera att innehållstypen är application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. Den här filsökvägen är den lokala filsökvägen, till exempel `acme/customers/campaigns/summer.json`. |

**Svar**

```http
200 OK
```

### Slutför batch

När du har överfört alla olika delar av filen måste du signalera att alla data har överförts och att gruppen är klar för befordran.

**API-format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |

**Begäran**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```http
200 OK
```

## Ingest Parquet-filer {#ingest-parquet-files}

>[!NOTE]
>
>Följande steg gäller för små filer (256 MB eller mindre). Om du får en timeout för gatewayen eller begär fel i brödtextstorleken måste du växla till stor filöverföring.

### Skapa batch

Först måste du skapa en batch med Parquet som indataformat. När du skapar gruppen måste du ange ett datauppsättnings-ID. Du måste också se till att alla filer som överförs som en del av gruppen följer XDM-schemat som är länkat till den angivna datauppsättningen.

**Begäran**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| Parameter | Beskrivning |
| --------- | ------------ |
| `{DATASET_ID}` | ID för referensdatauppsättningen. |

**Svar**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |
| `{USER_ID}` | ID för den användare som skapade gruppen. |

### Överför filer

Nu när du har skapat en grupp kan du använda `batchId` från innan för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. Se till att du använder ett unikt filnamn så att det inte hamnar i konflikt med en annan fil för gruppen med filer som skickas. |

**Begäran**

>[!CAUTION]
>
>Detta API har stöd för överföring till en del. Kontrollera att innehållstypen är application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. Den här filsökvägen är den lokala filsökvägen, till exempel `acme/customers/campaigns/summer.parquet`. |

**Svar**

```http
200 OK
```

### Slutför batch

När du har överfört alla olika delar av filen måste du signalera att alla data har överförts och att gruppen är klar för befordran.

**API-format**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för batchen som du vill signalera är klart för slutförande. |

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
200 OK
```

## Infoga stora Parquet-filer

>[!NOTE]
>
>I det här avsnittet beskrivs hur du överför filer som är större än 256 MB. De stora filerna överförs i segment och sammanfogas sedan med en API-signal.

### Skapa batch

Först måste du skapa en batch med Parquet som indataformat. När du skapar gruppen måste du ange ett datauppsättnings-ID. Du måste också se till att alla filer som överförs som en del av gruppen följer XDM-schemat som är länkat till den angivna datauppsättningen.

**API-format**

```http
POST /batches
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | ID för referensdatauppsättningen. |

**Svar**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |
| `{USER_ID}` | ID för den användare som skapade gruppen. |

### Initiera stor fil

När du har skapat gruppen måste du initiera den stora filen innan du överför segment till gruppen.

**API-format**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |
| `{FILE_NAME}` | Namnet på filen som ska initieras. |

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
201 Created
```

### Överför stora filsegment

Nu när filen har skapats kan alla efterföljande segment överföras genom upprepade förfrågningar från PATCH, en för varje del av filen.

**API-format**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. Se till att du använder ett unikt filnamn så att det inte hamnar i konflikt med en annan fil för gruppen med filer som skickas. |

**Begäran**

>[!CAUTION]
>
>Detta API har stöd för överföring till en del. Kontrollera att innehållstypen är application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONTENT_RANGE}` | I heltal börjar och slutar det begärda intervallet. |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. Den här filsökvägen är den lokala filsökvägen, till exempel `acme/customers/campaigns/summer.json`. |


**Svar**

```http
200 OK
```

### Fullständig stor fil

Nu när du har skapat en grupp kan du använda `batchId` från innan för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

**API-format**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för batchen som du vill signalera slutförande av. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på den fil som du vill signalera slutförande av. |

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
201 Created
```

### Slutför batch

När du har överfört alla olika delar av filen måste du signalera att alla data har överförts och att gruppen är klar för befordran.

**API-format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för batchen som du vill signalera är komplett. |


**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
200 OK
```

## Importera CSV-filer

För att kunna importera CSV-filer måste du skapa en klass, ett schema och en datauppsättning som stöder CSV. Detaljerad information om hur du skapar den klass och det schema som krävs finns i [självstudiekurs om att skapa ad hoc-schema](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>Följande steg gäller för små filer (256 MB eller mindre). Om du får en timeout för gatewayen eller begär fel i brödtextstorleken måste du växla till stor filöverföring.

### Skapa datauppsättning

När du har följt instruktionerna ovan för att skapa den klass och det schema som behövs måste du skapa en datauppsättning som kan hantera CSV.

**API-format**

```http
POST /catalog/dataSets
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TENANT_ID}` | Detta ID används för att säkerställa att de resurser du skapar namnges korrekt och finns i IMS-organisationen. |
| `{SCHEMA_ID}` | ID:t för schemat som du har skapat. |

### Skapa batch

Därefter måste du skapa en grupp med CSV som indataformat. När du skapar gruppen måste du ange ett datauppsättnings-ID. Du måste också se till att alla filer som överförs som en del av gruppen följer det schema som är länkat till den angivna datauppsättningen.

**API-format**

```http
POST /batches
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | ID för referensdatauppsättningen. |

**Svar**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |
| `{USER_ID}` | ID för den användare som skapade gruppen. |

### Överför filer

Nu när du har skapat en grupp kan du använda `batchId` från innan för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

>[!NOTE]
>
>I avsnittet Bilaga finns en [exempel på en korrekt formaterad CSV-datafil](#data-transformation-for-batch-ingestion).

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. Se till att du använder ett unikt filnamn så att det inte hamnar i konflikt med en annan fil för gruppen med filer som skickas. |

**Begäran**

>[!CAUTION]
>
>Detta API har stöd för överföring till en del. Kontrollera att innehållstypen är application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. Den här filsökvägen är den lokala filsökvägen, till exempel `acme/customers/campaigns/summer.csv`. |


**Svar**

```http
200 OK
```

### Slutför batch

När du har överfört alla olika delar av filen måste du signalera att alla data har överförts och att gruppen är klar för befordran.

**API-format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```http
200 OK
```

## Avbryt en batch

Batchen bearbetas, men den kan fortfarande avbrytas. Men när en batch har slutförts (till exempel om den har slutförts eller misslyckats) kan den inte avbrytas.

**API-format**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för den batch som du vill avbryta. |

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
200 OK
```

## Ta bort en grupp {#delete-a-batch}

En batch kan tas bort genom att utföra följande POST-begäran med `action=REVERT` frågeparameter till ID:t för den batch som du vill ta bort. Satsen är markerad som&quot;inaktiv&quot;, vilket gör att den kan användas för skräpinsamling. Batchen samlas in asynkront, och då markeras den som&quot;borttagen&quot;.

**API-format**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill ta bort. |

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
200 OK
```

## Laga en batch

Ibland kan det vara nödvändigt att uppdatera data i din organisations Profile Store. Du kan till exempel behöva korrigera poster eller ändra ett attributvärde. Adobe Experience Platform stöder uppdatering eller korrigering av data i Profile Store genom en upsert-åtgärd eller&quot;patching a batch&quot;.

>[!NOTE]
>
>Dessa uppdateringar tillåts bara för profilposter, inte för att uppleva händelser.

Följande krävs för att korrigera en sats:

- **En datauppsättning aktiverad för profiluppdateringar och attributuppdateringar.** Detta görs via datauppsättningstaggar och kräver en specifik `isUpsert:true` -taggen läggs till i `unifiedProfile` array. Följ självstudiekursen för mer information om hur du skapar en datauppsättning eller konfigurerar en befintlig datauppsättning för upsert [aktivera en datauppsättning för profiluppdateringar](../../catalog/datasets/enable-upsert.md).
- **En Parquet-fil som innehåller de fält som ska korrigeras och identitetsfält för profilen.** Dataformatet för att patchera en batch liknar den vanliga batchöverföringsprocessen. De indata som krävs är en Parquet-fil, och utöver de fält som ska uppdateras måste de överförda data innehålla identitetsfälten för att matcha data i profilarkivet.

När du har en datauppsättning aktiverad för Profil och upsert, och en Parquet-fil som innehåller de fält du vill korrigera samt de nödvändiga identitetsfälten, kan du följa stegen för [inhämtning av Parquet-filer](#ingest-parquet-files) för att färdigställa plåstret via batchintag.

## Spela upp en batch

Om du vill ersätta en redan skickad batch kan du göra det med&quot;batchrepriser&quot; - den här åtgärden motsvarar att ta bort den gamla gruppen och i stället hämta en ny.

### Skapa batch

För det första måste du skapa en batch med JSON som indataformat. När du skapar gruppen måste du ange ett datauppsättnings-ID. Du måste också se till att alla filer som överförs som en del av gruppen följer XDM-schemat som är länkat till den angivna datauppsättningen. Dessutom måste du ange de gamla batcherna som referens i avsnittet Spela upp. I exemplet nedan spelar du upp grupper med ID:n `batchIdA` och `batchIdB`.

**API-format**

```http
POST /batches
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| Parameter | Beskrivning |
| --------- | ----------- | 
| `{DATASET_ID}` | ID för referensdatauppsättningen. |

**Svar**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |
| `{USER_ID}` | ID för den användare som skapade gruppen. |


### Överför filer

Nu när du har skapat en grupp kan du använda `batchId` från innan för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. Se till att du använder ett unikt filnamn så att det inte hamnar i konflikt med en annan fil för gruppen med filer som skickas. |

**Begäran**

>[!CAUTION]
>
>Detta API har stöd för överföring till en del. Kontrollera att innehållstypen är application/octet-stream. Använd inte alternativet curl -F eftersom det som standard är en begäran om flera delar som inte är kompatibel med API:t.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. Den här filsökvägen är den lokala filsökvägen, till exempel `acme/customers/campaigns/summer.json`. |

**Svar**

```http
200 OK
```

### Slutför batch

När du har överfört alla olika delar av filen måste du signalera att alla data har överförts och att gruppen är klar för befordran.

**API-format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för den batch som du vill slutföra. |

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```http
200 OK
```

## Bilaga

Följande avsnitt innehåller ytterligare information om hur man får in data i Experience Platform med hjälp av batchintag.

### Datatransformering för batchinmatning

För att kunna importera en datafil till [!DNL Experience Platform]måste filens hierarkiska struktur överensstämma med [Experience Data Model (XDM)](../../xdm/home.md) schema som är associerat med den datauppsättning som överförs till.

Information om hur du mappar en CSV-fil så att den överensstämmer med ett XDM-schema finns i [exempelomformningar](../../etl/transformations.md) -dokument tillsammans med ett exempel på en korrekt formaterad JSON-datafil. Exempelfiler som finns i dokumentet finns här:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
