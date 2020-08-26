---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över partiell gruppinmatning i Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---



# Partiellt batchintag

Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som alla felaktiga data grupperas separat, tillsammans med information om varför de är ogiltiga.

Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.

I [bilagan](#appendix) till den här självstudien finns dessutom en referens för feltyper av partiell gruppinmatning.

## Komma igång

Den här självstudiekursen kräver en fungerande kunskap om de olika Adobe Experience Platform-tjänster som är involverade i partiell batchförbrukning. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Batchförtäring](./overview.md): Den metod som används för att [!DNL Platform] importera och lagra data från datafiler, till exempel CSV och Parquet.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API: [!DNL Platform] er.

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

## Aktivera en batch för partiell batchimport i API {#enable-api}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchimport med API:t. Instruktioner om hur du använder användargränssnittet finns i [Aktivera en batch för partiell gruppförbrukning i](#enable-ui) användargränssnittssteget.

Du kan skapa en ny grupp med partiellt intag aktiverat.

Om du vill skapa en ny batch följer du stegen i [Utvecklarhandbok](./api-overview.md)för batchimport. När du har nått **[!UICONTROL Create batch]** steget lägger du till följande fält i begärandetexten:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `enableErrorDiagnostics` | En flagga som gör [!DNL Platform] att du kan generera detaljerade felmeddelanden om din batch. |
| `partialIngestionPercentage` | Procentandelen godtagbara fel innan hela gruppen misslyckas. I det här exemplet kan alltså maximalt 5 % av batchen vara fel, innan den misslyckas. |


## Aktivera en batch för partiell batchförbrukning i användargränssnittet {#enable-ui}

>[!NOTE]
>
>I det här avsnittet beskrivs hur du aktiverar en batch för partiell batchförbrukning med användargränssnittet. Om du redan har aktiverat en batch för partiell gruppinmatning med API:t kan du hoppa fram till nästa avsnitt.

