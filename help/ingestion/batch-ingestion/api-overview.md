---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för Adobe Experience Platform Batch Ingakes
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 3%

---


# Utvecklarhandbok för batchintag

I det här dokumentet finns en omfattande översikt över hur du använder API:er för [gruppinmatning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

I bilagan till det här dokumentet finns information om [formatering av data som ska användas för konsumtion](#data-transformation-for-batch-ingestion), inklusive exempel på CSV- och JSON-datafiler.

## Komma igång

Inläsning av data ger en RESTful API genom vilken du kan utföra grundläggande CRUD-åtgärder mot de objekttyper som stöds.

I följande avsnitt finns ytterligare information som du behöver känna till eller ha till hands för att kunna anropa API:t för gruppinmatning.

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Batchförtäring](./overview.md): Gör att du kan importera data till Adobe Experience Platform som gruppfiler.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Begäranden som innehåller en nyttolast (POST, PUT, PATCH) kan kräva ytterligare ett `Content-Type` huvud. Godkända värden som är specifika för varje anrop anges i anropsparametrarna. Följande innehållstyper används i den här handboken:

- Innehållstyp: application/json
- Innehållstyp: application/octet-stream

## Typer

När du importerar data är det viktigt att förstå hur [!DNL Experience Data Model] (XDM)-scheman fungerar. Mer information om hur XDM-fälttyper mappas till olika format finns i utvecklarhandboken för [schemaregister](../../xdm/api/getting-started.md).

Det finns viss flexibilitet vid inmatning av data - om en typ inte matchar vad som finns i målschemat konverteras data till den angivna måltypen. Om den inte kan det misslyckas batchen med ett `TypeCompatibilityException`.

Varken JSON eller CSV har till exempel typen datum eller tid. Därför uttrycks dessa värden med [ISO 8061-formaterade strängar](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) eller Unix Time i millisekunder (153126395) 9000) och konverteras vid intag till mål-XDM-typen.

Tabellen nedan visar de konverteringar som stöds vid inmatning av data.

| Inkommande (rad) mot Target (kolumn) | Sträng | Byte | Kort | Heltal | Lång | Dubbel | Datum | Datum-tid | Objekt | Mappa |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Sträng | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Kort | X | X | X | X | X | X |  |  |  |  |
| Heltal | X | X | X | X | X | X |  |  |  |  |
| Lång | X | X | X | X | X | X | X | X |  |  |
| Dubbel | X | X | X | X | X | X |  |  |  |  |
| Datum |  |  |  |  |  |  | X |  |  |  |
| Datum-tid |  |  |  |  |  |  |  | X |  |  |
| Objekt |  |  |  |  |  |  |  |  | X | X |
| Mappa |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Booleaner och arrayer kan inte konverteras till andra typer.

## Begränsningar för intag

Batchdatainmatning har vissa begränsningar:
- Maximalt antal filer per grupp: 1500
- Maximal batchstorlek: 100 GB
- Maximalt antal egenskaper eller fält per rad: 10000
- Maximalt antal batchar per minut, per användare: 138

## Importera JSON-filer

>[!NOTE]
>
>Följande steg gäller för små filer (256 MB eller mindre). Om du råkar ut för en timeout för gatewayen eller begär fel i brödstorlek måste du växla till stor filöverföring.

### Skapa batch

För det första måste du skapa en batch med JSON som indataformat. När du skapar gruppen måste du ange ett datauppsättnings-ID. Du måste också se till att alla filer som överförs som en del av gruppen följer XDM-schemat som är länkat till den angivna datauppsättningen.

>[!NOTE]
>
>Exemplen nedan är för enradig JSON. Om du vill importera flerradig JSON måste du ange `isMultiLineJson` flaggan. Mer information finns i felsökningsguiden för [batchimport](./troubleshooting.md).

**API-format**

```http
POST /batches
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |

### Överför filer

Nu när du har skapat en grupp kan du använda kommandot `batchId` från tidigare för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

>[!NOTE]
>
>Ett [exempel på en korrekt formaterad JSON-datafil](#data-transformation-for-batch-ingestion)finns i bilagan.

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. |

**Begäran**

>[!NOTE]
>
>API:t stöder överföring till en del. Kontrollera att innehållstypen är application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```http
200 OK
```

## Ingest Parquet-filer

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
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
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

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |
| `{USER_ID}` | ID för den användare som skapade gruppen. |

### Överför filer

Nu när du har skapat en grupp kan du använda kommandot `batchId` från tidigare för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. |

**Begäran**

>[!CAUTION]
>
>Detta API har stöd för överföring till en del. Kontrollera att innehållstypen är application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{FILE_NAME}` | Namnet på filen som du vill överföra. |

**Begäran**

