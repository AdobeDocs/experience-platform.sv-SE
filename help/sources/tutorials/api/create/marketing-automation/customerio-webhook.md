---
title: Skapa en källanslutning och ett dataflöde för Customer.io med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Customer.io med API:t för Flow Service.
badge: Beta
exl-id: 1c84d818-428f-4097-9f6f-ef0cf1a04785
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 0%

---

# Skapa en källanslutning och ett dataflöde för [!DNL Customer.io] med API:t för Flow Service

>[!NOTE]
>
>Källan [!DNL Customer.io] är i betaversion. Mer information om hur du använder betatecknade källor finns i [källöversikten](../../../../home.md#terms-and-conditions).

I följande självstudiekurs får du hjälp med att skapa en [!DNL Customer.io]-källanslutning och ett dataflöde för att skicka [[!DNL Customer.io]](https://customer.io/) händelsedata till Adobe Experience Platform med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång {#getting-started}

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Anslut [!DNL Customer.io] till Experience Platform med API:t [!DNL Flow Service] {#connect-platform-to-flow-api}

Följande beskriver de steg du måste utföra för att skapa en källanslutning och ett dataflöde för att kunna överföra [!DNL Customer.io]-händelsedata till Experience Platform.

### Skapa en källanslutning {#source-connection}

Skapa en källanslutning genom att göra en POST-begäran till API:t [!DNL Flow Service], och ange källans anslutningsspec-ID, information som namn och beskrivning samt dataformatet.

**API-format**

```https
POST /sourceConnections
```

**Begäran**

Följande begäran skapar en källanslutning för [!DNL Customer.io]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Customer.io",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for customer.io",
      "connectionSpec": {
          "id": "96479064-7b8a-4d69-b9ed-21c5683837ea",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ta med för att ange mer information om din källanslutning. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar källan. |
| `data.format` | Formatet på de [!DNL Customer.io]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
    "etag": "\"af00a717-0000-0200-0000-63ef2cbd0000\""
}
```

### Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Experience Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en Experience Platform-datauppsättning där källdata finns.

Ett mål-XDM-schema kan skapas genom att en POST-begäran till [schemats register-API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) utförs.

Detaljerade steg om hur du skapar ett mål-XDM-schema finns i självstudiekursen [Skapa ett schema med API:t](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=sv-SE#create).

### Skapa en måldatauppsättning {#target-dataset}

En måldatauppsättning kan skapas genom att en POST-begäran till [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/) utförs, med ID:t för målschemat i nyttolasten.

Detaljerade steg om hur du skapar en måldatauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:t](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=sv-SE).

### Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inmatade data ska lagras. Om du vill skapa en målanslutning måste du ange det fasta anslutningsspecifikations-ID som motsvarar datasjön. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Nu har du de unika identifierarna ett målschema, en måldatamängd och ett anslutningsspec-ID till datasjön. Med hjälp av dessa identifierare kan du skapa en målanslutning med API:t [!DNL Flow Service] för att ange den datauppsättning som ska innehålla inkommande källdata.

**API-format**

```https
POST /targetConnections
```

**Begäran**

Följande begäran skapar en målanslutning för [!DNL Customer.io]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Customer.io",
      "description": "Streaming Target Connection for Customer.io",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63ec807d3f5ce91bd2d06c65"
      }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på målanslutningen. Kontrollera att namnet på målanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om målanslutningen. |
| `description` | Ett valfritt värde som du kan inkludera för att ange mer information om målanslutningen. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar datasjön. Detta fasta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Formatet på de [!DNL Customer.io]-data som du vill importera. |
| `params.dataSetId` | Måldatauppsättnings-ID som hämtades i ett tidigare steg. |

**Svar**

Ett svar returnerar den nya målanslutningens unika identifierare (`id`). Detta ID krävs i senare steg.

```json
{
    "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
    "etag": "\"70003dff-0000-0200-0000-63ef4a090000\""
}
```

### Skapa en mappning {#mapping}

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
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.cio_id",
            "sourceAttribute": "data.identifiers.cio_id",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.email",
            "sourceAttribute": "data.identifiers.email",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.event_id0",
            "sourceAttribute": "event_id",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.metricx",
            "sourceAttribute": "metric",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.object_type1",
            "sourceAttribute": "object_type",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestampx",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        }
    ]
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
    "id": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
    "version": 0,
    "createdDate": 1676627988129,
    "modifiedDate": 1676627988129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Skapa ett flöde {#flow}

Det sista steget mot att överföra data från [!DNL Customer.io] till Experience Platform är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

* [Source-anslutnings-ID](#source-connection)
* [Målanslutnings-ID](#target-connection)
* [Mappnings-ID](#mapping)

Ett dataflöde ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en POST-begäran samtidigt som du anger de tidigare nämnda värdena i nyttolasten.

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
      "name": "Streaming Dataflow for Customer.io",
      "description": "Streaming Dataflow for Customer.io",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "133bb51f-f310-4b4a-b8b2-731aef1e223c"
      ],
      "targetConnectionIds": [
          "da8b75ad-f6ee-4991-95df-291e62936e98"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på dataflödet. Kontrollera att namnet på dataflödet är beskrivande, eftersom du kan använda det för att söka efter information om dataflödet. |
| `description` | Ett valfritt värde som du kan inkludera för att få mer information om dataflödet. |
| `flowSpec.id` | Det ID för flödesspecifikation som krävs för att skapa ett dataflöde. Detta fasta ID är: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | Motsvarande version av flödesspecifikations-ID. Standardvärdet är `1.0`. |
| `sourceConnectionIds` | [källanslutnings-ID](#source-connection) genererades i ett tidigare steg. |
| `targetConnectionIds` | [målanslutnings-ID](#target-connection) genererades i ett tidigare steg. |
| `transformations` | Den här egenskapen innehåller de olika omformningar som behövs för att dina data ska kunna användas. Den här egenskapen krävs när data som inte är XDM-kompatibla skickas till Experience Platform. |
| `transformations.name` | Det namn som tilldelats omformningen. |
| `transformations.params.mappingId` | [Mappnings-ID](#mapping) genererades i ett tidigare steg. |
| `transformations.params.mappingVersion` | Motsvarande version av mappnings-ID. Standardvärdet är `0`. |

**Svar**

Ett lyckat svar returnerar ID:t (`id`) för det nyskapade dataflödet. Du kan använda det här ID:t för att övervaka, uppdatera eller ta bort dataflödet.

```json
{
    "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
    "etag": "\"4c012103-0000-0200-0000-63ef57db0000\""
}
```

### Hämta din URL för direktuppspelningsslutpunkt {#get-streaming-endpoint-url}

När dataflödet har skapats kan du nu hämta URL:en för direktuppspelningsslutpunkten. Du kommer att använda den här slutpunkts-URL:en för att prenumerera på en webkrok så att källan kan kommunicera med Experience Platform.

Om du vill hämta URL:en för direktuppspelningsslutpunkten gör du en GET-begäran till slutpunkten `/flows` och anger ID:t för dataflödet.

**API-format**

```http
GET /flows/{FLOW_ID}
```

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om ditt dataflöde, inklusive din slutpunkts-URL, markerad som `inletUrl`. Gå till sidan [Konfigurera webkrok](../../../ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint-url) för att hämta det värde som krävs.

```json
{
    "items": [
        {
            "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
            "createdAt": 1676629979503,
            "updatedAt": 1676629985390,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Customer.io",
            "description": "Streaming Dataflow for Customer.io",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"4c01c003-0000-0200-0000-63ef57e10000\"",
            "etag": "\"4c01c003-0000-0200-0000-63ef57e10000\"",
            "sourceConnectionIds": [
                "133bb51f-f310-4b4a-b8b2-731aef1e223c"
            ],
            "targetConnectionIds": [
                "da8b75ad-f6ee-4991-95df-291e62936e98"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
                        "connectionSpec": {
                            "id": "96479064-7b8a-4d69-b9ed-21c5683837ea",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e75dcb5247eb65e7385df30270192e80b145566f52ed74d570505bd2e82463f3"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4982698b-e6b3-48c2-8dcf-040e20121fd2",
            "providerRefId": "c4726e6f-64b4-4b3b-97e3-f128ace0cc74",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            }
        }
    ]
}
```

## Bilaga {#appendix}

Följande avsnitt innehåller information om hur du övervakar, uppdaterar och tar bort dataflödet.

### Övervaka dataflödet {#monitor-dataflow}

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om flödeskörningar, slutförandestatus och fel. Fullständiga API-exempel finns i handboken om [att övervaka källans dataflöden med API:t](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html?lang=sv-SE).

### Uppdatera ditt dataflöde {#update-dataflow}

Uppdatera informationen om dataflödet, till exempel namn och beskrivning, samt körningsschema och associerade mappningsuppsättningar genom att göra en PATCH-begäran till `/flows`-slutpunkten för [!DNL Flow Service] API, samtidigt som du anger ID:t för dataflödet. När du gör en PATCH-begäran måste du ange dataflödets unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken om att [uppdatera källkodsdataflöden med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html?lang=sv-SE)

### Uppdatera ditt konto {#update-account}

Uppdatera namn, beskrivning och autentiseringsuppgifter för källkontot genom att utföra en PATCH-begäran till [!DNL Flow Service]-API:t och ange ditt grundläggande anslutnings-ID som en frågeparameter. När du gör en PATCH-begäran måste du ange källkontots unika `etag` i rubriken `If-Match`. Fullständiga API-exempel finns i handboken [Uppdatera ditt källkonto med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html?lang=sv-SE).

### Ta bort ditt dataflöde {#delete-dataflow}

Ta bort dataflödet genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange ID:t för det dataflöde som du vill ta bort som en del av frågeparametern. Fullständiga API-exempel finns i guiden om att [ta bort dataflöden med API:t](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html?lang=sv-SE).

### Ta bort ditt konto {#delete-account}

Ta bort ditt konto genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t och ange det grundläggande anslutnings-ID:t för kontot som du vill ta bort. Fullständiga API-exempel finns i guiden om att [ta bort ditt källkonto med API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html?lang=sv-SE).
