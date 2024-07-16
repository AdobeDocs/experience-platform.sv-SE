---
title: Skapa en källanslutning och ett dataflöde för Pinterest Ads med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Pinterest Ads med API:t för Flow Service.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 293a3ec9-38ea-4b71-a923-1f4e28a41236
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 0%

---

# Skapa en källanslutning och ett dataflöde för [!DNL Pinterest Ads] med API:t [!DNL Flow Service]

>[!NOTE]
>
>Källan [!DNL Pinterest Ads] är i betaversion. Läs [källöversikten](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

I följande självstudiekurs får du hjälp med att skapa en [!DNL Pinterest Ads]-källanslutning och ett dataflöde för att överföra [[!DNL Pinterest Ads]](https://ads.pinterest.com/)-data till Adobe Experience Platform med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång {#getting-started}

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Pinterest Ads] med API:t [!DNL Flow Service].

### Förhandskrav {#prerequisites}

För att kunna ansluta [!DNL Pinterest Ads] till Experience Platform måste du ange värden för följande anslutningsegenskaper:

* [!DNL Pinterest] `accessToken`.
* [!DNL Pinterest] `adAccountId`.
* Ett av [!DNL Pinterest] `campaign`, `adGroup` eller `ad` ID:n efter behov.

Mer information om de här anslutningsegenskaperna finns i [[!DNL Pinterest Ads] översikten](../../../../connectors/advertising/pinterest-ads.md#prerequisites).

## Anslut [!DNL Pinterest Ads] till plattformen med API:t [!DNL Flow Service] {#connect-platform-to-flow-api}

Följande visar vilka steg som ska vidtas för att ansluta [!DNL Pinterest Ads] till Experience Platform.

### Skapa en basanslutning {#base-connection}

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina [!DNL Pinterest Ads] autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Pinterest Ads]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Pinterest Ads",
      "description": "Create a live inbound connection to your Pinterest Ads instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "f82aae23-91e7-4884-b25f-2d2159d841fd",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {  
              "accessToken": "{PINTEREST_ACCESS_TOKEN}"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på din basanslutning. Kontrollera att namnet på din basanslutning är beskrivande, eftersom du kan använda detta för att söka efter information om din basanslutning. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din basanslutning. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för källan. Detta ID kan hämtas när källan har registrerats och godkänts via API:t [!DNL Flow Service]. |
| `auth.specName` | Autentiseringstypen som du använder för att autentisera källan till plattformen. |
| `auth.params.accessToken` | Innehåller det [!DNL Pinterest]-åtkomsttoken-värde som krävs för att autentisera källan. |

**Svar**

Ett svar returnerar den nyskapade basanslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att undersöka källans filstruktur och innehåll i nästa steg.

```json
{
    "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
    "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### Utforska din källa {#explore}

Med det grundläggande anslutnings-ID som du skapade i det föregående steget kan du utforska filer och kataloger genom att utföra GET-begäranden.
Använd följande anrop för att hitta sökvägen till filen som du vill hämta till plattformen:

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
| `{SOURCE_PARAMS}` | Definierar parametrar för källfilen som du vill hämta till plattformen. Om du vill hämta den godkända formattypen för `{SOURCE_PARAMS}` måste du koda hela `{"ad_account_id":"{PINTEREST_AD_ACCOUNT_ID}","object_ids":"{COMMA_SEPERATED_OBJECT_IDS}","object_type":"{OBJECT_TYPE}}"}`-strängen i base64. |

[!DNL Pinterest Ads] stöder flera [!DNL Pinterest] API-slutpunkter för analys. Beroende på vilken objekttyp du utnyttjar den begäran som ska skickas anges nedan:

**Begäran**

>[!BEGINTABS]

>[!TAB Kampanjer]

För [!DNL Pinterest Ads] skickas värdet för `{SOURCE_PARAMS}` som `{"ad_account_id":"123456789000","object_ids":"000123456789","object_type":"campaigns"}` när API:t för Campaign Analytics används. När den kodas i base64 är den lika med `YHsiYWRfYWNjb3VudF9pZCI6IjEyMzQ1Njc4OTAwMCIsIm9iamVjdF9pZHMiOiIwMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImNhbXBhaWducyJ9` enligt nedan.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=YHsiYWRfYWNjb3VudF9pZCI6IjEyMzQ1Njc4OTAwMCIsIm9iamVjdF9pZHMiOiIwMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImNhbXBhaWducyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB Annonsgrupper]

För [!DNL Pinterest Ads] skickas värdet för `{SOURCE_PARAMS}` som `{"ad_account_id":"123456789000","object_ids":"000123456789,100123456789","object_type":"ad_groups"}` när API:t för annonsgruppsanalys används. När den kodas i base64 är den lika med `eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjAwMDEyMzQ1Njc4OSwxMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImFkX2dyb3VwcyJ9`, vilket visas nedan.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjAwMDEyMzQ1Njc4OSwxMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImFkX2dyb3VwcyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB Ads]

För [!DNL Pinterest Ads] skickas värdet för `{SOURCE_PARAMS}` som `{"ad_account_id":"123456789000","object_ids":"687247811001,687247811002,687247815005,687247834765","object_type":"ads"}` när API:t för annonsanalys används. När den kodas i base64 är den lika med `eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjY4NzI0NzgxMTAwMSw2ODcyNDc4MTEwMDIsNjg3MjQ3ODE1MDA1LDY4NzI0NzgzNDc2NSIsIm9iamVjdF90eXBlIjoiYWRzIn0=`, vilket visas nedan.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjY4NzI0NzgxMTAwMSw2ODcyNDc4MTEwMDIsNjg3MjQ3ODE1MDA1LDY4NzI0NzgzNDc2NSIsIm9iamVjdF90eXBlIjoiYWRzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**Svar**

>[!NOTE]
>
>Vissa poster har trunkerats för att ge en bättre presentation.

>[!BEGINTABS]

>[!TAB Kampanjer]

Ett lyckat svar returnerar datastrukturen för motsvarande [!DNL Pinterest Ads]-API som du anropade.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "string"
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "REPIN_1": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 355,
            "DATE": "2023-02-10",
            "TOTAL_CLICKTHROUGH": 7,
            "CAMPAIGN_ID": "000123456789",
            "TOTAL_IMPRESSION_USER": 324,
            "REPIN_1": 2,
            "TOTAL_ENGAGEMENT": 10,
            "ENGAGEMENT_RATE": 0.029940119760479042,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "ECTR": 0.020833333333333332
        }
    ]
}
```

>[!TAB Annonsgrupper]

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "AD_GROUP_ID": {
                "type": "string"
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 164,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 2,
            "CAMPAIGN_ID": 626747962992,
            "TOTAL_IMPRESSION_USER": 149,
            "TOTAL_ENGAGEMENT": 3,
            "ENGAGEMENT_RATE": 0.01910828025477707,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": "000123456789",
            "ECTR": 0.012658227848101266
        },
        {
            "IMPRESSION_1_GROSS": 177,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 5,
            "CAMPAIGN_ID": 626747962992,
            "TOTAL_IMPRESSION_USER": 167,
            "TOTAL_ENGAGEMENT": 5,
            "ENGAGEMENT_RATE": 0.028901734104046242,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": "100123456789",
            "ECTR": 0.028901734104046242
        }
    ]
}
```

>[!TAB Ads]

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "AD_ID": {
                "type": "string"
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "AD_GROUP_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 146,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 2,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 132,
            "AD_ID": "687247811001",
            "TOTAL_ENGAGEMENT": 3,
            "ENGAGEMENT_RATE": 0.02158273381294964,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 000123456789,
            "ECTR": 0.014285714285714285
        },
        {
            "IMPRESSION_1_GROSS": 19,
            "DATE": "2023-02-13",
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 18,
            "AD_ID": "687247811002",
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 000123456789
        },
        {
            "IMPRESSION_1_GROSS": 63,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 1,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 57,
            "AD_ID": "687247815005",
            "TOTAL_ENGAGEMENT": 1,
            "ENGAGEMENT_RATE": 0.016129032258064516,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 100123456789,
            "ECTR": 0.016129032258064516
        },
        {
            "IMPRESSION_1_GROSS": 116,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 4,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 115,
            "AD_ID": "687247834765",
            "TOTAL_ENGAGEMENT": 4,
            "ENGAGEMENT_RATE": 0.035398230088495575,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 100123456789,
            "ECTR": 0.035398230088495575
        }
    ]
}
```

