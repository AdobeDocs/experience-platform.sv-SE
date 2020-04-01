---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över partiell gruppinmatning i Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---



# Partiellt batchintag

Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som alla felaktiga data grupperas separat, tillsammans med information om varför de är ogiltiga.

Det här dokumentet innehåller en självstudiekurs för hantering av partiell batchimport.

I [bilagan](#partial-batch-ingestion-error-types) till den här självstudien finns dessutom en referens för feltyper av partiell gruppinmatning.

## Komma igång

Den här självstudiekursen kräver en fungerande kunskap om de olika Adobe Experience Platform-tjänsterna som är involverade i partiell gruppinmatning. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Batchförtäring](./overview.md): Den metod som används för att importera och lagra data från datafiler, som CSV och Parquet.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa plattforms-API:er.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Mer information om sandlådor i plattformen finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

## Aktivera en datauppsättning för partiell batchinmatning i API:t

>[!NOTE] I det här avsnittet beskrivs hur du aktiverar en datauppsättning för partiell batchimport med API:t. Instruktioner om hur du använder användargränssnittet finns i [Aktivera en datauppsättning för partiell batchförbrukning i](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) gränssnittssteget.

Du kan skapa en ny datauppsättning eller ändra en befintlig datauppsättning med partiellt intag aktiverat.

Om du vill skapa en ny datauppsättning följer du stegen i [Skapa en datauppsättning-självstudiekurs](../../catalog/api/create-dataset.md). När du har nått steget *Skapa en datauppsättning* lägger du till följande fält i begärandetexten:

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `errorThresholdPercentage` | Procentandelen godtagbara fel innan hela gruppen misslyckas. |

Om du vill ändra en befintlig datauppsättning följer du stegen i [Utvecklarhandbok](../../catalog/api/update-object.md)för katalog.

I datauppsättningen måste du lägga till taggen som beskrivs ovan.

## Aktivera en datauppsättning för partiell batchinmatning i användargränssnittet

>[!NOTE] I det här avsnittet beskrivs hur du aktiverar en datauppsättning för partiell batchimport med hjälp av användargränssnittet. Om du redan har aktiverat en datauppsättning för partiell gruppinmatning med API:t kan du hoppa fram till nästa avsnitt.

Om du vill aktivera en datauppsättning för partiellt intag via plattformsgränssnittet klickar du på **Datauppsättningar** i den vänstra navigeringen. Du kan antingen [skapa en ny datauppsättning](#create-a-new-dataset-with-partial-batch-ingestion-enabled) eller [ändra en befintlig datauppsättning](#modify-an-existing-dataset-to-enable-partial-batch-ingestion).

### Skapa en ny datauppsättning med partiell batchimport aktiverad

Om du vill skapa en ny datauppsättning följer du stegen i användarhandboken för [datauppsättningen](../../catalog/datasets/user-guide.md). När du har kommit till *Konfigurera datauppsättning* ska du tänka på fälten *Partiell matning* och *Feldiagnostik* .

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

Med *alternativet Partiellt* intag kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Växlingsknappen *Feldiagnostik* visas bara när *alternativet Partiellt* intag är inaktiverat. Med den här funktionen kan Platform generera detaljerade felmeddelanden om dina inkapslade batchar. Om *alternativet Delvis inmatning* är aktiverat aktiveras automatisk feldiagnostik.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

Med *feltröskeln* kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

### Ändra en befintlig datauppsättning för att aktivera partiell batchinmatning

Om du vill ändra en befintlig datauppsättning markerar du den datauppsättning som du vill ändra. Sidlisten till höger innehåller information om datauppsättningen.

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

Med *alternativet Partiellt* intag kan du aktivera eller inaktivera användning av partiell gruppinmatning.

Med *feltröskeln* kan du ange procentandelen godtagbara fel innan hela gruppen misslyckas. Som standard är värdet 5 %.

## Hämta fel för partiell gruppinmatning

Om batchar innehåller fel måste du hämta felinformation om dessa fel så att du kan importera data igen.

### Kontrollera status

Om du vill kontrollera status för den kapslade batchen måste du ange batchens ID i sökvägen till en GET-begäran.

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

## Nästa steg

I den här självstudiekursen beskrivs hur du skapar eller ändrar en datauppsättning för att aktivera partiell gruppinmatning. Mer information om batchintag finns i Utvecklarhandbok för [batchintag](./api-overview.md).

## Feltyper för partiell batchöverföring

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
