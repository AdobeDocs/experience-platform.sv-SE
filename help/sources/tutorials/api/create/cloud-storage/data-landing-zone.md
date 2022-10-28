---
keywords: Experience Platform;hemmabruk;populära ämnen;
solution: Experience Platform
title: Anslut Data Landing Zone till Adobe Experience Platform med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Data Landing Zone med API:t för Flow Service.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 1%

---

# Anslut [!DNL Data Landing Zone] till Adobe Experience Platform med API:t för Flow Service

[!DNL Data Landing Zone] är en säker, molnbaserad fillagringsfunktion för att överföra filer till Adobe Experience Platform. Data tas automatiskt bort från [!DNL Data Landing Zone] efter sju dagar.

Den här självstudiekursen visar hur du skapar en [!DNL Data Landing Zone] källanslutning med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Den här självstudiekursen innehåller även anvisningar om hur du hämtar [!DNL Data Landing Zone], samt visa och uppdatera dina uppgifter.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna skapa en [!DNL Data Landing Zone] källanslutning med [!DNL Flow Service] API.

Den här självstudiekursen kräver även att du läser guiden på [komma igång med plattforms-API:er](../../../../../landing/api-guide.md) om du vill lära dig hur du autentiserar till plattforms-API:er och tolkar exempelanrop som finns i dokumentationen.

## Hämta en användbar landningszon

Det första steget i att använda API:er för att komma åt [!DNL Data Landing Zone] ska göra en GET-förfrågan till `/landingzone` slutpunkt för [!DNL Connectors] API:n ger `type=user_drop_zone` som en del av ditt begärandehuvud.

**API-format**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Sidhuvuden | Beskrivning |
| --- | --- |
| `user_drop_zone` | The `user_drop_zone` -typ gör att API:t kan skilja en landningszonsbehållare från andra typer av behållare som är tillgängliga för dig. |

**Begäran**

Följande begäran hämtar en befintlig landningszon.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Svar**

Följande svar returnerar information om en landningszon, inklusive dess motsvarande `containerName` och `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `containerName` | Namnet på den landningszon som du har hämtat. |
| `containerTTL` | Förfallotid (i dagar) som gäller för dina data inom landningszonen. Alla inom en viss landningszon ska strykas efter sju dagar. |

## Hämta [!DNL Data Landing Zone] autentiseringsuppgifter

Så här hämtar du autentiseringsuppgifter för en [!DNL Data Landing Zone], gör en GET-förfrågan till `/credentials` slutpunkt för [!DNL Connectors] API.

**API-format**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**Begäran**

I följande exempel på begäran hämtas autentiseringsuppgifter för en befintlig landningszon.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Svar**

Följande svar returnerar autentiseringsuppgifter för din landningszon, inklusive din nuvarande `SASToken` och `SASUri`, samt `storageAccountName` som motsvarar behållaren för landningszonen.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `containerName` | Namnet på din landningszon. |
| `SASToken` | Den delade åtkomstsignaturtoken för din landningszon. Strängen innehåller all information som krävs för att godkänna en begäran. |
| `SASUri` | Den delade åtkomstsignaturens URI för din landningszon. Den här strängen är en kombination av URI:n till den landningszon som du autentiseras mot och dess motsvarande SAS-token, |


## Uppdatera [!DNL Data Landing Zone] autentiseringsuppgifter

Du kan uppdatera din `SASToken` genom att göra en POST-förfrågan till `/credentials` slutpunkt för [!DNL Connectors] API.

**API-format**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Sidhuvuden | Beskrivning |
| --- | --- |
| `user_drop_zone` | The `user_drop_zone` -typ gör att API:t kan skilja en landningszonsbehållare från andra typer av behållare som är tillgängliga för dig. |
| `refresh` | The `refresh` kan du återställa dina inloggningsuppgifter för landningszonen och automatiskt generera en ny `SASToken`. |

**Begäran**

Följande begäran uppdaterar dina inloggningsuppgifter för landningszonen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Svar**

Följande svar returnerar uppdaterade värden för `SASToken` och `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Utforska landningszonens filstruktur och innehåll

Du kan utforska filstrukturen och innehållet i din landningszon genom att göra en GET-förfrågan till `connectionSpecs` slutpunkt för [!DNL Flow Service] API.

