---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;error diagnostics;retrieve error diagnostics;get error diagnostics;get error;get errors;retrieve errors;
solution: Experience Platform
title: Översikt över partiell gruppinmatning i Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 4652722b17a290c9ef53244498257eb4cb97ac6d
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 1%

---


# Hämtar feldiagnostik

Adobe Experience Platform har två metoder för att överföra och importera data. Du kan antingen använda gruppinmatning, vilket gör att du kan infoga data med olika filtyper (t.ex. CSV-filer), eller direktuppspelningsuppläsning, vilket gör att du kan infoga data i [!DNL Platform] direktuppspelningsslutpunkter i realtid.

Det här dokumentet innehåller information om övervakning av batchförbrukning, hantering av partiella batchöverföringsfel samt en referens för partiella batchinsatstyper.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
- [[!DNL Adobe Experience Platform - datainmatning]](../home.md): Metoderna som data kan skickas till [!DNL Experience Platform].

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Schema Registry], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

## Hämtar feldiagnostik {#download-diagnostics}

Med Adobe Experience Platform kan användare hämta feldiagnostiken för indatafilerna. Diagnostiken behålls inom [!DNL Platform] upp till 30 dagar.

### Visa indatafiler {#list-files}

Följande begäran hämtar en lista över alla filer som finns i en slutförd batch.

**API-format**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du letar upp. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar JSON-objekt som anger var diagnostikerna sparades.

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Hämta diagnostik för indatafiler {#retrieve-diagnostics}

När du har hämtat en lista över alla olika indatafiler kan du hämta diagnostiken för den enskilda filen med följande begäran.

**API-format**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du letar upp. |
| `{FILE}` | Namnet på filen som du försöker komma åt. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar JSON-objekt som innehåller `path` objekt som anger var diagnostikerna sparades. Svaret returnerar `path` objekten i [JSON-radformat](https://jsonlines.org/) .

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Hämta batchbearbetningsfel {#retrieve-errors}

Om batchar innehåller fel bör du hämta felinformation om dessa fel så att du kan importera data igen.

### Kontrollera status {#check-status}

Om du vill kontrollera status för den inkapslade batchen måste du ange batchens ID i sökvägen till en GET-förfrågan.

**API-format**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | Värdet `id` för den batch som du vill kontrollera status för. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svara utan fel**

Ett lyckat svar returneras med detaljerad information om batchens status.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `metrics.failedRecordCount` | Antalet rader som inte kunde bearbetas på grund av parsning, konvertering eller validering. Det här värdet kan härledas genom att subtrahera `inputRecordCount` från `outputRecordCount`. Det här värdet genereras för alla batchar, oavsett om det `errorDiagnostics` är aktiverat. |

**Svara med fel**

Om batchen har ett eller flera fel och feldiagnostik är aktiverat, returnerar svaret mer information om felen, både inom själva nyttolasten och en hämtningsbar felfil. Observera att status för en batch som innehåller fel fortfarande kan ha status Slutfört.

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `metrics.failedRecordCount` | Antalet rader som inte kunde bearbetas på grund av parsning, konvertering eller validering. Det här värdet kan härledas genom att subtrahera `inputRecordCount` från `outputRecordCount`. Det här värdet genereras för alla batchar, oavsett om det `errorDiagnostics` är aktiverat. |
| `errors.recordCount` | Antalet rader som misslyckades för den angivna felkoden. Det här värdet genereras **bara** om `errorDiagnostics` är aktiverat. |

>[!NOTE]
>
>Om ingen feldiagnostik är tillgänglig visas följande felmeddelande i stället:
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Nästa steg {#next-steps}

I den här självstudiekursen beskrivs hur du övervakar fel vid partiell gruppinmatning. Mer information om batchintag finns i Utvecklarhandbok för [batchintag](../batch-ingestion/api-overview.md).

## Bilaga {#appendix}

I det här avsnittet finns ytterligare information om olika typer av matningsfel.

### Feltyper för partiell batchöverföring {#partial-ingestion-types}

Partiell gruppinmatning har tre olika feltyper vid datainmatning:

- [Oläsbara filer](#unreadable)
- [Ogiltiga scheman eller rubriker](#schemas-headers)
- [Otolkningsbara rader](#unparsable)

### Oläsbara filer {#unreadable}

Om det finns oläsbara filer i den inlästa gruppen bifogas batchfelen på själva gruppen. Mer information om hur du hämtar den misslyckade batchen finns i guiden [](../quality/retrieve-failed-batches.md)Hämta misslyckade batchar.

### Ogiltiga scheman eller rubriker {#schemas-headers}

Om den inmatade gruppen har ett ogiltigt schema eller ogiltiga rubriker, bifogas batchfelen på själva gruppen. Mer information om hur du hämtar den misslyckade batchen finns i guiden [](../quality/retrieve-failed-batches.md)Hämta misslyckade batchar.

### Otolkningsbara rader {#unparsable}

Om den grupp som du har infogat har rader som inte kan tolkas kan du använda följande begäran för att visa en lista med filer som innehåller fel.

**API-format**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | Värdet `id` för gruppen som du hämtar felinformation från. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista över de filer som innehåller fel.

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Du kan sedan hämta detaljerad information om felen med hjälp av [diagnostikåterställningens slutpunkt](#retrieve-diagnostics).

Ett exempelsvar på hämtning av felfilen visas nedan:

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
