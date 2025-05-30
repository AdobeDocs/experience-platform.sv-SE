---
title: Skapa en Source-anslutning och ett dataflöde för Mixpanel med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Mixpanel med API:t för Flow Service.
exl-id: 804b876d-6fd5-4a28-b33c-4ecab1ba3333
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1992'
ht-degree: 0%

---

# Skapa en källanslutning och ett dataflöde för [!DNL Mixpanel] med API:t [!DNL Flow Service]

I följande självstudiekurs får du hjälp med att skapa en källanslutning och ett dataflöde för att överföra [!DNL Mixpanel]-data till Adobe Experience Platform med [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) .

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Mixpanel] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL Mixpanel] till Experience Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `username` | Användarnamnet för tjänstkontot som motsvarar ditt [!DNL Mixpanel]-konto. Mer information finns i [[!DNL Mixpanel] tjänstkontodokumentationen](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account). | `Test8.6d4ee7.mp-service-account` |
| `password` | Lösenordet för tjänstkontot som motsvarar ditt [!DNL Mixpanel]-konto. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| `projectId` | Ditt projekt-ID för [!DNL Mixpanel]. Detta ID krävs för att skapa en källanslutning. Mer information finns i [[!DNL Mixpanel] projektinställningsdokumentationen](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) och [[!DNL Mixpanel] handboken om att skapa och hantera projekt](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) . | `2384945` |
| `timezone` | Tidszonen som motsvarar ditt [!DNL Mixpanel]-projekt. Tidszon krävs för att skapa en källanslutning. Mer information finns i [dokumentationen för projektinställningar på blandpanelen](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings). | `Pacific Standard Time` |

Mer information om hur du autentiserar [!DNL Mixpanel]-källan finns i [[!DNL Mixpanel] källöversikten](../../../../connectors/analytics/mixpanel.md).