>[!ENDTABS]

### Skapa en källanslutning {#source-connection}

Du kan skapa en källanslutning genom att göra en POST-förfrågan till API:t [!DNL Flow Service]. En källanslutning består av ett grundläggande anslutnings-ID, en sökväg till källdatafilen och ett anslutnings-spec-ID.

**API-format**

```https
POST /sourceConnections
```

**Begäran**

Källan [!DNL Pinterest Ads] stöder flera [!DNL Pinterest] API-slutpunkter för analys. Beroende på vilken objekttyp du använder skapar följande begäran en källanslutning:

>[!BEGINTABS]

>[!TAB Kampanjer]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "campaigns",
            "object_ids": "2680074532641"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för [!DNL Pinterest Ads]. Detta ID genererades i ett tidigare steg. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar källan. |
| `data.format` | Formatet på de [!DNL Pinterest Ads]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`. |
| `params.object_type` | Eftersom API-slutpunkten [!DNL Pinterest] för kampanjanalys krävs blir värdet `campaigns`. |
| `params.object_ids` | Kommaavgränsad lista med [!DNL Pinterest] kampanj-ID:n. |

>[!TAB Annonsgrupper]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "ad_groups",
            "object_ids": "2680074532641,2680074533547"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för [!DNL Pinterest Ads]. Detta ID genererades i ett tidigare steg. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar källan. |
| `data.format` | Formatet på de [!DNL Pinterest Ads]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`. |
| `params.object_type` | Eftersom API-slutpunkten för [!DNL Pinterest] Ad Groups Analytics krävs blir värdet `ad_groups`. |
| `params.object_ids` | Kommaseparerad lista över [!DNL Pinterest] annonsgrupps-ID:n. |

