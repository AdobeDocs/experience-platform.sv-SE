---
keywords: Experience Platform;hem;populära ämnen;direktuppspelningsanslutning;skapa direktuppspelningsanslutning;api guide;självstudiekurs;skapa en direktuppspelningsanslutning;direktuppspelningsproblem;intag;
title: Skapa en HTTP API Streaming Connection med API:t för Flow Service
description: I den här självstudiekursen beskrivs hur du skapar en direktuppspelningsanslutning med hjälp av HTTP API-källan för både raw- och XDM-data med API:t för Flow Service
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 0%

---


# Skapa en HTTP API-direktuppspelningsanslutning med API:t [!DNL Flow Service]

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) för att vägleda dig genom stegen för att skapa en direktuppspelningsanslutning med API:t [!DNL Flow Service].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar upplevelsedata med.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du vill skapa en direktuppspelningsanslutning måste du dessutom ha ett mål-XDM-schema och en datauppsättning. Om du vill lära dig hur du skapar dessa läser du självstudiekursen [om dataströmmar ](../../../../../ingestion/tutorials/streaming-record-data.md) eller självstudiekursen [om dataströmmar i tidsserier](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning anger källan och innehåller den information som krävs för att göra flödet kompatibelt med API:er för direktuppspelning. När du skapar en basanslutning kan du välja att skapa en icke-autentiserad och autentiserad anslutning.

### Icke-autentiserad anslutning

Icke-autentiserade anslutningar är den standarddirektuppspelningsanslutning som du kan skapa när du vill strömma data till plattformen.

Om du vill skapa en oautentiserad basanslutning skickar du en POST till slutpunkten `/connections` samtidigt som du anger ett namn för anslutningen, datatypen och ID:t för HTTP API-anslutningsspecifikationen. Detta ID är `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**API-format**

```http
POST /flowservice/connections
```

**Begäran**

Följande begäran skapar en basanslutning för HTTP API.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB Raw-data]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på din basanslutning. Kontrollera att namnet är beskrivande eftersom du kan använda det för att söka efter information om din basanslutning. |
| `description` | (Valfritt) En egenskap som du kan inkludera för att få mer information om din basanslutning. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som motsvarar HTTP API. Detta ID är `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | Datatypen för direktuppspelningsanslutningen. Värden som stöds är: `xdm` och `raw`. |
| `auth.params.name` | Namnet på den direktuppspelningsanslutning som du vill skapa. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | `id` för din nya basanslutning. |
| `etag` | En identifierare som är tilldelad anslutningen och som anger versionen av basanslutningen. |

### Autentiserad anslutning

Autentiserade anslutningar bör användas när du behöver skilja mellan poster som kommer från betrodda och ej betrodda källor. Användare som vill skicka information med personligt identifierbar information (PII) bör skapa en autentiserad anslutning vid direktuppspelning av information till plattformen.

Om du vill skapa en autentiserad basanslutning måste du ta med parametern `authenticationRequired` i din begäran och ange dess värde som `true`. Under det här steget kan du även ange ett käll-ID för din autentiserade basanslutning. Den här parametern är valfri och kommer att använda samma värde som attributet `name`, om det inte anges.


**API-format**

```http
POST /flowservice/connections
```

**Begäran**

Följande begäran skapar en autentiserad basanslutning för HTTP API.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB Raw-data]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.sourceId` | En ytterligare identifierare som kan användas när en autentiserad basanslutning skapas. Den här parametern är valfri och kommer att använda samma värde som attributet `name`, om det inte anges. |
| `auth.params.authenticationRequired` | Den här parametern anger om direktuppspelningsanslutningen kräver autentisering eller inte. Om `authenticationRequired` är inställt på `true` måste autentisering anges för direktuppspelningsanslutningen. Om `authenticationRequired` är inställt på `false` krävs ingen autentisering. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## Hämta URL för direktuppspelningsslutpunkt

När du har skapat basanslutningen kan du nu hämta URL:en för direktuppspelningsslutpunkten.

**API-format**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Värdet `id` för anslutningen som du skapade tidigare. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den begärda anslutningen. URL:en för direktuppspelningsslutpunkten skapas automatiskt med anslutningen och kan hämtas med värdet `inletUrl`.

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## Skapa en källanslutning {#source}

Om du vill skapa en källanslutning skickar du en POST till slutpunkten `/sourceConnections` samtidigt som du anger ditt grundläggande anslutnings-ID.

**API-format**

```http
POST /flowservice/sourceConnections
```

**Begäran**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "connectionSpec": {
          "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
          "version": "1.0"
      }
    }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med detaljerad information om den nyligen skapade källanslutningen, inklusive dess unika identifierare (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en plattformsdatauppsättning där källdata finns.

Ett mål-XDM-schema kan skapas genom att utföra en POST-begäran till [schemats register-API ](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Detaljerade steg om hur du skapar ett mål-XDM-schema finns i självstudiekursen [Skapa ett schema med API:t](../../../../../xdm/api/schemas.md).

### Skapa en måldatauppsättning {#target-dataset}

En måldatamängd kan skapas genom att utföra en POST-begäran till [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), som anger målschemats ID i nyttolasten.

Detaljerade steg om hur du skapar en måldatauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:t](../../../../../catalog/api/create-dataset.md).

## Skapa en målanslutning {#target}

En målanslutning representerar anslutningen till målet där inkapslade data kommer in. Om du vill skapa en målanslutning skickar du en POST till `/targetConnections` samtidigt som du anger ID:n för måldatauppsättningen och XDM-målschemat. Under det här steget måste du även ange data Lake Connection specification ID. Detta ID är `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API-format**

