---
keywords: Experience Platform;hem;populära ämnen;molnlagring;molnlagring
solution: Experience Platform
title: Utforska ett högt lagringssystem med API:t för Flow Service
topic: overview
description: I den här självstudien används API:t för Flow Service för att utforska ett molnlagringssystem från tredje part.
translation-type: tm+mt
source-git-commit: 457fc9e1b0c445233f0f574fefd31bc1fc3bafc8
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---


# Utforska ett molnlagringssystem med API:t [!DNL Flow Service]

I den här självstudien används [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) för att utforska ett molnlagringssystem från tredje part.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till ett molnlagringssystem med API:t [!DNL Flow Service].

### Hämta ett anslutnings-ID

För att kunna utforska ett molnlagringsutrymme från tredje part med hjälp av [!DNL Platform] API:er måste du ha ett giltigt anslutnings-ID. Om du inte redan har en anslutning till det lagringsutrymme du vill arbeta med kan du skapa en genom följande självstudier:

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Utforska din molnlagring

Med anslutnings-ID:t för molnlagringen kan du utforska filer och kataloger genom att utföra GET-förfrågningar. När du gör GET-förfrågningar för att utforska ditt molnlagringsutrymme måste du inkludera frågeparametrarna som listas i tabellen nedan:

| Parameter | Beskrivning |
| --------- | ----------- |
| `objectType` | Den typ av objekt som du vill utforska. Ange det här värdet som antingen: <ul><li>`folder`: Utforska en specifik katalog</li><li>`root`: Utforska rotkatalogen.</li></ul> |
| `object` | Den här parametern krävs bara när du visar en viss katalog. Dess värde representerar sökvägen till den katalog du vill utforska. |

Använd följande anrop för att hitta sökvägen till filen som du vill hämta till [!DNL Platform]:

**API-format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONNECTION_ID}` | Anslutnings-ID för din källanslutning till molnlagring. |
| `{PATH}` | Sökvägen till en katalog. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med filer och mappar som finns i den efterfrågade katalogen. Observera egenskapen `path` för filen som du vill överföra, eftersom du måste ange den i nästa steg för att kunna kontrollera filens struktur.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect en fils struktur

Om du vill inspektera datafilens struktur från ditt molnlagringsutrymme utför du en GET-förfrågan och anger filens sökväg och typ som en frågeparameter.

Du kan inspektera datafilens struktur från molnlagringskällan genom att utföra en GET-begäran och samtidigt ange filens sökväg och typ. Du kan också inspektera olika filtyper, till exempel CSV, TSV eller komprimerad JSON och avgränsade filer, genom att ange deras filtyper som en del av frågeparametrarna.

**API-format**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Anslutnings-ID för din molnlagringskälla. |
| `{FILE_PATH}` | Sökvägen till filen som du vill inspektera. |
| `{FILE_TYPE}` | Filtypen. Filtyper som stöds:<ul><li>DELIMITED</code>: Avgränsaravgränsat värde. DSV-filer måste vara kommaavgränsade.</li><li>JSON</code>: JavaScript-objektnotation. JSON-filer måste vara XDM-kompatibla</li><li>PARQUET</code>: Apache Parquet. Parquet-filer måste vara XDM-kompatibla.</li></ul> |
| `{QUERY_PARAMS}` | Valfria frågeparametrar som kan användas för att filtrera resultat. Mer information finns i avsnittet [frågeparametrar](#query). |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den efterfrågade filen inklusive tabellnamn och datatyper.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## Använda frågeparametrar {#query}

[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) stöder användning av frågeparametrar för att förhandsgranska och inspektera olika filtyper.

| Parameter | Beskrivning |
| --------- | ----------- |
| `columnDelimiter` | Värdet för ett tecken som du angav som en kolumnavgränsare för att inspektera CSV- eller TSV-filer. Om parametern inte anges används standardvärdet som komma `(,)`. |
| `compressionType` | En obligatorisk frågeparameter för förhandsgranskning av en komprimerad avgränsad fil eller JSON-fil. Komprimerade filer som stöds är: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## Nästa steg

Genom att följa den här självstudiekursen har du utforskat ditt molnlagringssystem, hittat sökvägen till filen som du vill hämta till [!DNL Platform] och visat dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från ditt molnlagringsutrymme och överföra den till plattformen](../collect/cloud-storage.md).