---
title: Anslut Data Landing Zone till Adobe Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Data Landing Zone med API:t för Flow Service.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 1%

---

# Anslut [!DNL Data Landing Zone] till Adobe Experience Platform med API:t för Flow Service

>[!IMPORTANT]
>
>Den här sidan är specifik för [!DNL Data Landing Zone] *source*-anslutningen i Experience Platform. Information om hur du ansluter till [!DNL Data Landing Zone] *destination*-kopplingen finns på [[!DNL Data Landing Zone] dokumentationssidan för målet](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] är en säker, molnbaserad fillagringsfunktion som hämtar filer till Adobe Experience Platform. Data tas automatiskt bort från [!DNL Data Landing Zone] efter sju dagar.

I den här självstudiekursen får du hjälp med att skapa en [!DNL Data Landing Zone]-källanslutning med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Den här självstudiekursen innehåller även anvisningar om hur du hämtar din [!DNL Data Landing Zone] samt visar och uppdaterar dina autentiseringsuppgifter.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Den här självstudien kräver även att du läser guiden [komma igång med Experience Platform API:er](../../../../../landing/api-guide.md) för att lära dig hur du autentiserar Experience Platform API:er och tolkar de exempelanrop som finns i dokumentationen.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna skapa en [!DNL Data Landing Zone]-källanslutning med API:t [!DNL Flow Service].

## Hämta en användbar landningszon

