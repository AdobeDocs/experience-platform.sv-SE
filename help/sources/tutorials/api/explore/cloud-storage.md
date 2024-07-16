---
keywords: Experience Platform;hem;populära ämnen;molnlagring;molnlagring
title: Utforska en molnlagringsmapp med API:t för flödestjänsten
description: I den här självstudien används API:t för Flow Service för att utforska ett molnlagringssystem från tredje part.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 9b9803b4d2aeb2a86ef980f34ee34909679ea3d9
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Utforska dina molnlagringsmappar med API:t för [!DNL Flow Service]

I den här självstudiekursen beskrivs hur du utforskar och förhandsgranskar strukturen och innehållet i molnlagringen med hjälp av API:t [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>För att kunna utforska ditt molnlagringsutrymme måste du redan ha ett giltigt ID för basanslutning för en molnlagringskälla. Om du inte har det här ID:t kan du se [Källöversikt](../../../home.md#cloud-storage) för en lista över molnlagringskällor som du kan skapa en basanslutning med.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [Sandlådor](../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../landing/api-guide.md).

## Utforska dina molnlagringsmappar

Du kan hämta information om strukturen för dina molnlagringsmappar genom att göra en GET-förfrågan till [!DNL Flow Service]-API:t och samtidigt ange källans anslutnings-ID.

När du gör GET-förfrågningar för att utforska ditt molnlagringsutrymme måste du inkludera frågeparametrarna som listas i tabellen nedan:

| Parameter | Beskrivning |
| --------- | ----------- |
| `objectType` | Den typ av objekt som du vill utforska. Ange det här värdet som antingen: <ul><li>`folder`: Utforska en specifik katalog</li><li>`root`: Utforska rotkatalogen.</li></ul> |
| `object` | Den här parametern krävs bara när du visar en viss katalog. Dess värde representerar sökvägen till den katalog du vill utforska. |


**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Basanslutnings-ID för molnlagringskällan. |
| `{PATH}` | Sökvägen till en katalog. |

**Begäran**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&fileType=delimited&encoding=ISO-8859-1;
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Anslutnings-ID för din molnlagringskälla. |
| `{FILE_PATH}` | Sökvägen till filen som du vill inspektera. |
| `{FILE_TYPE}` | Filtypen. Filtyper som stöds:<ul><li><code>DELIMITED</code>: Avgränsaravgränsat värde. DSV-filer måste vara kommaavgränsade.</li><li><code>JSON</code>: JavaScript Object Notation. JSON-filer måste vara XDM-kompatibla</li><li><code>PARQUET</code>: Apache Parquet. Parquet-filer måste vara XDM-kompatibla.</li></ul> |
| `{QUERY_PARAMS}` | Valfria frågeparametrar som kan användas för att filtrera resultat. Mer information finns i avsnittet om [frågeparametrar](#query). |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) stöder användning av frågeparametrar för att förhandsgranska och inspektera olika filtyper.

| Parameter | Beskrivning |
| --------- | ----------- |
| `columnDelimiter` | Värdet för ett tecken som du angav som en kolumnavgränsare för att inspektera CSV- eller TSV-filer. Om parametern inte anges används standardvärdet för kommatecken `(,)`. |
| `compressionType` | En obligatorisk frågeparameter för förhandsgranskning av en komprimerad avgränsad fil eller JSON-fil. Komprimerade filer som stöds är: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Definierar vilken kodningstyp som ska användas vid förhandsgranskning av återgivning. Följande kodningstyper stöds: `UTF-8` och `ISO-8859-1`. **Obs!**: Parametern `encoding` är bara tillgänglig när du importerar avgränsade CSV-filer. Andra filtyper importeras med standardkodningen, `UTF-8`. |

## Nästa steg

Genom att följa den här självstudiekursen har du utforskat ditt molnlagringssystem, hittat sökvägen till filen som du vill hämta till [!DNL Platform] och visat dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från ditt molnlagringsutrymme och överföra dem till plattformen](../collect/cloud-storage.md).
