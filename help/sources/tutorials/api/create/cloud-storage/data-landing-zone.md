---
keywords: Experience Platform;hemmabruk;populära ämnen;
solution: Experience Platform
title: Anslut Data Landing Zone till Adobe Experience Platform med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Data Landing Zone med API:t för Flow Service.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 1%

---

# Anslut [!DNL Data Landing Zone] till Adobe Experience Platform med API:t för Flow Service

[!DNL Data Landing Zone] är en molnbaserad datalagringsfunktion för tillfällig fillagring som tillhandahålls med Adobe Experience Platform. [!DNL Data Landing Zone] används endast för att lägga in och ta bort data i och från plattformen. Data tas automatiskt bort från [!DNL Data Landing Zone] efter sju dagar.

I den här självstudiekursen får du hjälp med att skapa en [!DNL Data Landing Zone]-källanslutning med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Den här självstudiekursen innehåller även anvisningar om hur du hämtar din [!DNL Data Landing Zone] samt visar och uppdaterar dina inloggningsuppgifter.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna skapa en [!DNL Data Landing Zone]-källanslutning med hjälp av API:t [!DNL Flow Service].

I den här självstudien måste du även läsa guiden [komma igång med plattforms-API:er](../../../../../landing/api-guide.md) för att lära dig hur du autentiserar till plattforms-API:er och tolkar de exempelanrop som finns i dokumentationen.

## Hämta en användbar landningszon

Det första steget i att använda API:er för att få åtkomst till [!DNL Data Landing Zone] är att göra en GET-begäran till `/landingzone`-slutpunkten för API:t [!DNL Connectors] samtidigt som du anger `type=user_drop_zone` som en del av begärandehuvudet.

**API-format**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Sidhuvuden | Beskrivning |
| --- | --- |
| `user_drop_zone` | Typen `user_drop_zone` gör att API:t kan skilja en behållare för landningszon från andra typer av behållare som är tillgängliga för dig. |

**Begäran**

Följande begäran hämtar en befintlig landningszon.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Svar**

Följande svar returnerar information om en landningszon, inklusive motsvarande `containerName` och `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `containerName` | Namnet på den landningszon som du har hämtat. |
| `containerTTL` | Tidsinställningen som tillämpas på dina data inom landningszonen. Alla inom en viss landningszon ska strykas efter sju dagar. |

## Hämta [!DNL Data Landing Zone]-autentiseringsuppgifter

Om du vill hämta autentiseringsuppgifter för en [!DNL Data Landing Zone]-instans gör du en GET-begäran till `/credentials`-slutpunkten för API:t [!DNL Connectors].

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Svar**

Följande svar returnerar inloggningsinformationen för din landningszon, inklusive din nuvarande `SASToken` och `SASUri`, samt den `storageAccountName` som motsvarar din landningszonsbehållare.

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


## Uppdatera [!DNL Data Landing Zone]-autentiseringsuppgifter

Du kan uppdatera din `SASToken` genom att göra en POST-förfrågan till `/credentials`-slutpunkten för API:t [!DNL Connectors].

**API-format**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Sidhuvuden | Beskrivning |
| --- | --- |
| `user_drop_zone` | Typen `user_drop_zone` gör att API:t kan skilja en behållare för landningszon från andra typer av behållare som är tillgängliga för dig. |
| `refresh` | Med åtgärden `refresh` kan du återställa dina inloggningsuppgifter för landningszonen och automatiskt generera en ny `SASToken`. |

**Begäran**

Följande begäran uppdaterar dina inloggningsuppgifter för landningszonen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Du kan utforska filstrukturen och innehållet i landningszonen genom att göra en GET-förfrågan till `connectionSpecs`-slutpunkten för API:t [!DNL Flow Service].

**API-format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | Anslutningsspecifikationens ID som motsvarar [!DNL Data Landing Zone]. Detta fasta ID är: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
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
| `{CONNECTION_SPEC_ID}` | Anslutningsspecifikationens ID som motsvarar [!DNL Data Landing Zone]. Detta fasta ID är: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den efterfrågade filen inklusive tabellnamn och datatyper.

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

## Skapa en källanslutning

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från. En källanslutning består av information som datakälla, dataformat och det källanslutnings-ID som behövs för att skapa ett dataflöde. En källanslutningsinstans är specifik för en klientorganisation och IMS-organisation.

Om du vill skapa en källanslutning skickar du en POST till `/sourceConnections`-slutpunkten för API:t [!DNL Flow Service].


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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Namnet på din [!DNL Data Landing Zone]-källanslutning. |
| `data.format` | Formatet på de data du vill hämta till plattformen. |
| `params.path` | Sökvägen till filen som du vill hämta till plattformen. |
| `connectionSpec.id` | Anslutningsspecifikationens ID som motsvarar [!DNL Data Landing Zone]. Detta fasta ID är: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudiekurs för att skapa ett dataflöde.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du hämtat dina [!DNL Data Landing Zone]-autentiseringsuppgifter, utforskat filstrukturen för att hitta filen som du vill hämta till plattformen och skapat en källanslutning för att börja överföra dina data till plattformen. Du kan nu gå vidare till nästa självstudiekurs där du får lära dig att [skapa ett dataflöde för att överföra molnlagringsdata till plattformen med hjälp av [!DNL Flow Service] API](../../collect/cloud-storage.md).