## Skapa en basanslutning {#base-connection}

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skapar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Mixpanel]-autentiseringsuppgifter som en del av begärandetexten.

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
      "description": "Mixpanel base connection to authenticate to Experience Platform",
      "connectionSpec": {
          "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
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
| `connectionSpec.id` | Anslutningsspecifikations-ID för källan. Detta ID kan hämtas när källan har registrerats och godkänts via API:t [!DNL Flow Service]. |
| `auth.specName` | Autentiseringstypen som du använder för att autentisera källan till Experience Platform. |
| `auth.params.` | Innehåller de autentiseringsuppgifter som krävs för att autentisera källan. |
| `auth.params.username` | Användarnamnet som motsvarar ditt [!DNL Mixpanel]-konto. |
| `auth.params.password` | Lösenordet som motsvarar ditt [!DNL Mixpanel]-konto. |

**Svar**

Ett svar returnerar den nyskapade basanslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att undersöka källans filstruktur och innehåll i nästa steg.

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

När du utför GET-förfrågningar om källans filstruktur och innehåll måste du inkludera de frågeparametrar som anges i tabellen nedan:


| Parameter | Beskrivning |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Det grundläggande anslutnings-ID som genererades i föregående steg. |
| `objectType=rest` | Den typ av objekt som du vill utforska. För närvarande är det här värdet alltid inställt på `rest`. |
| `{OBJECT}` | Den här parametern krävs bara när du visar en viss katalog. Dess värde representerar sökvägen till den katalog du vill utforska. För den här källan är värdet `json`. |
| `fileType=json` | Filtypen för filen som du vill hämta till Experience Platform. För närvarande är `json` den enda filtypen som stöds. |
| `{PREVIEW}` | Ett booleskt värde som definierar om innehållet i anslutningen stöder förhandsvisning. |
| `{SOURCE_PARAMS}` | Definierar parametrar för källfilen som du vill hämta till Experience Platform. Om du vill hämta den godkända formattypen för `{SOURCE_PARAMS}` måste du koda hela `{"projectId":"2671127","timezone":"Pacific Standard Time"}`-strängen i base64. **Obs!**: I exemplet nedan motsvarar `"{"projectId":"2671127","timezone":"Pacific Standard Time"}"` som är kodad i base64 `eyJwcm9qZWN0SWQiOiIyNjcxMTI3IiwidGltZXpvbmUiOiJQYWNpZmljIFN0YW5kYXJkIFRpbWUifQ==`. |


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

Du kan skapa en källanslutning genom att göra en POST-begäran till API:t [!DNL Flow Service]. En källanslutning består av ett anslutnings-ID, en sökväg till källdatafilen och ett anslutnings-spec-ID.

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
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar källan. |
| `data.format` | Formatet på de [!DNL Mixpanel]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.projectId` | Ditt projekt-ID för [!DNL Mixpanel]. |
| `params.timezone` | Tidszonen för ditt [!DNL Mixpanel]-projekt. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i ett senare steg för att skapa ett dataflöde.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

## Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Experience Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en Experience Platform-datauppsättning där källdata finns.

Ett mål-XDM-schema kan skapas genom att en POST-begäran till [schemats register-API ](https://www.adobe.io/experience-platform-apis/references/schema-registry/) utförs.

Detaljerade steg om hur du skapar ett mål-XDM-schema finns i självstudiekursen [Skapa ett schema med API:t](../../../../../xdm/api/schemas.md).

## Skapa en måldatauppsättning {#target-dataset}

En måldatauppsättning kan skapas genom att en POST-begäran till [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/) utförs, med ID:t för målschemat i nyttolasten.

Detaljerade steg om hur du skapar en måldatauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:t](../../../../../catalog/api/create-dataset.md).

## Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inmatade data ska lagras. Om du vill skapa en målanslutning måste du ange det fasta anslutningsspecifikations-ID som motsvarar datasjön. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Nu har du de unika identifierarna ett målschema, en måldatamängd och ett anslutningsspec-ID till datasjön. Med hjälp av dessa identifierare kan du skapa en målanslutning med API:t [!DNL Flow Service] för att ange den datauppsättning som ska innehålla inkommande källdata.

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
| `data.format` | Formatet på de [!DNL Mixpanel]-data som du vill hämta till Experience Platform. |
| `params.dataSetId` | Måldatauppsättnings-ID som hämtades i ett tidigare steg. |


**Svar**

Ett svar returnerar den nya målanslutningens unika identifierare (`id`). Detta ID krävs i senare steg.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

## Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste den först mappas till målschemat som måldatamängden följer. Detta uppnås genom att utföra en POST-begäran till [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) med datamappningar definierade i nyttolasten för begäran.

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

## Skapa ett flöde {#flow}

Det sista steget mot att överföra data från [!DNL Mixpanel] till Experience Platform är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

* [Source-anslutnings-ID](#source-connection)
* [Målanslutnings-ID](#target-connection)
* [Mappnings-ID](#mapping)

Ett dataflöde ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en POST-begäran samtidigt som du anger de tidigare nämnda värdena i nyttolasten.

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
| `sourceConnectionIds` | [källanslutnings-ID](#source-connection) genererades i ett tidigare steg. |
| `targetConnectionIds` | [målanslutnings-ID](#target-connection) genererades i ett tidigare steg. |
| `transformations` | Den här egenskapen innehåller de olika omformningar som behövs för att dina data ska kunna användas. Den här egenskapen krävs när data som inte är XDM-kompatibla skickas till Experience Platform. |
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

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om flödeskörningar, slutförandestatus och fel. Fullständiga API-exempel finns i handboken om [att övervaka källans dataflöden med API:t](../../monitor.md).

### Uppdatera ditt dataflöde

Uppdatera informationen om dataflödet, till exempel namn och beskrivning, samt körningsschema och associerade mappningsuppsättningar genom att göra en PATCH-begäran till `/flows`-slutpunkten för [!DNL Flow Service] API, samtidigt som du anger ID:t för dataflödet. När du gör en PATCH-begäran måste du ange dataflödets unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i guiden om att [uppdatera källkodsdataflöden med API:t](../../update-dataflows.md).

### Uppdatera ditt konto

Uppdatera namn, beskrivning och autentiseringsuppgifter för källkontot genom att utföra en PATCH-begäran till [!DNL Flow Service]-API:t och ange ditt grundläggande anslutnings-ID som en frågeparameter. När du gör en PATCH-begäran måste du ange källkontots unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken [Uppdatera ditt källkonto med API](../../update.md).

### Ta bort ditt dataflöde

Ta bort dataflödet genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange ID:t för det dataflöde som du vill ta bort som en del av frågeparametern. Fullständiga API-exempel finns i guiden om att [ta bort dataflöden med API:t](../../delete-dataflows.md).

### Ta bort ditt konto

Ta bort ditt konto genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange det grundläggande anslutnings-ID:t för kontot som du vill ta bort. Fullständiga API-exempel finns i guiden om att [ta bort ditt källkonto med API](../../delete.md).