```http
POST /flowservice/targetConnections
```

**Begäran**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om den nya målanslutningen, inklusive dess unika identifierare (`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste den först mappas till målschemat som måldatamängden följer.

Om du vill skapa en mappningsuppsättning skickar du en POST till `mappingSets`-slutpunkten för [[!DNL Data Prep]  API](https://developer.adobe.com/experience-platform-apis/references/data-prep/) samtidigt som du anger ditt mål-XDM-schema `$id` och information om de mappningsuppsättningar du vill skapa.

**API-format**

```http
POST /mappingSets
```

**Begäran**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `xdmSchema` | `$id` för mål-XDM-schemat. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade mappningen inklusive dess unika identifierare (`id`). Detta ID krävs i ett senare steg för att skapa ett dataflöde.

```json
{
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

## Skapa ett dataflöde

När käll- och målanslutningarna har skapats kan du nu skapa ett dataflöde. Dataflödet ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en begäran om POST till slutpunkten `/flows`.

**API-format**

```http
POST /flows
```

**Begäran**

>[!BEGINTABS]

>[!TAB XDM]

Följande begäran skapar ett direktuppspelat dataflöde för XDM-data.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB RAW]

Följande begäran skapar ett direktuppspelat dataflöde för rådata.

När du skapar ett dataflöde med omformningar kan parametern `name` inte ändras. Värdet måste alltid anges till `Mapping`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på dataflödet. Kontrollera att namnet på dataflödet är beskrivande, eftersom du kan använda det för att söka efter information om dataflödet. |
| `description` | (Valfritt) En egenskap som du kan inkludera för att få mer information om dataflödet. |
| `flowSpec.id` | Flödesspecifikations-ID för [!DNL HTTP API]. Om du vill skapa ett dataflöde med omformningar måste du använda `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. Använd `d8a6f005-7eaf-4153-983e-e8574508b877` om du vill skapa ett dataflöde utan omformningar. |
| `sourceConnectionIds` | [källanslutnings-ID](#source) har hämtats i ett tidigare steg. |
| `targetConnectionIds` | [målanslutnings-ID](#target) har hämtats i ett tidigare steg. |
| `transformations.params.mappingId` | [Mappnings-ID](#mapping) hämtades i ett tidigare steg. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om det nya dataflödet, inklusive dess unika identifierare (`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## Bokför data som ska importeras till plattformen {#ingest-data}

>[!NOTE]
>
>Du måste lägga till en fördröjning på minst ~5 minuter mellan att dataflödet skapas och att data hämtas. Detta gör att dataflödet kan aktiveras fullständigt innan data hämtas.

Nu när du har skapat ditt flöde kan du skicka ditt JSON-meddelande till direktuppspelningsslutpunkten som du skapade tidigare.

**API-format**

```http
POST /collection/{INLET_URL}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INLET_URL}` | URL:en för din direktuppspelande slutpunkt. Du kan hämta den här URL:en genom att göra en GET-förfrågan till slutpunkten `/connections` och samtidigt ange ditt grundläggande anslutnings-ID. |
| `{FLOW_ID}` | ID:t för HTTP API-direktuppspelningsdataflödet. Detta ID krävs för både XDM- och RAW-data. |

**Begäran**

>[!BEGINTABS]

>[!TAB Skicka XDM-data]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB Skicka Raw-data med flödes-ID som HTTP-huvud]

När du skickar rådata kan du ange ditt flödes-ID som en frågeparameter eller som en del av HTTP-huvudet. I följande exempel anges flödes-ID som HTTP-huvud.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' 
  -H 'x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB Skicka Raw-data med flödes-ID som en frågeparameter]

När du skickar rådata kan du ange ditt flödes-ID som antingen en frågeparameter eller som ett HTTP-huvud. I följande exempel anges flödes-ID som en frågeparameter.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2 \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!ENDTABS]

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nya informationen.

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID:t för den tidigare skapade direktuppspelningsanslutningen. |
| `xactionId` | En unik identifierare som genererats på serversidan för den post du just skickade. Detta ID hjälper Adobe att spåra postens livscykel via olika system och med felsökning. |
| `receivedTimeMs` | En tidsstämpel (epok i millisekunder) som visar vilken tid begäran togs emot. |


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en HTTP-direktuppspelningsanslutning, vilket gör att du kan använda direktuppspelningsslutpunkten för att importera data till plattformen. Instruktioner om hur du skapar en direktuppspelningsanslutning i användargränssnittet finns i självstudiekursen [Skapa en direktuppspelningsanslutning](../../../ui/create/streaming/http.md).

Om du vill lära dig hur du direktuppspelar data på en plattform kan du läsa självstudiekursen [om att strömma tidsseriedata](../../../../../ingestion/tutorials/streaming-time-series-data.md) eller självstudiekursen om [direktuppspelade postdata](../../../../../ingestion/tutorials/streaming-record-data.md).

## Bilaga

I det här avsnittet finns ytterligare information om hur du skapar direktuppspelningsanslutningar med API:t.

### Skicka meddelanden till en autentiserad direktuppspelningsanslutning

Om en direktuppspelningsanslutning har autentisering aktiverat måste klienten lägga till huvudet `Authorization` i sin begäran.

Om `Authorization`-huvudet inte finns, eller om en ogiltig/utgången åtkomsttoken skickas, returneras ett otillåtet HTTP 401-svar, med ett liknande svar som nedan:

**Svar**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```

