---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utforska ett molnlagringssystem med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 7cd9bec7336d0e1d9f3036cf862633f498002af8

---


# Utforska ett molnlagringssystem med API:t för Flow Service

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att utforska ett molnlagringssystem från en annan leverantör.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till ett molnlagringssystem med API:t för Flow Service.

### Hämta en basanslutning

För att kunna utforska en molnlagring från tredje part med hjälp av plattforms-API:er måste du ha ett giltigt basanslutnings-ID. Om du inte redan har en basanslutning för det lagringsutrymme du vill arbeta med kan du skapa en genom följande självstudier:

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../create/cloud-storage/adls-gen2.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör Flow Service, isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Utforska din molnlagring

Med basanslutningen för ditt molnlagringsutrymme kan du utforska filer och kataloger genom att utföra GET-begäranden. När du utför GET-begäranden för att utforska ditt molnlagringsutrymme måste du inkludera de frågeparametrar som anges i tabellen nedan:

| Parameter | Beskrivning |
| --------- | ----------- |
| `objectType` | Den typ av objekt som du vill utforska. Ange det här värdet som antingen: <ul><li>`folder`: Utforska en specifik katalog</li><li>`root`: Utforska rotkatalogen.</li></ul> |
| `object` | Den här parametern krävs bara när du visar en viss katalog. Dess värde representerar sökvägen till den katalog du vill utforska. |

Använd följande anrop för att hitta sökvägen till filen som du vill hämta till plattformen:

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID:t för en molnbaserad anslutning. |
| `{PATH}` | Sökvägen till en katalog. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med filer och mappar som finns i den efterfrågade katalogen. Observera vilken egenskap som `path` tillkommer den fil du vill överföra, eftersom du måste ange den i nästa steg för att kunna kontrollera filens struktur.

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## Inspektera filens struktur

Om du vill inspektera datafilens struktur från ditt molnlagringsutrymme utför du en GET-begäran och anger filens sökväg som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID:t för en molnbaserad anslutning. |
| `{FILE_PATH}` | Sökväg till en fil. |
| `{FILE_TYPE}` | Filtypen. Filtyper som stöds:<ul><li>AVGRÄNSAD</code>: Avgränsaravgränsat värde. DSV-filer måste vara kommaavgränsade.</li><li>JSON</code>: JavaScript-objektnotation. JSON-filer måste vara XDM-kompatibla</li><li>PARQUET</code>: Apache Parquet. Parquet-filer måste vara XDM-kompatibla.</li></ul> |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

## Nästa steg

Genom att följa den här självstudiekursen har du utforskat ditt molnlagringssystem, hittat sökvägen till filen som du vill hämta till plattformen och visat dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från ditt molnlagringsutrymme och överföra dem till plattformen](../collect/cloud-storage.md).