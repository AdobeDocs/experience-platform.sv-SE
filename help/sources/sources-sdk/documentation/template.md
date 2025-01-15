---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Självbetjäningsmall för dokumentation
description: Lär dig hur du ansluter Adobe Experience Platform till DIN KÄLLA med API:t för Flow Service.
exl-id: c6927a71-3721-461e-9752-8ebc0b7b1cca
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---

# Skapa en *YOURSOURCE*-anslutning med API:t [!DNL Flow Service]

*När du går igenom den här mallen ersätter eller tar du bort alla stycken i kursiv stil (med början från den här).*

*Börja med att uppdatera metadata (rubrik och beskrivning) högst upp på sidan. Please ignore all instances of DNL on this page. Det här är en tagg som hjälper våra maskinöversättningsprocesser att översätta sidan korrekt till flera språk som stöds. Vi lägger till taggar i dokumentationen när du har skickat den.*

## Översikt

*Ge en kort översikt över ditt företag, inklusive det värde det ger kunderna. Ta med en länk till din produktdokumentationswebbplats för ytterligare läsning.*

>[!IMPORTANT]
>
>Den här källkopplingen och dokumentationssidan skapas och underhålls av *YourSource* -teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *Infoga länk eller e-postadress där du kan komma åt uppdateringar*.

## Förhandskrav

*Lägg till information i det här avsnittet om allt som kunderna behöver känna till innan de börjar konfigurera källan i Adobe Experience Platform användargränssnitt. Det här kan vara om:*

* *måste läggas till i en tillåtelselista*
* *krav för e-posthashning*
* *kontoinformation på din sida*
* *Så här hämtar du en API-nyckel för att ansluta till din plattform*

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta *YOURSOURCE* till Experience Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| *autentiseringsuppgifter en* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |
| *autentiseringsuppgifter två* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |
| *autentiseringsuppgifter tre* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |

Mer information om de här autentiseringsuppgifterna finns i *YOURSOURCE* -autentiseringsdokumentationen. *Lägg till en länk till din plattforms autentiseringsdokumentation här*.

## Anslut *DIN KÄLLA* till plattformen med API:t [!DNL Flow Service]

I följande självstudiekurs får du hjälp med att skapa en *YOURSOURCE* -källanslutning och skapa ett dataflöde för att överföra *YOURCE*-data till plattformen med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Skapa en basanslutning {#base-connection}

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till slutpunkten `/connections` och anger dina autentiseringsuppgifter för *YOURCE* som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} base connection",
        "description": "{YOURSOURCE} base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth generic-rest-connector",
            "params": {
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}",
                "expirationDate": "{EXPIRATION_DATE}"
            }
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på din basanslutning. Kontrollera att namnet på din basanslutning är beskrivande, eftersom du kan använda detta för att söka efter information om din basanslutning. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din basanslutning. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för källan. Detta ID kan hämtas när källan har registrerats och godkänts via API:t [!DNL Flow Service]. |
| `auth.specName` | Autentiseringstypen som du använder för att autentisera källan till plattformen. |
| `auth.params.` | Innehåller de autentiseringsuppgifter som krävs för att autentisera källan. |

**Svar**