**API-format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | Anslutningsspecifikations-ID som motsvarar [!DNL Data Landing Zone]. Detta fasta ID är: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med filer och mappar som finns i den efterfrågade katalogen. Observera `path` -egenskapen för filen som du vill överföra, eftersom du måste ange den i nästa steg för att kunna kontrollera dess struktur.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## Förhandsgranska landningszonens filstruktur och innehåll

Om du vill inspektera strukturen för en fil i din landningszon ska du utföra en GET-förfrågan och ange filens sökväg och typ som en frågeparameter.

**API-format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | Anslutningsspecifikations-ID som motsvarar [!DNL Data Landing Zone]. Detta fasta ID är: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Den typ av objekt som du vill komma åt. | `file` |
| `{OBJECT}` | Sökvägen till och namnet på det objekt du vill komma åt. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Filtypen. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Ett booleskt värde som definierar om filförhandsvisning stöds. | </ul><li>`true`</li><li>`false`</li></ul> |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den efterfrågade filen, inklusive filnamn och datatyper.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

### Använd `determineProperties` för att automatiskt identifiera filegenskapsinformation för en [!DNL Data Landing Zone]

Du kan använda `determineProperties` parameter för att automatiskt identifiera egenskapsinformation för filinnehållet i [!DNL Data Landing Zone] när du gör ett GET-anrop för att utforska källans innehåll och struktur.

#### `determineProperties` användningsfall

I följande tabell visas olika scenarier som du kan träffa på när du använder `determineProperties` eller ange information manuellt om filen.

| `determineProperties` | `queryParams` | Svar |
| --- | --- | --- |
| True | Ej tillämpligt | If `determineProperties` anges som en frågeparameter, upptäcks filegenskaperna och svaret returnerar ett nytt `properties` som innehåller information om filtyp, komprimeringstyp och kolumnavgränsare. |
| Ej tillämpligt | True | Om värdena för filtyp, komprimeringstyp och kolumnavgränsare anges manuellt som en del av `queryParams`, används de för att generera schemat och samma egenskaper returneras som en del av svaret. |
| True | True | Om båda alternativen utförs samtidigt returneras ett fel. |
| Ej tillämpligt | Ej tillämpligt | Om inget av de två alternativen anges returneras ett fel eftersom det inte finns något sätt att hämta egenskaper för svaret. |

**API-format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `determineProperties` | Den här frågeparametern tillåter [!DNL Flow Service] API för att identifiera information om filens egenskaper, inklusive information om filtyp, komprimeringstyp och kolumnavgränsare. | `true` |

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett svar returnerar strukturen för den efterfrågade filen, inklusive filnamn och datatyper, samt en `properties` nyckel, med information om `fileType`, `compressionType`och `columnDelimiter`.

+++Klicka på mig

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| Egenskap | Beskrivning |
| --- | --- |
| `properties.fileType` | Motsvarande filtyp för den efterfrågade filen. De filtyper som stöds är: `delimited`, `json`och `parquet`. |
| `properties.compressionType` | Motsvarande komprimeringstyp som används för den efterfrågade filen. Komprimeringstyperna som stöds är: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Motsvarande kolumnavgränsare som används för den efterfrågade filen. Ett teckenvärde är en tillåten kolumnavgränsare. Standardvärdet är ett komma `(,)`. |


## Skapa en källanslutning

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från. En källanslutning består av information som datakälla, dataformat och det källanslutnings-ID som behövs för att skapa ett dataflöde. En källanslutningsinstans är specifik för en klientorganisation och IMS-organisation.

Om du vill skapa en källanslutning skickar du en POST till `/sourceConnections` slutpunkt för [!DNL Flow Service] API.


**API-format**

```http
POST /sourceConnections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på [!DNL Data Landing Zone] källanslutning. |
| `data.format` | Formatet på de data du vill hämta till plattformen. |
| `params.path` | Sökvägen till filen som du vill hämta till plattformen. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar [!DNL Data Landing Zone]. Detta fasta ID är: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudiekurs för att skapa ett dataflöde.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du hämtat [!DNL Data Landing Zone] inloggningsuppgifter, utforskade filstrukturen för att hitta filen som du vill hämta till plattformen och skapade en källanslutning för att börja överföra data till plattformen. Du kan nu gå vidare till nästa självstudiekurs där du får lära dig hur [skapa ett dataflöde för att överföra molnlagringsdata till plattformen med [!DNL Flow Service] API](../../collect/cloud-storage.md).
