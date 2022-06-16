---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: (Beta) Skapa en källanslutning och ett dataflöde för blandpanelen med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Mixpanel med API:t för Flow Service.
hide: true
hidefromtoc: true
source-git-commit: 0a21280aaeb62374437c208da83cd4b42569ee91
workflow-type: tm+mt
source-wordcount: '2391'
ht-degree: 0%

---

# (Beta) Skapa en källanslutning och ett dataflöde för [!DNL Mixpanel] med [!DNL Flow Service] API

>[!NOTE]
>
>The [!DNL Mixpanel] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

I följande självstudiekurs får du hjälp med att skapa en källanslutning och ett dataflöde som ger [!DNL Mixpanel] data till Adobe Experience Platform med [API för flödestjänst](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Mixpanel] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL Mixpanel] till Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `host` | The [!DNL Mixpanel] API-slutpunkt för export av rådata. Se [!DNL Raw Data Export API] i [API-referensdokumentation för blandpanelen](https://developer.mixpanel.com/reference/overview) för mer information. | `https://data.mixpanel.com` |
| `username` | Användarnamnet för tjänstkontot som motsvarar ditt [!DNL Mixpanel] konto. Se [[!DNL Mixpanel] dokumentation för tjänstkonton](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) för mer information. | `Test8.6d4ee7.mp-service-account` |
| `password` | Lösenordet för tjänstkontot som motsvarar ditt [!DNL Mixpanel] konto. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| `projectId` | Dina [!DNL Mixpanel] projekt-ID. Detta ID krävs för att skapa en källanslutning. Se [[!DNL Mixpanel] dokumentation för projektinställningar](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) och [[!DNL Mixpanel] guide för att skapa och hantera projekt](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) för mer information. | `2384945` |
| `timezone` | Den tidszon som motsvarar din [!DNL Mixpanel] projekt. Tidszon krävs för att skapa en källanslutning. Se [Dokumentation för projektinställningar på blandpanelen](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) för mer information. | `Pacific Standard Time` |

Mer information om hur du autentiserar [!DNL Mixpanel] -källa, se [[!DNL Mixpanel] källöversikt](../../../../connectors/analytics/mixpanel.md).

## Skapa en basanslutning {#base-connection}

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Mixpanel] autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Mixpanel]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Mixpanel base connection",
      "description": "Mixpanel base connection to authenticate to Platform",
      "connectionSpec": {
          "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "https://data.mixpanel.com",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på din basanslutning. Kontrollera att namnet på din basanslutning är beskrivande, eftersom du kan använda detta för att söka efter information om din basanslutning. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din basanslutning. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för källan. Detta ID kan hämtas när källan har registrerats och godkänts via [!DNL Flow Service] API. |
| `auth.specName` | Autentiseringstypen som du använder för att autentisera källan till plattformen. |
| `auth.params.` | Innehåller de autentiseringsuppgifter som krävs för att autentisera källan. |
| `auth.params.host` | Den unika domän som är specifik för ditt konto och som skapas under registreringsprocessen. |
| `auth.params.username` | Användarnamnet som motsvarar ditt [!DNL Mixpanel] konto. |
| `auth.params.password` | Lösenordet som motsvarar [!DNL Mixpanel] konto. |

**Svar**

Ett lyckat svar returnerar den nyskapade basanslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att undersöka källans filstruktur och innehåll i nästa steg.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

## Utforska din källa {#explore}

Med det grundläggande anslutnings-ID som du skapade i det föregående steget kan du utforska filer och kataloger genom att utföra GET-begäranden.
Använd följande anrop för att hitta sökvägen till filen som du vill hämta till Experience Platform:

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

När du gör en GET-förfrågan om att utforska källans filstruktur och innehåll måste du inkludera frågeparametrarna som listas i tabellen nedan:


| Parameter | Beskrivning |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Det grundläggande anslutnings-ID som genererades i föregående steg. |
| `objectType=rest` | Den typ av objekt som du vill utforska. För närvarande är det här värdet alltid inställt på `rest`. |
| `{OBJECT}` | Den här parametern krävs bara när du visar en viss katalog. Dess värde representerar sökvägen till den katalog du vill utforska. För den här källan skulle värdet vara `json`. |
| `fileType=json` | Filtypen för filen som du vill hämta till plattformen. För närvarande `json` är den enda filtypen som stöds. |
| `{PREVIEW}` | Ett booleskt värde som definierar om innehållet i anslutningen stöder förhandsvisning. |
| `{SOURCE_PARAMS}` | Definierar parametrar för källfilen som du vill hämta till plattformen. Hämta den godkända formattypen för `{SOURCE_PARAMS}`måste du koda hela `{"projectId":"2671127","timezone":"Pacific Standard Time"}` sträng i base64. **Anteckning**: I exemplet nedan `"{"projectId":"2671127","timezone":"Pacific Standard Time"}"` kodad i base64 motsvarar `eyJwcm9qZWN0SWQiOiIyNjcxMTI3IiwidGltZXpvbmUiOiJQYWNpZmljIFN0YW5kYXJkIFRpbWUifQ==`. |


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
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "event": {
                "type": "string"
            },
            "properties": {
                "type": "object",
                "properties": {
                    "$mp_api_endpoint": {
                        "type": "string"
                    },
                    "$insert_id": {
                        "type": "string"
                    },
                    "item_id": {
                        "type": "string"
                    },
                    "distinct_id": {
                        "type": "string"
                    },
                    "$mp_api_timestamp_ms": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "item_price": {
                        "type": "string"
                    },
                    "$import": {
                        "type": "boolean"
                    },
                    "item_name": {
                        "type": "string"
                    },
                    "time": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "mp_processing_time_ms": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    }
                }
            }
        }
    },
    "data": [
        {
            "event": "Items purchased",
            "properties": {
                "time": 1652825148,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652850348643,
                "item_id": "29066",
                "item_name": "charger",
                "item_price": "800.00",
                "mp_processing_time_ms": 1652850348702
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1652423938,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652449138115,
                "item_id": "29036",
                "item_name": "chair",
                "item_price": "5000.00",
                "mp_processing_time_ms": 1652449138173
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1652854256,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652879456538,
                "item_id": "29066",
                "item_name": "mobile",
                "item_price": "7000.00",
                "mp_processing_time_ms": 1652879456604
            }
        },
        {
            "event": "Sign off",
            "properties": {
                "time": 1648140611,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648555709515,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648555710375
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1648140612,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648556481708,
                "item_id": "29073",
                "item_name": "Pen",
                "item_price": "1000.00",
                "mp_processing_time_ms": 1648556481880
            }
        },
        {
            "event": "Sign in",
            "properties": {
                "time": 1648140614,
                "distinct_id": "test1@test.com",
                "$import": true,
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648556032401,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648556032462
            }
        },
        {
            "event": "Item Purchased",
            "properties": {
                "time": 1648165814,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b74",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648480684785,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648480685058
            }
        },
        {
            "event": "Item Purchased",
            "properties": {
                "time": 1648165814,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648551687866,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648551687922
            }
        },
        {
            "event": "Sign off",
            "properties": {
                "time": 1648530419,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648555619274,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648555619326
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1648566534,
                "distinct_id": "test1@test.com",
                "$import": true,
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648635830114,
                "item_id": "29073",
                "item_name": "Pen",
                "item_price": "1000.00",
                "mp_processing_time_ms": 1648635831010
            }
        }
    ]
}
```

## Skapa en källanslutning {#source-connection}

Du kan skapa en källanslutning genom att göra en POST-förfrågan till [!DNL Flow Service] API. En källanslutning består av ett anslutnings-ID, en sökväg till källdatafilen och ett anslutnings-spec-ID.

**API-format**

```https
POST /sourceConnections
```

**Begäran**

Följande begäran skapar en källanslutning för [!DNL Mixpanel]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Mixpanel source connection",
      "description": "Mixpanel source connection",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "projectId": "{PROJECT_ID}",
          "timezone": "{TIMEZONE}"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för [!DNL Mixpanel]. Detta ID genererades i ett tidigare steg. |
| `connectionSpec.id` | Det ID för anslutningsspecifikation som motsvarar källan. |
| `data.format` | Formatet på [!DNL Mixpanel] data som du vill importera. För närvarande är det enda dataformatet som stöds `json`. |
| `params.projectId` | Dina [!DNL Mixpanel] projekt-ID. |
| `params.timezone` | Tidszonen för din [!DNL Mixpanel] projekt. |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i ett senare steg för att skapa ett dataflöde.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

## Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en plattformsdatauppsättning där källdata finns.

Ett mål-XDM-schema kan skapas genom att utföra en POST-begäran till [API för schemaregister](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Detaljerade anvisningar om hur du skapar ett XDM-målschema finns i självstudiekursen om [skapa ett schema med API](../../../../../xdm/api/schemas.md).

## Skapa en måldatauppsättning {#target-dataset}

En måldatauppsättning kan skapas genom att en POST till [Katalogtjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), med ID:t för målschemat i nyttolasten.

Detaljerade anvisningar om hur du skapar en måldatauppsättning finns i självstudiekursen om [skapa en datauppsättning med API](../../../../../catalog/api/create-dataset.md).

## Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inmatade data ska lagras. Om du vill skapa en målanslutning måste du ange det fasta anslutningsspecifikations-ID som motsvarar datasjön. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Nu har du de unika identifierarna ett målschema, en måldatamängd och ett anslutningsspec-ID till datasjön. Med dessa identifierare kan du skapa en målanslutning med [!DNL Flow Service] API för att ange den datauppsättning som ska innehålla inkommande källdata.

**API-format**

```https
POST /targetConnections
```

**Begäran**

Följande begäran skapar en målanslutning för [!DNL Mixpanel]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{Mixpanel} Target Connection",
        "description": "{Mixpanel} Target Connection",
        "connectionSpec": {
            "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
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
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar datasjön. Detta fasta ID är: `fd2c8ff3-1de0-4f6b-8fa8-4264784870eb`. |
| `data.format` | Formatet på [!DNL Mixpanel] data som du vill ta med till plattformen. |
| `params.dataSetId` | Måldatauppsättnings-ID som hämtades i ett tidigare steg. |


**Svar**

Ett godkänt svar returnerar den nya målanslutningens unika identifierare (`id`). Detta ID krävs i senare steg.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

## Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste den först mappas till målschemat som måldatamängden följer. Detta uppnås genom att en POST begär att [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) med datamappningar definierade i nyttolasten för begäran.

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
              "sourceType": "ATTRIBUTE",
              "source": "data.distinct_id",
              "destination": "_extconndev.distinct_id",
              "name": "distinct_id",
              "description": "Mixpanel"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.event_name",
              "destination": "_extconndev.event_name"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.import",
              "destination": "_extconndev.import"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.insert_id",
              "destination": "_extconndev.insert_id"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_id",
              "destination": "_extconndev.item_id"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_name",
              "destination": "_extconndev.item_name"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_price",
              "destination": "_extconndev.item_price"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_api_endpoint",
              "destination": "_extconndev.mp_api_endpoint"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_api_timestamp_ms",
              "destination": "_extconndev.mp_api_timestamp_ms"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_processing_time_ms",
              "destination": "_extconndev.mp_processing_time_ms"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.time",
              "destination": "_extconndev.time"
          }
      ]
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdmSchema` | ID för [mål-XDM-schema](#target-schema) som genererats i ett tidigare steg. |
| `mappings.destinationXdmPath` | Mål-XDM-sökvägen dit källattributet mappas. |
| `mappings.sourceAttribute` | Källattributet som måste mappas till en mål-XDM-sökväg. |
| `mappings.identity` | Ett booleskt värde som anger om mappningsuppsättningen ska markeras för [!DNL Identity Service]. |

**Svar**

Ett godkänt svar returnerar information om den nyligen skapade mappningen inklusive dess unika identifierare (`id`). Detta värde krävs i ett senare steg för att skapa ett dataflöde.

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

## Skapa ett flöde {#flow}

Det sista steget mot att hämta in data från [!DNL Mixpanel] till Platform är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

* [Källanslutnings-ID](#source-connection)
* [Målanslutnings-ID](#target-connection)
* [Mappnings-ID](#mapping)

Ett dataflöde ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en begäran om POST samtidigt som du anger de tidigare angivna värdena i nyttolasten.

Om du vill schemalägga ett intag måste du först ange starttidsvärdet till epok time i sekunder. Sedan måste du ange frekvensvärdet till ett av de fem alternativen: `once`, `minute`, `hour`, `day`, eller `week`. Intervallvärdet anger emellertid perioden mellan två på varandra följande frågor, och om du skapar en engångsinmatning behöver du inte ange något intervall. För alla andra frekvenser måste intervallvärdet anges till lika med eller större än `15`.


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
      "name": "{Mixpanel} dataflow",
      "description": "{Mixpanel} dataflow",
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
| `sourceConnectionIds` | The [källanslutnings-ID](#source-connection) som genererats i ett tidigare steg. |
| `targetConnectionIds` | The [målanslutnings-ID](#target-connection) som genererats i ett tidigare steg. |
| `transformations` | Den här egenskapen innehåller de olika omformningar som behövs för att dina data ska kunna användas. Den här egenskapen krävs när data som inte är XDM-kompatibla skickas till plattformen. |
| `transformations.name` | Det namn som tilldelats omformningen. |
| `transformations.params.mappingId` | The [mappnings-ID](#mapping) som genererats i ett tidigare steg. |
| `transformations.params.mappingVersion` | Motsvarande version av mappnings-ID. Standardvärdet är `0`. |
| `scheduleParams.startTime` | Den här egenskapen innehåller information om dataflödets ingsplanering. |
| `scheduleParams.frequency` | Frekvensen med vilken dataflödet samlar in data. Godtagbara värden är: `once`, `minute`, `hour`, `day`, eller `week`. |
| `scheduleParams.interval` | Intervallet anger perioden mellan två på varandra följande flödeskörningar. Intervallets värde ska vara ett heltal som inte är noll. Intervall krävs inte när frekvens har angetts som `once` och ska vara större än eller lika med `15` för andra frekvensvärden. |

**Svar**

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet. Du kan använda det här ID:t för att övervaka, uppdatera eller ta bort dataflödet.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om flödeskörningar, slutförandestatus och fel.

**API-format**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**Begäran**

Följande begäran hämtar specifikationerna för ett befintligt dataflöde.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om flödets körning, inklusive information om dess skapandedatum, käll- och målanslutningar samt flödets unika identifierare (`id`).

```json
{
    "items": [
        {
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
            "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `items` | Innehåller en enda nyttolast av metadata som är associerade med din specifika flödeskörning. |
| `metrics` | Definierar egenskaper för data i flödeskörningen. |
| `activities` | Definierar hur data omformas. |
| `durationSummary` | Definierar start- och sluttiden för flödeskörningen. |
| `sizeSummary` | Definierar datavolymen i byte. |
| `recordSummary` | Definierar antalet poster i data. |
| `fileSummary` | Definierar antalet filer för data. |
| `statusSummary` | Definierar om flödeskörningen är en lyckad eller misslyckad åtgärd. |

## Uppdatera ditt dataflöde

Om du vill uppdatera ditt dataflödes körningsschema, namn och beskrivning utför du en PATCH-begäran till [!DNL Flow Service] API när du anger ditt flödes-ID, version och det nya schema som du vill använda.

>[!IMPORTANT]
>
>The `If-Match` måste anges när du gör en PATCH-begäran. Värdet för den här rubriken är den unika taggen för dataflödet som du vill uppdatera.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäran uppdaterar ditt flödeskörningsschema samt dataflödets namn och beskrivning.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "New dataflow name"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Updated dataflow description"
            }
        ]'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Sökvägen till den parameter som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Ta bort ditt dataflöde

Med ett befintligt flödes-ID kan du ta bort ett dataflöde genom att göra en DELETE-begäran till [!DNL Flow Service] API.

**API-format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Unika `id` värdet för det dataflöde som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext. Du kan bekräfta borttagningen genom att försöka utföra en sökbegäran (GET) i dataflödet. API:t returnerar ett HTTP 404-fel (Hittades inte) som anger att dataflödet har tagits bort.

## Uppdatera anslutningen

Om du vill uppdatera anslutningsens namn, beskrivning och autentiseringsuppgifter utför du en PATCH-begäran till [!DNL Flow Service] API när du anger ditt grundläggande anslutnings-ID, version och den nya information du vill använda.

>[!IMPORTANT]
>
>The `If-Match` måste anges när du gör en PATCH-begäran. Värdet för den här rubriken är den unika versionen av anslutningen som du vill uppdatera.

**API-format**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Unika `id` värdet för anslutningen som du vill uppdatera. |

**Begäran**

Följande begäran innehåller ett nytt namn och en beskrivning samt en ny uppsättning autentiseringsuppgifter för att uppdatera anslutningen med.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera den åtgärd som krävs för att uppdatera anslutningen. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Sökvägen till den parameter som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt grundläggande anslutnings-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt anslutnings-ID.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Ta bort anslutningen

När du har ett befintligt basanslutnings-ID utför du en DELETE-förfrågan till [!DNL Flow Service] API.

**API-format**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Unika `id` värdet för den basanslutning som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET) på anslutningen.
