---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Skapa ett dataflöde för Zendesk med API:t för Flow Service
topic-legacy: tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Zendesk med API:t för Flow Service.
exl-id: 3e00e375-c6f8-407c-bded-7357ccf3482e
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# (Beta) Skapa ett dataflöde för [!DNL Zendesk] med [!DNL Flow Service] API

>[!NOTE]
>
>The [!DNL Zendesk] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

I följande självstudiekurs får du hjälp med att skapa en källanslutning och ett dataflöde som ger [!DNL Zendesk] data till plattformen med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Zendesk] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Zendesk] på Platform måste du ange värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `host` | Den unika domän som är specifik för ditt konto och som skapas under registreringsprocessen. | `https://yoursubdomain.zendesk.com` |
| `accessToken` | Zendesk API-token. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Mer information om hur du autentiserar [!DNL Zendesk] -källa, se [[!DNL Zendesk] källöversikt](../../../../connectors/customer-success/zendesk.md).

## Anslut [!DNL Zendesk] till plattform med [!DNL Flow Service] API

I följande självstudiekurs får du hjälp med att skapa en [!DNL Zendesk] källanslutning och skapa ett dataflöde som ger [!DNL Zendesk] data till plattformen med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Skapa en basanslutning {#base-connection}

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Zendesk] autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Zendesk]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk base connection",
        "description": "Zendesk base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "0a27232b-2c6e-4396-b8c6-c9fc24e37ba4",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth2 Refresh Code",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
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
| `auth.params.host` | Den unika domän som är specifik för ditt konto och som skapas under registreringsprocessen. Underdomänens format är `https://yoursubdomain.zendesk.com`. |
| `auth.params.accessToken` | Motsvarande åtkomsttoken som används för att autentisera källan. Detta krävs för OAuth-baserad autentisering. |

**Svar**

Ett lyckat svar returnerar den nyskapade basanslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att undersöka källans filstruktur och innehåll i nästa steg.

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
| `fileType=json` | Filtypen för filen som du vill hämta till plattformen. För närvarande `json` är den enda filtypen som stöds. |
| `{PREVIEW}` | Ett booleskt värde som definierar om innehållet i anslutningen stöder förhandsvisning. |
| `{SOURCE_PARAMS}` | Definierar parametrar för källfilen som du vill hämta till plattformen. Hämta den godkända formattypen för `{SOURCE_PARAMS}`måste du koda hela `parameter` sträng i base64. I exemplet nedan `"{}"` kodad i base64 motsvarar `e30`. |