Ett svar returnerar den nyskapade basanslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att undersöka källans filstruktur och innehåll i nästa steg.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Utforska din källa {#explore}

Med det grundläggande anslutnings-ID som du skapade i det föregående steget kan du utforska filer och kataloger genom att utföra GET-begäranden.
Använd följande anrop för att hitta sökvägen till filen som du vill hämta till [!DNL Platform]:

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

När du gör en GET-förfrågan om att utforska källans filstruktur och innehåll måste du inkludera frågeparametrarna som listas i tabellen nedan:


| Parameter | Beskrivning |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Det grundläggande anslutnings-ID som genererades i föregående steg. |
| `objectType=rest` | Den typ av objekt som du vill utforska. För närvarande är det här värdet alltid inställt på `rest`. |
| `{OBJECT}` | Den här parametern krävs bara när du visar en viss katalog. Dess värde representerar sökvägen till den katalog du vill utforska. |
| `fileType=json` | Filtypen för filen som du vill hämta till plattformen. För närvarande är `json` den enda filtypen som stöds. |
| `{PREVIEW}` | Ett booleskt värde som definierar om innehållet i anslutningen stöder förhandsvisning. |
| `{SOURCE_PARAMS}` | Definierar parametrar för källfilen som du vill hämta till plattformen. Om du vill hämta den godkända formattypen för `{SOURCE_PARAMS}` måste du koda hela `list_id`-strängen i base64. I exemplet nedan motsvarar `"list_id": "10c097ca71"` som är kodad i base64 `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`. |


**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den efterfrågade filen.

```json
{
  "data": [
    {
      "members": [
        {
          "id": "cff65fb4c5f5828666ad846443720efd",
          "email_address": "roykent@gmail.com",
          "unique_email_id": "72c758cbf1",
          "full_name": "Roy Kent",
          "web_id": 547094062,
          "email_type": "html",
          "status": "subscribed",
          "merge_fields": {
            "FNAME": "Roy",
            "LNAME": "Kent",
            "ADDRESS": {
              "addr1": "",
              "addr2": "",
              "city": "Richmond",
              "state": "Virginia",
              "zip": "",
              "country": "US"
            },
            "PHONE": "",
            "BIRTHDAY": ""
          },
          "stats": {
            "avg_open_rate": 0,
            "avg_click_rate": 0
          },
          "ip_signup": "",
          "timestamp_signup": "",
          "ip_opt": "103.43.112.97",
          "timestamp_opt": "2021-06-01T15:31:36+00:00",
          "member_rating": 2,
          "last_changed": "2021-06-01T15:31:36+00:00",
          "language": "",
          "vip": false,
          "email_client": "",
          "location": {
            "latitude": 0,
            "longitude": 0,
            "gmtoff": 0,
            "dstoff": 0,
            "country_code": "",
            "timezone": ""
          },
          "source": "Admin Add",
          "tags_count": 0,
          "tags": [
             
          ],
          "list_id": "10c097ca71"
        }
      ],
      "list_id": "10c097ca71",
      "total_items": 2,
      "_links": [
        {
          "rel": "self",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
        },
        {
          "rel": "parent",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
        },
        {
          "rel": "create",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "POST",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
        }
      ]
    }
  ]
}
```

### Skapa en källanslutning {#source-connection}

Du kan skapa en källanslutning genom att göra en POST-förfrågan till API:t [!DNL Flow Service]. En källanslutning består av ett anslutnings-ID, en sökväg till källdatafilen och ett anslutnings-spec-ID.

**API-format**

```https
POST /sourceConnections
```

**Begäran**

Följande begäran skapar en källanslutning för *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Source Connection",
        "description": "{YOURSOURCE} Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "server": "us6",
            "listId": "10c097ca71"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för *YOURSOURCE*. Detta ID genererades i ett tidigare steg. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar källan. |
| `data.format` | Formatet på de *YOURSOURCE*-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i ett senare steg för att skapa ett dataflöde.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en plattformsdatauppsättning där källdata finns.

Ett mål-XDM-schema kan skapas genom att utföra en POST-begäran till [schemats register-API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Detaljerade steg om hur du skapar ett mål-XDM-schema finns i självstudiekursen [Skapa ett schema med API:t](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Skapa en måldatauppsättning {#target-dataset}

En måldatamängd kan skapas genom att utföra en POST-begäran till [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), som anger målschemats ID i nyttolasten.

Detaljerade steg om hur du skapar en måldatauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:t](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inmatade data ska lagras. Om du vill skapa en målanslutning måste du ange det fasta ID för anslutningsspecifikationen som motsvarar [!DNL Data Lake]. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Du har nu de unika identifierarna för ett målschema, en måldatamängd och ett anslutningsspec-ID för [!DNL Data Lake]. Med hjälp av dessa identifierare kan du skapa en målanslutning med API:t [!DNL Flow Service] för att ange den datauppsättning som ska innehålla inkommande källdata.

**API-format**

```https
POST /targetConnections
```

**Begäran**

Följande begäran skapar en målanslutning för *YOURSOURCE*:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Target Connection",
        "description": "{YOURSOURCE} Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på målanslutningen. Kontrollera att namnet på målanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om målanslutningen. |
| `description` | Ett valfritt värde som du kan inkludera för att ange mer information om målanslutningen. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar [!DNL Data Lake]. Detta fasta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Formatet för de *YOURSOURCE*-data som du vill hämta till plattformen. |
| `params.dataSetId` | Måldatauppsättnings-ID som hämtades i ett tidigare steg. |


**Svar**

Ett svar returnerar den nya målanslutningens unika identifierare (`id`). Detta ID krävs i senare steg.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste den först mappas till målschemat som måldatamängden följer. Detta uppnås genom att utföra en begäran om POST till [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) med datamappningar definierade i nyttolasten för begäran.

**API-format**

```http
POST /conversion/mappingSets
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdmSchema` | ID:t för [mål-XDM-schemat](#target-schema) genererades i ett tidigare steg. |
| `mappings.destinationXdmPath` | Mål-XDM-sökvägen dit källattributet mappas. |
| `mappings.sourceAttribute` | Källattributet som måste mappas till en mål-XDM-sökväg. |
| `mappings.identity` | Ett booleskt värde som anger om mappningsuppsättningen ska markeras för [!DNL Identity Service]. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade mappningen inklusive dess unika identifierare (`id`). Detta värde krävs i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Skapa ett flöde {#flow}

Det sista steget mot att överföra data från *YOURSOURCE* till plattformen är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

* [Source-anslutnings-ID](#source-connection)
* [Målanslutnings-ID](#target-connection)
* [Mappnings-ID](#mapping)

Ett dataflöde ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en begäran om POST samtidigt som du anger de tidigare angivna värdena i nyttolasten.

Om du vill schemalägga ett intag måste du först ange starttidsvärdet till epok time i sekunder. Sedan måste du ange frekvensvärdet till ett av de fem alternativen: `once`, `minute`, `hour`, `day` eller `week`. Intervallvärdet anger emellertid perioden mellan två på varandra följande frågor, och om du skapar en engångsinmatning behöver du inte ange något intervall. Intervallvärdet måste vara lika med eller större än `15` för alla andra frekvenser.


**API-format**

```http
POST /flows
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} dataflow",
        "description": "{YOURSOURCE} dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "246d052c-da4a-494a-937f-a0d17b1c6cf5"
        ],
        "targetConnectionIds": [
            "7c96c827-3ffd-460c-a573-e9558f72f263"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1625040887",
            "frequency": "minute",
            "interval": 15
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på dataflödet. Kontrollera att namnet på dataflödet är beskrivande, eftersom du kan använda det för att söka efter information om dataflödet. |
| `description` | Ett valfritt värde som du kan inkludera för att få mer information om dataflödet. |
| `flowSpec.id` | Det ID för flödesspecifikation som krävs för att skapa ett dataflöde. Detta fasta ID är: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Motsvarande version av flödesspecifikations-ID. Standardvärdet är `1.0`. |
| `sourceConnectionIds` | [källanslutnings-ID](#source-connection) genererades i ett tidigare steg. |
| `targetConnectionIds` | [målanslutnings-ID](#target-connection) genererades i ett tidigare steg. |
| `transformations` | Den här egenskapen innehåller de olika omformningar som behövs för att dina data ska kunna användas. Den här egenskapen krävs när data som inte är XDM-kompatibla skickas till plattformen. |
| `transformations.name` | Det namn som tilldelats omformningen. |
| `transformations.params.mappingId` | [Mappnings-ID](#mapping) genererades i ett tidigare steg. |
| `transformations.params.mappingVersion` | Motsvarande version av mappnings-ID. Standardvärdet är `0`. |
| `scheduleParams.startTime` | Den här egenskapen innehåller information om dataflödets ingsplanering. |
| `scheduleParams.frequency` | Frekvensen med vilken dataflödet samlar in data. Godtagbara värden är: `once`, `minute`, `hour`, `day` eller `week`. |
| `scheduleParams.interval` | Intervallet anger perioden mellan två på varandra följande flödeskörningar. Intervallets värde ska vara ett heltal som inte är noll. Intervall krävs inte när frekvens har angetts som `once` och ska vara större än eller lika med `15` för andra frekvensvärden. |

**Svar**

Ett lyckat svar returnerar ID:t (`id`) för det nyskapade dataflödet. Du kan använda det här ID:t för att övervaka, uppdatera eller ta bort dataflödet.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## Bilaga

Följande avsnitt innehåller information om hur du övervakar, uppdaterar och tar bort dataflödet.

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om flödeskörningar, slutförandestatus och fel. Fullständiga API-exempel finns i handboken om [att övervaka källans dataflöden med API:t](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Uppdatera ditt dataflöde

Uppdatera informationen om dataflödet, till exempel namn och beskrivning, samt körningsschema och associerade mappningsuppsättningar genom att göra en PATCH-begäran till `/flows`-slutpunkten i [!DNL Flow Service]-API:t, samtidigt som du anger ID:t för dataflödet. När du gör en PATCH-begäran måste du ange dataflödets unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken om att [uppdatera källkodsdataflöden med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Uppdatera ditt konto

Uppdatera namn, beskrivning och autentiseringsuppgifter för källkontot genom att utföra en PATCH-begäran till [!DNL Flow Service]-API:t och ange ditt grundläggande anslutnings-ID som en frågeparameter. När du gör en PATCH-begäran måste du ange källkontots unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken [Uppdatera ditt källkonto med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Ta bort ditt dataflöde

Ta bort dataflödet genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange ID:t för det dataflöde som du vill ta bort som en del av frågeparametern. Fullständiga API-exempel finns i guiden om att [ta bort dataflöden med API:t](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Ta bort ditt konto

Ta bort ditt konto genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange det grundläggande anslutnings-ID:t för kontot som du vill ta bort. Fullständiga API-exempel finns i guiden om att [ta bort ditt källkonto med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).