>[!TAB Ads]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "ads",
            "object_ids": "687247811001,687247811002,687247815005,687247834765"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för [!DNL Pinterest Ads]. Detta ID genererades i ett tidigare steg. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar källan. |
| `data.format` | Formatet på de [!DNL Pinterest Ads]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`. |
| `params.object_type` | Eftersom API-slutpunkten [!DNL Pinterest] för annonsanalys krävs blir värdet `ads`. |
| `params.object_ids` | Kommaavgränsad lista med [!DNL Pinterest] annons-ID:n. |

>[!ENDTABS]

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

En måldatamängd kan skapas genom att utföra en POST-begäran till [katalogtjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), som anger målschemats ID i nyttolasten.

Detaljerade steg om hur du skapar en måldatauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:t](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inmatade data ska lagras. Om du vill skapa en målanslutning måste du ange det fasta anslutningsspecifikations-ID som motsvarar datasjön. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Nu har du de unika identifierarna ett målschema, en måldatamängd och ett anslutningsspec-ID till datasjön. Med hjälp av dessa identifierare kan du skapa en målanslutning med API:t [!DNL Flow Service] för att ange den datauppsättning som ska innehålla inkommande källdata.

**API-format**

```https
POST /targetConnections
```

**Begäran**

Följande begäran skapar en målanslutning för [!DNL Pinterest Ads]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Target Connection",
        "description": "Pinterest Ads Target Connection",
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
| `data.format` | Formatet för de [!DNL Pinterest Ads]-data som du vill hämta till plattformen. |
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
            "sourceType": "ATTRIBUTE",
            "source": "CAMPAIGN_ID",
            "destination": "_extconndev.ID_CAMPAIGN"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "CAMPAIGN_NAME",
            "destination": "_extconndev.NAME_CAMPAIGN"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "AD_GROUP_ID",
            "destination": "_extconndev.AD_GROUP_ID"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "AD_ID",
            "destination": "_extconndev.AD_ID"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "DATE",
            "destination": "_extconndev.DATE"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "ECTR",
            "destination": "_extconndev.ECTR"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "ENGAGEMENT_RATE",
            "destination": "_extconndev. ENGAGEMENT_RATE"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "IMPRESSION_1_GROSS",
            "destination": "_extconndev. IMPRESSION_1_GROSS"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "REPIN_1",
            "destination": "_extconndev. REPIN_1"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_CLICKTHROUGH",
            "destination": "_extconndev. TOTAL_CLICKTHROUGH"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_ENGAGEMENT",
            "destination": "_extconndev. TOTAL_ENGAGEMENT"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_IMPRESSION_USER",
            "destination": "_extconndev. TOTAL_IMPRESSION_USER"
            }
        ],
        "outputSchema": {
            "schemaRef": {
            "id": "{{schemaId}}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `outputSchema.schemaRef.id` | ID:t för [mål-XDM-schemat](#target-schema) genererades i ett tidigare steg. |
| `mappings.sourceType` | Källattributtypen som mappas. |
| `mappings.source` | Källattributet som måste mappas till en mål-XDM-sökväg. |
| `mappings.destination` | Mål-XDM-sökvägen dit källattributet mappas. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade mappningen inklusive dess unika identifierare (`id`). Detta värde krävs i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "059c69f7207b4d7e9b48c47e2fd966a6",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Skapa ett flöde {#flow}

Det sista steget mot att överföra data från [!DNL Pinterest Ads] till plattformen är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

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
        "name": "Pinterest Ads dataflow",
        "description": "Pinterest Ads dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3"
        ],
        "targetConnectionIds": [
            "6b137bf6-d2a0-48c8-914b-d50f4942eb85"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "059c69f7207b4d7e9b48c47e2fd966a6",
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

## Bilaga {#appendix}

Följande avsnitt innehåller information om hur du övervakar, uppdaterar och tar bort dataflödet.

### Övervaka dataflödet {#monitor-dataflow}

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om flödeskörningar, slutförandestatus och fel. Fullständiga API-exempel finns i handboken om [att övervaka källans dataflöden med API:t](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Uppdatera ditt dataflöde {#update-dataflow}

Uppdatera informationen om dataflödet, till exempel namn och beskrivning, samt körningsschema och associerade mappningsuppsättningar genom att göra en PATCH-begäran till `/flows`-slutpunkten i [!DNL Flow Service]-API:t, samtidigt som du anger ID:t för dataflödet. När du gör en PATCH-begäran måste du ange dataflödets unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken om att [uppdatera källkodsdataflöden med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Uppdatera ditt konto {#update-account}

Uppdatera namn, beskrivning och autentiseringsuppgifter för källkontot genom att utföra en PATCH-begäran till [!DNL Flow Service]-API:t och ange ditt grundläggande anslutnings-ID som en frågeparameter. När du gör en PATCH-begäran måste du ange källkontots unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken [Uppdatera ditt källkonto med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Ta bort ditt dataflöde {#delete-dataflow}

Ta bort dataflödet genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange ID:t för det dataflöde som du vill ta bort som en del av frågeparametern. Fullständiga API-exempel finns i guiden om att [ta bort dataflöden med API:t](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Ta bort ditt konto {#delete-account}

Ta bort ditt konto genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange det grundläggande anslutnings-ID:t för kontot som du vill ta bort. Fullständiga API-exempel finns i guiden om att [ta bort ditt källkonto med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
