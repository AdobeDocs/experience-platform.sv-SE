---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över partiell gruppinmatning i Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---



# Partiellt batchintag

Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som alla felaktiga data grupperas separat, tillsammans med information om varför de är ogiltiga.

Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.

I [bilagan](#appendix) till den här självstudien finns dessutom en referens för feltyper av partiell gruppinmatning.

## Komma igång

Den här självstudiekursen kräver en fungerande kunskap om de olika Adobe Experience Platform-tjänster som är involverade i partiell batchförbrukning. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Batchförtäring](./overview.md): Den metod som används för att [!DNL Platform] importera och lagra data från datafiler, till exempel CSV och Parquet.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.

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

Om du vill skapa en ny batch följer du stegen i [Utvecklarhandbok](./api-overview.md)för batchimport. När du har nått steget *Skapa grupp* lägger du till följande fält i begärandetexten:

```json
{
    ...
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
    ...
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

Om du vill skapa en ny källanslutning följer du stegen i listan i [Källöversikt](../../sources/home.md). När du har kommit till *[!UICONTROL Dataflow detail]* steget bör du tänka på *[!UICONTROL Partial ingestion]* - och *[!UICONTROL Error diagnostics]* fälten.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Med *[!UICONTROL Partial ingestion]* växlingsknappen kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växlingsknappen *[!UICONTROL Error diagnostics]* visas bara när *[!UICONTROL Partial ingestion]* växlingsknappen är inaktiverad. Med den här funktionen kan du [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om *[!UICONTROL Partial ingestion]* växeln är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Med *[!UICONTROL Error threshold]* den kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

### Använd en befintlig datauppsättning {#existing-dataset}

Om du vill använda en befintlig datauppsättning börjar du med att välja en datauppsättning. Sidlisten till höger innehåller information om datauppsättningen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Med *[!UICONTROL Partial ingestion]* växlingsknappen kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växlingsknappen *[!UICONTROL Error diagnostics]* visas bara när *[!UICONTROL Partial ingestion]* växlingsknappen är inaktiverad. Med den här funktionen kan du [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om *[!UICONTROL Partial ingestion]* växeln är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Med *[!UICONTROL Error threshold]* den kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

Nu kan du överföra data med knappen **Lägg till data** , och den kommer att importeras delvis.

### Använd flödet &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Om du vill använda &quot;[!UICONTROL Map CSV to XDM schema]&quot;-flödet följer du stegen i [Mappa en CSV-fil i självstudiekursen](../tutorials/map-a-csv-file.md). När du har kommit till *[!UICONTROL Add data]* steget bör du tänka på *[!UICONTROL Partial ingestion]* - och *[!UICONTROL Error diagnostics]* fälten.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Med *[!UICONTROL Partial ingestion]* växlingsknappen kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växlingsknappen *[!UICONTROL Error diagnostics]* visas bara när *[!UICONTROL Partial ingestion]* växlingsknappen är inaktiverad. Med den här funktionen kan du [!DNL Platform] generera detaljerade felmeddelanden om dina inkapslade batchar. Om *[!UICONTROL Partial ingestion]* växeln är aktiverad aktiveras förbättrad feldiagnostik automatiskt.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Med *[!UICONTROL Error threshold]* den kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

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

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om batchstatusen.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
            ...
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
            "outputRecordCount": 497
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

Om batchen har ett fel och feldiagnostik är aktiverat, kommer statusen att vara &quot;success&quot; med mer information om felet som finns i en hämtningsbar felfil.

## Nästa steg {#next-steps}

I den här självstudiekursen beskrivs hur du skapar eller ändrar en datauppsättning för att aktivera partiell gruppinmatning. Mer information om batchintag finns i Utvecklarhandbok för [batchintag](./api-overview.md).

## Feltyper för partiell batchöverföring {#appendix}

Delvis batchinmatning har fyra olika feltyper vid inmatning av data.

- [Oläsbara filer](#unreadable)
- [Ogiltiga scheman eller rubriker](#schemas-headers)
- [Otolkningsbara rader](#unparsable)
- [Ogiltig XDM-konvertering](#conversion)

### Oläsbara filer {#unreadable}

Om det finns oläsbara filer i den inlästa gruppen bifogas batchfelen på själva gruppen. Mer information om hur du hämtar den misslyckade batchen finns i guiden [](../quality/retrieve-failed-batches.md)Hämta misslyckade batchar.

### Ogiltiga scheman eller rubriker {#schemas-headers}

Om den inmatade gruppen har ett ogiltigt schema eller ogiltiga rubriker, bifogas batchfelen på själva gruppen. Mer information om hur du hämtar den misslyckade batchen finns i guiden [](../quality/retrieve-failed-batches.md)Hämta misslyckade batchar.

### Otolkningsbara rader {#unparsable}

Om det finns rader som inte kan parsas i den inkapslade gruppen kommer batchfelen att lagras i en fil som du kan komma åt med hjälp av slutpunkten som beskrivs nedan.

**API-format**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | Värdet `id` för gruppen som du hämtar felinformation från. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om rader som inte kan tolkas.

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### Ogiltig XDM-konvertering {#conversion}

Om den inmatade gruppen innehåller ogiltiga XDM-konverteringar lagras batchfelen i en fil som du kan komma åt med följande slutpunkt.

**API-format**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | Värdet `id` för gruppen som du hämtar felinformation från. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om felen vid XDM-konvertering.

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