**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den efterfrågade filen. I exemplet nedan i ``data[]`` endast en post visas, men det kan finnas flera poster.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "result": {
                "type": "object",
                "properties": {
                    "organization_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "external_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "role_type": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "custom_role_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "default_group_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "phone": {
                        "type": "string"
                    },
                    "shared_phone_number": {
                        "type": "boolean"
                    },
                    "alias": {
                        "type": "string"
                    },
                    "last_login_at": {
                        "type": "string"
                    },
                    "signature": {
                        "type": "string"
                    },
                    "details": {
                        "type": "string"
                    },
                    "notes": {
                        "type": "string"
                    },
                    "photo": {
                        "type": "string",
                        "media": {
                            "binaryEncoding": "base64",
                            "type": "image/png"
                        }
                    },
                    "active": {
                        "type": "boolean"
                    },
                    "created_at": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    },
                    "iana_time_zone": {
                        "type": "string"
                    },
                    "id": {
                        "type": "integer"
                    },
                    "locale": {
                        "type": "string"
                    },
                    "locale_id": {
                        "type": "integer"
                    },
                    "moderator": {
                        "type": "boolean"
                    },
                    "name": {
                        "type": "string"
                    },
                    "only_private_comments": {
                        "type": "boolean"
                    },
                    "report_csv": {
                        "type": "boolean"
                    },
                    "restricted_agent": {
                        "type": "boolean"
                    },
                    "result_type": {
                        "type": "string"
                    },
                    "role": {
                        "type": "integer"
                    },
                    "shared": {
                        "type": "boolean"
                    },
                    "shared_agent": {
                        "type": "boolean"
                    },
                    "suspended": {
                        "type": "boolean"
                    },
                    "ticket_restriction": {
                        "type": "string"
                    },
                    "time_zone": {
                        "type": "string"
                    },
                    "two_factor_auth_enabled": {
                        "type": "boolean"
                    },
                    "updated_at": {
                        "type": "string"
                    },
                    "url": {
                        "type": "string"
                    },
                    "verified": {
                        "type": "boolean"
                    },
                    "tags": {
                        "type": "array",
                        "items": {
                            "type": "string"
                        }
                    }
                }
            }
        }
    },
    "data": [
        {
            "result": {
                "id": 6106699702801,
                "url": "https://d3v-dxinfosys.zendesk.com/api/v2/users/6106699702801.json",
                "name": "test",
                "email": "test@org.com",
                "created_at": "2022-05-13T08:04:22Z",
                "updated_at": "2022-05-13T08:04:22Z",
                "time_zone": "Asia/Kolkata",
                "iana_time_zone": "Asia/Kolkata",
                "locale_id": 1,
                "locale": "en-US",
                "role": "end-user",
                "verified": false,
                "active": true,
                "shared": false,
                "shared_agent": false,
                "two_factor_auth_enabled": false,
                "moderator": false,
                "ticket_restriction": "requested",
                "only_private_comments": false,
                "restricted_agent": true,
                "suspended": false,
                "report_csv": false,
                "result_type": "user"
            }
        }
    ]
}
```

### Skapa en källanslutning {#source-connection}

Du kan skapa en källanslutning genom att göra en POST-förfrågan till [!DNL Flow Service] API. En källanslutning består av ett anslutnings-ID, en sökväg till källdatafilen och ett anslutnings-spec-ID.

**API-format**

```https
POST /sourceConnections
```

**Begäran**

Följande begäran skapar en källanslutning för [!DNL Zendesk]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk Source Connection",
        "description": "Zendesk Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "0a27232b-2c6e-4396-b8c6-c9fc24e37ba4",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {}
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för [!DNL Zendesk]. Detta ID genererades i ett tidigare steg. |
| `connectionSpec.id` | Det ID för anslutningsspecifikation som motsvarar källan. |
| `data.format` | Formatet på [!DNL Zendesk] data som du vill importera. För närvarande är det enda dataformatet som stöds `json`. |

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

### Skapa en måldatauppsättning {#target-dataset}

En måldatauppsättning kan skapas genom att en POST till [Katalogtjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), med ID:t för målschemat i nyttolasten.

Detaljerade anvisningar om hur du skapar en måldatauppsättning finns i självstudiekursen om [skapa en datauppsättning med API](../../../../../catalog/api/create-dataset.md).

### Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inmatade data ska lagras. Om du vill skapa en målanslutning måste du ange det fasta anslutningsspecifikations-ID som motsvarar datasjön. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Nu har du de unika identifierarna ett målschema, en måldatamängd och ett anslutningsspec-ID till datasjön. Med dessa identifierare kan du skapa en målanslutning med [!DNL Flow Service] API för att ange den datauppsättning som ska innehålla inkommande källdata.

**API-format**

```https
POST /targetConnections
```

**Begäran**

Följande begäran skapar en målanslutning för Zendesk:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk Target Connection",
        "description": "Zendesk Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "624bf42e16519d19496e3f67"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på målanslutningen. Kontrollera att namnet på målanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om målanslutningen. |
| `description` | Ett valfritt värde som du kan inkludera för att ange mer information om målanslutningen. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar datasjön. Detta fasta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Formatet på [!DNL Zendesk] data som du vill ta med till plattformen. |
| `params.dataSetId` | Måldatauppsättnings-ID som hämtades i ett tidigare steg. |


**Svar**

Ett godkänt svar returnerar den nya målanslutningens unika identifierare (`id`). Detta ID krävs i senare steg.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Skapa en mappning {#mapping}

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.id",
                "destination": "_extconndev.id",
                "name": "id",
                "description": "Zendesk"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.external_id",
                "destination": "_extconndev.external_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.role_type",
                "destination": "_extconndev.role_type"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.custom_role_id",
                "destination": "_extconndev.custom_role_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.default_group_id",
                "destination": "_extconndev.default_group_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.phone",
                "destination": "_extconndev.phone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared_phone_number",
                "destination": "_extconndev.shared_phone_number"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.verified",
                "destination": "_extconndev.verified"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.alias",
                "destination": "_extconndev.alias"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.last_login_at",
                "destination": "_extconndev.last_login_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.signature",
                "destination": "_extconndev.signature"
            },        {
                "sourceType": "ATTRIBUTE",
                "source": "result.details",
                "destination": "_extconndev.details"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.notes",
                "destination": "_extconndev.notes"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.active",
                "destination": "_extconndev.active"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.created_at",
                "destination": "_extconndev.created_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.email",
                "destination": "_extconndev.email"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.iana_time_zone",
                "destination": "_extconndev.iana_time_zone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.organization_id",
                "destination": "_extconndev.organization_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.locale",
                "destination": "_extconndev.locale"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.locale_id",
                "destination": "_extconndev.locale_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.moderator",
                "destination": "_extconndev.moderator"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.name",
                "destination": "_extconndev.name"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.only_private_comments",
                "destination": "_extconndev.only_private_comments"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.report_csv",
                "destination": "_extconndev.report_csv"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.restricted_agent",
                "destination": "_extconndev.restricted_agent"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.result_type",
                "destination": "_extconndev.result_type"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.role",
                "destination": "_extconndev.role"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared",
                "destination": "_extconndev.shared"
            },        {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared_agent",
                "destination": "_extconndev.shared_agent"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.time_zone",
                "destination": "_extconndev.time_zone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.two_factor_auth_enabled",
                "destination": "_extconndev.two_factor_auth_enabled"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.suspended",
                "destination": "_extconndev.suspended"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.updated_at",
                "destination": "_extconndev.updated_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.url",
                "destination": "_extconndev.url"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.verified",
                "destination": "_extconndev.verified"
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

### Skapa ett flöde {#flow}

Det sista steget mot att överföra data från Zendesk till Platform är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk dataflow",
        "description": "Zendesk dataflow",
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

### Övervaka dataflödet

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

### Uppdatera ditt dataflöde

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

### Ta bort ditt dataflöde

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext. Du kan bekräfta borttagningen genom att försöka utföra en sökbegäran (GET) i dataflödet. API:t returnerar ett HTTP 404-fel (Hittades inte) som anger att dataflödet har tagits bort.

### Uppdatera anslutningen

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "{USERNAME}",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Zendesk connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "Zendesk connection"
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

### Ta bort anslutningen

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET) på anslutningen.