>[!IMPORTANT]
>
>Du måste ha åtkomstkontrollbehörighet **[!UICONTROL Manage Sources]** för att kunna använda API:erna för [!DNL Data Landing Zone] och hämta `type=user_drop_zone`. Mer information finns i [åtkomstkontrollsöversikten](../../../../../access-control/home.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Det första steget i att använda API:er för att få åtkomst till [!DNL Data Landing Zone] är att göra en GET-begäran till `/landingzone`-slutpunkten för [!DNL Connectors] API:t och samtidigt tillhandahålla `type=user_drop_zone` som en del av din begäranderubrik.

**API-format**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Svar**

Beroende på din leverantör returnerar en slutförd begäran följande:

>[!BEGINTABS]

>[!TAB Svar på Azure]

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `containerName` | Namnet på den landningszon som du hämtade. |
| `containerTTL` | Förfallotid (i dagar) som gäller för dina data inom landningszonen. Alla inom en viss landningszon ska strykas efter sju dagar. |


>[!TAB Svar på AWS]

```json
{
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "dlz-adf-connectors"
  },
  "dataTTL": {
    "timeUnit": "days",
    "timeQuantity": 7
  },
  "dlzProvider": "Amazon S3"
}
```

>[!ENDTABS]


## Hämta autentiseringsuppgifter för [!DNL Data Landing Zone]

Om du vill hämta autentiseringsuppgifter för en [!DNL Data Landing Zone] gör du en GET-begäran till `/credentials`-slutpunkten för API:t [!DNL Connectors].

**API-format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
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

Beroende på din leverantör returnerar en slutförd begäran följande:

>[!BEGINTABS]

>[!TAB Svar på Azure]

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `containerName` | Namnet på din [!DNL Data Landing Zone]. |
| `SASToken` | Underskriftstoken för delad åtkomst för din [!DNL Data Landing Zone]. Strängen innehåller all information som krävs för att godkänna en begäran. |
| `storageAccountName` | Namnet på ditt lagringskonto. |
| `SASUri` | Den delade åtkomstsignaturens URI för din [!DNL Data Landing Zone]. Den här strängen är en kombination av URI:n till [!DNL Data Landing Zone] som du autentiseras mot och dess motsvarande SAS-token. |
| `expiryDate` | Det datum då din SAS-token upphör att gälla. Du måste uppdatera din token före förfallodatumet för att kunna fortsätta använda den i ditt program för att överföra data till [!DNL Data Landing Zone]. Om du inte uppdaterar din token manuellt före det angivna förfallodatumet uppdateras den automatiskt och en ny token skapas när GET-inloggningsanropet utförs. |

>[!TAB Svar på AWS]

```json
{
  "credentials": {
    "clientId": "example-client-id",
    "awsAccessKeyId": "example-access-key-id",
    "awsSecretAccessKey": "example-secret-access-key",
    "awsSessionToken": "example-session-token"
  },
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "user_drop_zone"
  },
  "dlzProvider": "Amazon S3",
  "expiryTime": 1735689599
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `credentials.clientId` | Klient-ID för din [!DNL Data Landing Zone] i AWS. |
| `credentials.awsAccessKeyId` | Åtkomstnyckel-ID för din [!DNL Data Landing Zone] i AWS. |
| `credentials.awsSecretAccessKey` | Den hemliga åtkomstnyckeln för din [!DNL Data Landing Zone] i AWS. |
| `credentials.awsSessionToken` | Din AWS sessionstoken. |
| `dlzPath.bucketName` | Namnet på din AWS-bucket. |
| `dlzPath.dlzFolder` | Mappen [!DNL Data Landing Zone] som du använder. |
| `dlzProvider` | Providern [!DNL Data Landing Zone] som du använder. För Amazon blir detta [!DNL Amazon S3]. |
| `expiryTime` | Utgångsdatum i unix-tid. |

>[!ENDTABS]

### Hämta obligatoriska fält med API:er

När du har genererat din token kan du hämta de obligatoriska fälten via programmering med hjälp av exemplen nedan:

>[!BEGINTABS]

>[!TAB Python]

```py
import requests
 
# API endpoint
url = "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone"
 
headers = {
    "Authorization": "{TOKEN}",
    "Content-Type": "application/json",
    "x-gw-ims-org-id": "{ORG_ID}",
    "x-api-key": "{API_KEY}"
}
 
# Send GET request to the API
response = requests.get(url, headers=headers)
 
# Check if the request was successful
if response.status_code == 200:
    # Parse the response as JSON (if applicable)
    data = response.json()
 
    # Print or work with the fetched data 
    print(" Sas Token:", data['SASToken'])
    print(" Container Name:",  data['containerName'])
    print("\n")
 
else:
    # Print an error message if the request failed
    print(f"Failed to fetch data. Status code: {response.status_code}")
    print(f"Response: {response.text}")
```

>[!TAB Java]


```java
package org.example;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
 
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
 
public class Main {
    public static void main(String[] args) {
 
        ObjectMapper objectMapper = new ObjectMapper();
 
        try {
 
            DefaultHttpClient httpClient = new DefaultHttpClient();
            HttpGet getRequest = new HttpGet(
                "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone");
            getRequest.addHeader("accept", "application/json");
            getRequest.addHeader("Authorization","<TOKEN>");
            getRequest.addHeader("Content-Type", "application/json");
            getRequest.addHeader("x-gw-ims-org-id", "<ORG_ID>");
            getRequest.addHeader("x-api-key", "<API_KEY>");
 
            HttpResponse response = httpClient.execute(getRequest);
 
            if (response.getStatusLine().getStatusCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : "
                    + response.getStatusLine().getStatusCode());
            }
 
            final JsonNode jsonResponse = objectMapper.readTree(response.getEntity().getContent());
 
            System.out.println("\nOutput from API Response .... \n");
            System.out.printf("ContainerName: %s%n", jsonResponse.at("/containerName").textValue());
            System.out.printf("SASToken: %s%n", jsonResponse.at("/SASToken").textValue());
 
            httpClient.getConnectionManager().shutdown();
 
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

>[!ENDTABS]


## Uppdatera autentiseringsuppgifter för [!DNL Data Landing Zone]

Du kan uppdatera din `SASToken` genom att göra en POST-begäran till `/credentials`-slutpunkten för [!DNL Connectors] API:t.

**API-format**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Sidhuvuden | Beskrivning |
| --- | --- |
| `user_drop_zone` | Typen `user_drop_zone` gör att API:t kan skilja en behållare för landningszon från andra typer av behållare som är tillgängliga för dig. |
| `refresh` | Med åtgärden `refresh` kan du återställa dina autentiseringsuppgifter för landningszonen och automatiskt generera en ny `SASToken`. |

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
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## Utforska landningszonens filstruktur och innehåll

Du kan utforska filstrukturen och innehållet i landningszonen genom att göra en GET-begäran till `connectionSpecs`-slutpunkten för [!DNL Flow Service] API.

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

Om du vill inspektera strukturen för en fil i landningszonen utför du en GET-begäran och anger filens sökväg och typ som en frågeparameter.

**API-format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | Anslutningsspecifikations-ID som motsvarar [!DNL Data Landing Zone]. Detta fasta ID är: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Den typ av objekt som du vill komma åt. | `file` |
| `{OBJECT}` | Sökvägen till och namnet på det objekt som du vill komma åt. | `dlz-user-container/data8.csv` |
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

Du kan använda parametern `determineProperties` för att automatiskt identifiera egenskapsinformation för filinnehållet i [!DNL Data Landing Zone] när du gör ett GET-anrop för att utforska innehållet och strukturen i källan.

#### `determineProperties` använder fall

I följande tabell visas olika scenarier som du kan träffa på när du använder frågeparametern `determineProperties` eller manuellt anger information om filen.

| `determineProperties` | `queryParams` | Svar |
| --- | --- | --- |
| True | N/A | Om `determineProperties` anges som en frågeparameter, sker identifiering av filegenskaper och svaret returnerar en ny `properties`-nyckel som innehåller information om filtyp, komprimeringstyp och kolumnavgränsare. |
| N/A | True | Om värdena för filtyp, komprimeringstyp och kolumnavgränsare anges manuellt som en del av `queryParams`, används de för att generera schemat och samma egenskaper returneras som en del av svaret. |
| True | True | Om båda alternativen utförs samtidigt returneras ett fel. |
| N/A | N/A | Om inget av de två alternativen anges returneras ett fel eftersom det inte finns något sätt att hämta egenskaper för svaret. |

**API-format**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `determineProperties` | Med den här frågeparametern kan API:t [!DNL Flow Service] identifiera information om filens egenskaper, inklusive information om filtyp, komprimeringstyp och kolumnavgränsare. | `true` |

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

Ett lyckat svar returnerar strukturen för den efterfrågade filen, inklusive filnamn och datatyper, samt en `properties`-nyckel, som innehåller information om `fileType`, `compressionType` och `columnDelimiter`.

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
| `properties.fileType` | Motsvarande filtyp för den efterfrågade filen. De filtyper som stöds är: `delimited`, `json` och `parquet`. |
| `properties.compressionType` | Motsvarande komprimeringstyp som används för den efterfrågade filen. Komprimeringstyperna som stöds är: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Motsvarande kolumnavgränsare som används för den efterfrågade filen. Ett enda teckenvärde är en tillåten kolumnavgränsare. Standardvärdet är kommatecken `(,)`. |


## Skapa en källanslutning

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från. En källanslutning består av information som datakälla, dataformat och det källanslutnings-ID som behövs för att skapa ett dataflöde. En källanslutningsinstans är specifik för en klientorganisation och organisation.

Om du vill skapa en källanslutning skickar du en POST-begäran till `/sourceConnections`-slutpunkten för [!DNL Flow Service] API:t.


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
| `name` | Namnet på [!DNL Data Landing Zone]-källanslutningen. |
| `data.format` | Formatet på de data du vill hämta till Experience Platform. |
| `params.path` | Sökvägen till filen som du vill hämta till Experience Platform. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar [!DNL Data Landing Zone]. Detta fasta ID är: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudie för att skapa ett dataflöde.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du hämtat dina [!DNL Data Landing Zone]-inloggningsuppgifter, utforskat filstrukturen för att hitta filen som du vill hämta till Experience Platform och skapat en källanslutning för att börja överföra dina data till Experience Platform. Du kan nu gå vidare till nästa självstudiekurs, där du får lära dig hur du [skapar ett dataflöde för att överföra molnlagringsdata till Experience Platform med  [!DNL Flow Service] API](../../collect/cloud-storage.md).