Om du vill aktivera en batch för partiell förtäring via [!DNL Platform] användargränssnittet kan du skapa en ny batch via källanslutningar, skapa en ny batch i en befintlig datauppsättning eller skapa en ny batch via&quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Skapa en ny källanslutning {#new-source}

Om du vill skapa en ny källanslutning följer du stegen i listan i [Källöversikt](../../sources/home.md). När du har kommit till **[!UICONTROL Dataflow detail]** steget bör du tänka på **[!UICONTROL Partial ingestion]** - och **[!UICONTROL Error diagnostics]** fälten.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Med **[!UICONTROL Partial ingestion]** växlingsknappen kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växlingsknappen **[!UICONTROL Error diagnostics]** visas bara när **[!UICONTROL Partial ingestion]** växlingsknappen är inaktiverad. Med den här funktionen kan du [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om *[!UICONTROL Partial ingestion]* växeln är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** den kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

### Använd en befintlig datauppsättning {#existing-dataset}

Om du vill använda en befintlig datauppsättning börjar du med att välja en datauppsättning. Sidlisten till höger innehåller information om datauppsättningen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Med **[!UICONTROL Partial ingestion]** växlingsknappen kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växlingsknappen **[!UICONTROL Error diagnostics]** visas bara när **[!UICONTROL Partial ingestion]** växlingsknappen är inaktiverad. Med den här funktionen kan du [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om **[!UICONTROL Partial ingestion]** växeln är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** den kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

Nu kan du överföra data med knappen **Lägg till data** , och den kommer att importeras delvis.

### Använd flödet &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Om du vill använda &quot;[!UICONTROL Map CSV to XDM schema]&quot;-flödet följer du stegen i [Mappa en CSV-fil i självstudiekursen](../tutorials/map-a-csv-file.md). När du har kommit till **[!UICONTROL Add data]** steget bör du tänka på **[!UICONTROL Partial ingestion]** - och **[!UICONTROL Error diagnostics]** fälten.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Med **[!UICONTROL Partial ingestion]** växlingsknappen kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växlingsknappen **[!UICONTROL Error diagnostics]** visas bara när **[!UICONTROL Partial ingestion]** växlingsknappen är inaktiverad. Med den här funktionen kan du [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om **[!UICONTROL Partial ingestion]** växeln är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Med **[!UICONTROL Error threshold]** den kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

## Hämtar metadata på filnivå {#download-metadata}

Med Adobe Experience Platform kan användarna hämta indatafilernas metadata. Metadata bevaras inom [!DNL Platform] upp till 30 dagar.

### Visa indatafiler {#list-files}

Med följande begäran kan du visa en lista över alla filer som ingår i en slutförd grupp.

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med JSON-objekt som innehåller sökvägsobjekt som anger var metadata sparades.

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Hämta metadata för indatafil {#retrieve-metadata}

När du har hämtat en lista över alla olika indatafiler kan du hämta metadata för den enskilda filen med följande slutpunkt.

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med JSON-objekt som innehåller sökvägsobjekt som anger var metadata sparades.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Hämta fel för partiell gruppinmatning {#retrieve-errors}

Om batchar innehåller fel måste du hämta felinformation om dessa fel så att du kan importera data igen.

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
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svara utan fel**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om batchstatusen.

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
| `metrics.failedRecordCount` | Antalet rader som inte kunde bearbetas på grund av parsning, konvertering eller validering. Det här värdet kan härledas genom att subtrahera `inputRecordCount` från `outputRecordCount`. Det här värdet genereras för alla batchar, oavsett om `errorDiagnostics` är aktiverat. |

**Svara med fel**

Om batchen har ett eller flera fel och feldiagnostik är aktiverat får du mer information `success` om felen både i svaret och i en hämtningsbar felfil.

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
| `metrics.failedRecordCount` | Antalet rader som inte kunde bearbetas på grund av parsning, konvertering eller validering. Det här värdet kan härledas genom att subtrahera `inputRecordCount` från `outputRecordCount`. Det här värdet genereras för alla batchar, oavsett om `errorDiagnostics` är aktiverat. |
| `errors.recordCount` | Antalet rader som misslyckades för den angivna felkoden. Det här värdet genereras **bara** om `errorDiagnostics` är aktiverat. |

>[!NOTE]
>
>Om ingen feldiagnostik är tillgänglig visas följande felmeddelande i stället:
> 
```json
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## Nästa steg {#next-steps}

I den här självstudiekursen beskrivs hur du skapar eller ändrar en datauppsättning för att aktivera partiell gruppinmatning. Mer information om batchintag finns i Utvecklarhandbok för [batchintag](./api-overview.md).

## Feltyper för partiell batchöverföring {#appendix}

Partiell batchinmatning har tre olika feltyper vid inmatning av data.

- [Oläsbara filer](#unreadable)
- [Ogiltiga scheman eller rubriker](#schemas-headers)
- [Otolkningsbara rader](#unparsable)

### Oläsbara filer {#unreadable}

Om det finns oläsbara filer i den inlästa gruppen bifogas batchfelen på själva gruppen. Mer information om hur du hämtar den misslyckade batchen finns i guiden [](../quality/retrieve-failed-batches.md)Hämta misslyckade batchar.

### Ogiltiga scheman eller rubriker {#schemas-headers}

Om den inmatade gruppen har ett ogiltigt schema eller ogiltiga rubriker, bifogas batchfelen på själva gruppen. Mer information om hur du hämtar den misslyckade batchen finns i guiden [](../quality/retrieve-failed-batches.md)Hämta misslyckade batchar.

### Otolkningsbara rader {#unparsable}

Om den grupp som du har infogat har rader som inte kan tolkas kan du använda följande slutpunkt för att visa en lista med filer som innehåller fel.

**API-format**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | Värdet `id` för gruppen som du hämtar felinformation från. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över de filer som innehåller fel.

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

Sedan kan du hämta detaljerad information om felen med hjälp av [metadatahämtningsslutpunkten](#retrieve-metadata).

Ett exempelsvar på hämtning av felfilen visas nedan:

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