>[!CAUTION]
>
>Detta API har stöd för överföring till en del. Kontrollera att innehållstypen är application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONTENT_RANGE}` | I heltal börjar och slutar det begärda intervallet. |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. |


**Svar**

```http
200 OK
```

### Fullständig stor fil

Nu när du har skapat en grupp kan du använda kommandot `batchId` från tidigare för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
200 OK
```

## Importera CSV-filer

För att kunna importera CSV-filer måste du skapa en klass, ett schema och en datauppsättning som stöder CSV. Detaljerad information om hur du skapar nödvändiga klasser och scheman finns i instruktionerna i självstudiekursen [för att skapa](../../xdm/api/ad-hoc.md)ad hoc-scheman.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TENANT_ID}` | Detta ID används för att säkerställa att de resurser du skapar namnges korrekt och finns i IMS-organisationen. |
| `{SCHEMA_ID}` | ID:t för schemat som du har skapat. |

En förklaring till vad olika delar av avsnittet &quot;fileDescription&quot; i JSON-brödtexten kan ses nedan:

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `format` | Den överordnade filens format, inte indatafilens format. |
| `delimiters` | Det tecken som ska användas som avgränsare. |
| `quotes` | Det tecken som ska användas för citattecken. |
| `escapes` | Det tecken som ska användas som escape-tecken. |
| `header` | Den överförda filen **måste** innehålla rubriker. Eftersom schemavalideringen är klar måste detta anges till true. Dessutom får rubriker **inte** innehålla blanksteg. Om du har blanksteg i huvudet kan du ersätta dem med understreck istället. |
| `charset` | Ett valfritt fält. Andra teckenuppsättningar som stöds är&quot;US-ASCII&quot; och&quot;ISO-8869-1&quot;. Om den lämnas tom används UTF-8 som standard. |

Den datauppsättning som refereras måste ha filbeskrivningsblocket som listas ovan och måste peka på ett giltigt schema i registret. Annars kan filen inte mastras i en parquet.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID för den nyligen skapade gruppen. |
| `{DATASET_ID}` | ID för den refererade datauppsättningen. |
| `{USER_ID}` | ID för den användare som skapade gruppen. |

### Överför filer

Nu när du har skapat en grupp kan du använda kommandot `batchId` från tidigare för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

>[!NOTE]
>
>Ett [exempel på en korrekt formaterad CSV-datafil](#data-transformation-for-batch-ingestion)finns i bilagan.

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. |

**Begäran**

>[!CAUTION]
>
>Detta API har stöd för överföring till en del. Kontrollera att innehållstypen är application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. |


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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
200 OK
```

## Ta bort en grupp {#delete-a-batch}

En batch kan tas bort genom att utföra följande begäran med frågeparametern till ID:t för den POST som du vill ta bort. `action=REVERT` Satsen är markerad som&quot;inaktiv&quot;, vilket gör att den kan användas för skräpinsamling. Batchen samlas in asynkront, och då markeras den som&quot;borttagen&quot;.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

```http
200 OK
```

## Spela upp en batch

Om du vill ersätta en redan skickad batch kan du göra det med&quot;batchrepriser&quot; - den här åtgärden motsvarar att ta bort den gamla gruppen och i stället hämta en ny.

### Skapa batch

För det första måste du skapa en batch med JSON som indataformat. När du skapar gruppen måste du ange ett datauppsättnings-ID. Du måste också se till att alla filer som överförs som en del av gruppen följer XDM-schemat som är länkat till den angivna datauppsättningen. Dessutom måste du ange de gamla batcherna som referens i avsnittet Spela upp. I exemplet nedan spelar du upp grupper med ID `batchIdA` och `batchIdB`.

**API-format**

```http
POST /batches
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

Nu när du har skapat en grupp kan du använda kommandot `batchId` från tidigare för att överföra filer till gruppen. Du kan överföra flera filer till gruppen.

**API-format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du vill överföra till. |
| `{DATASET_ID}` | ID för batchens referensdatauppsättning. |
| `{FILE_NAME}` | Namnet på filen som du vill överföra. |

**Begäran**

>[!CAUTION]
>
>Detta API har stöd för överföring till en del. Kontrollera att innehållstypen är application/octet-stream. Använd inte alternativet curl -F eftersom det som standard är en begäran om flera delar som inte är kompatibel med API:t.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Den fullständiga sökvägen och namnet för filen som du försöker överföra. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```http
200 OK
```

## Bilaga

### Datatransformering för batchinmatning

För att kunna importera en datafil till [!DNL Experience Platform]måste filens hierarkiska struktur följa det XDM-schema ( [Experience Data Model)](../../xdm/home.md) som är associerat med den datauppsättning som överförs till.

Information om hur du mappar en CSV-fil så att den överensstämmer med ett XDM-schema finns i [exempeldokumentet för omformningar](../../etl/transformations.md) , tillsammans med ett exempel på en korrekt formaterad JSON-datafil. Exempelfiler som finns i dokumentet finns här:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)