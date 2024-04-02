---
keywords: Experience Platform;hem;populära ämnen;dataöverföring;batch;batchvis;aktivera datauppsättning;batchöverföring översikt;översikt;batchöverföring översikt;
solution: Experience Platform
title: Översikt över API för gruppinmatning
description: Med API:t för Adobe Experience Platform Batch Ingclosure kan du importera data till Platform som gruppfiler. Data som importeras kan vara profildata från en platt fil i ett CRM-system (till exempel en Parquet-fil) eller data som följer ett känt schema i XDM-registret (Experience Data Model).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 9d3a8aac120119ce0361685f9cb8d3bfc28dc7fd
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 4%

---

# API-översikt för gruppinmatning

Med API:t för Adobe Experience Platform Batch Ingclosure kan du importera data till Platform som gruppfiler. Data som importeras kan vara profildata från en platt fil (t.ex. en Parquet-fil) eller data som följer ett känt schema i [!DNL Experience Data Model] (XDM)-registret.

The [API-referens för gruppinmatning](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) innehåller ytterligare information om dessa API-anrop.

I följande diagram visas batchintagsprocessen:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Komma igång

API-slutpunkterna som används i den här handboken är en del av [API för gruppinmatning](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Innan du fortsätter bör du granska [komma igång-guide](getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

### [!DNL Data Ingestion] krav

- Data som ska överföras måste vara antingen i Parquet- eller JSON-format.
- En datauppsättning som skapats i [[!DNL Catalog services]](../../catalog/home.md).
- Innehållet i Parquet-filen måste matcha en delmängd av schemat i datauppsättningen som överförs till.
- Ha din unika åtkomsttoken efter autentisering.

### Bästa praxis för gruppkonsumtion

- Den rekommenderade batchstorleken är mellan 256 MB och 100 GB.
- Varje grupp bör innehålla högst 1 500 filer.

### Begränsningar för batchförbrukning

Batchdatainmatning har vissa begränsningar:

- Maximalt antal filer per batch: 1 500
- Maximal batchstorlek: 100 GB
- Maximalt antal egenskaper eller fält per rad: 10000
- Maximalt antal batchar i sjödata per minut, per användare: 138

>[!NOTE]
>
>Om du vill överföra en fil som är större än 512 MB måste filen delas upp i mindre segment. Instruktioner för att överföra en stor fil finns i [stort filöverföringsavsnitt i det här dokumentet](#large-file-upload---create-file).

### Typer

När data hämtas är det viktigt att förstå hur [!DNL Experience Data Model] (XDM) scheman fungerar. Mer information om hur XDM-fälttyper mappas till olika format finns i [Utvecklarhandbok för schemaregister](../../xdm/api/getting-started.md).

Det finns viss flexibilitet vid inmatning av data - om en typ inte matchar vad som finns i målschemat konverteras data till den angivna måltypen. Om så inte är fallet misslyckas batchen med `TypeCompatibilityException`.

Till exempel har varken JSON eller CSV en `date` eller `date-time` typ. Därför uttrycks dessa värden med [Formaterade strängar enligt ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) eller Unix-tid i millisekunder (1531263959000) och konverteras vid importen till mål-XDM-typen.

Tabellen nedan visar de konverteringar som stöds vid inmatning av data.

| Inkommande (rad) kontra mål (kol) | Sträng | Byte | Kort | Heltal | Lång | Dubbel | Datum | Datum-tid | Objekt | Karta |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Sträng | X | X | X | X | X | X | X | X |   |   |
| Byte | X | X | X | X | X | X |   |   |   |   |
| Kort | X | X | X | X | X | X |   |   |   |   |
| Heltal | X | X | X | X | X | X |   |   |   |   |
| Lång | X | X | X | X | X | X | X | X |   |   |
| Dubbel | X | X | X | X | X | X |   |   |   |   |
| Datum |   |   |   |   |   |   | X |   |   |   |
| Datum-tid |   |   |   |   |   |   |   | X |   |   |
| Objekt |   |   |   |   |   |   |   |   | X | X |
| Karta |   |   |   |   |   |   |   |   | X | X |

>[!NOTE]
>
>Booleaner och arrayer kan inte konverteras till andra typer.

## Använda API:et

The [!DNL Data Ingestion] Med API kan du importera data som grupper (en dataenhet som består av en eller flera filer som ska importeras som en enda enhet) till [!DNL Experience Platform] tre grundläggande steg:

1. Skapa en ny batch.
2. Överför filer till en angiven datauppsättning som matchar datans XDM-schema.
3. Signalera slutet av gruppen.

## Skapa en batch

Innan data kan läggas till i en datauppsättning måste de länkas till en batch, som senare överförs till en angiven datauppsättning.

```http
POST /batches
```

**Begäran**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
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

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | ID för den batch som precis skapades (används i efterföljande begäranden). |
| `relatedObjects.id` | ID:t för datauppsättningen som filerna ska överföras till. |

## Filöverföring

När du har skapat en ny batch för överföring kan filer sedan överföras till en viss datauppsättning.

Du kan överföra filer med hjälp av API:t för liten filöverföring. Om filerna är för stora och gatewaygränsen överskrids (t.ex. utökade tidsgränser, begäranden om kroppsstorlek har överskridits och andra begränsningar) kan du växla till API:t för stor filöverföring. Denna API överför filen i segment och sammanfogar data med API-anropet Large File Upload Complete.

>[!NOTE]
>
>Batchmatning kan användas för att stegvis uppdatera data i profilarkivet. Mer information finns i avsnittet om [uppdatera en batch](#patch-a-batch) i [Utvecklarhandbok för batchintag](api-overview.md).

>[!INFO]
>
>Exemplen nedan använder [Apache Parquet](https://parquet.apache.org/docs/) filformat. Ett exempel som använder JSON-filformatet finns i [Utvecklarhandbok för batchintag](api-overview.md).

### Liten filöverföring

När en batch har skapats kan data överföras till en befintlig datauppsättning.  Filen som överförs måste matcha det refererade XDM-schemat.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | Batchens ID. |
| `{DATASET_ID}` | ID:t för datauppsättningen som ska överföras. |
| `{FILE_NAME}` | Namnet på filen så som den visas i datauppsättningen. |

**Begäran**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
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
| `{FILE_NAME}` | Namnet på filen så som den visas i datauppsättningen. |

**Begäran**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Svar**

```JSON
#Status 201 CREATED, with empty response body
```

### Stor filöverföring - överför efterföljande delar

När filen har skapats kan alla efterföljande segment överföras genom upprepade PATCH-begäranden, en för varje del av filen.

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
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

När alla filer har överförts till gruppen kan gruppen signaleras för slutförande. Genom att göra det här [!DNL Catalog] DataSetFile-poster skapas för de slutförda filerna och kopplas till den grupp som genereras ovan. The [!DNL Catalog] batchen markeras sedan som lyckad, vilket aktiverar efterföljande flöden för att importera tillgängliga data.

**Begäran**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | ID för den batch som ska överföras till datauppsättningen. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Svar**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
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

The `"status"` fält är det som visar aktuell status för den begärda batchen. Batcherna kan ha något av följande lägen:

## Status för batchförtäring

| Status | Beskrivning |
| ------ | ----------- |
| Övergiven | Batchen har inte slutförts inom den förväntade tidsramen. |
| Avbruten | En avbrottsåtgärd har **explicit** har anropats (via API:t för gruppinmatning) för den angivna batchen. När batchen är i inläst läge kan den inte avbrytas. |
| Aktiv | Batchen har befordrats och är tillgänglig för nedladdning. Den här statusen kan användas omväxlande med &quot;Lyckades&quot;. |
| Borttagen | Data för batchen har tagits bort helt. |
| Misslyckades | Ett terminaltillstånd som antingen beror på felaktig konfiguration och/eller felaktiga data. Data för en misslyckad batch kommer att **not** visa upp. Den här statusen kan användas som ersättning med &quot;Misslyckades&quot;. |
| Inaktiv | Batchen befordrades men har återförts eller gått ut. Batchen är inte längre tillgänglig för nedströmsförbrukning. |
| Inläst | Data för batchen har slutförts och batchen är klar för befordran. |
| Läser in | Data för den här batchen överförs och batchen är för närvarande **not** redo att befordras. |
| Försöker igen | Data för den här batchen bearbetas. På grund av ett system- eller övergående fel misslyckades dock batchen. Detta innebär att batchen provas igen. |
| Mellanlagrad | Mellanlagringsfasen av befordringsprocessen för en batch är slutförd och åtkomsten har körts. |
| Mellanlagring | Data för batchen bearbetas. |
| Stängd | Data för batchen bearbetas. Batchkampanjen har dock avstannat efter ett antal försök. |
