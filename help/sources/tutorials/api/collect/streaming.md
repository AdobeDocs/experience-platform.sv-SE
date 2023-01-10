---
keywords: Experience Platform;hem;populära ämnen;molnlagringsdata;strömmande data;strömning
solution: Experience Platform
title: Skapa ett direktuppspelat dataflöde för rådata med API:t för flödestjänsten
type: Tutorial
description: Den här självstudiekursen beskriver stegen för att hämta direktuppspelningsdata och föra in dem på plattformen med hjälp av källanslutningar och API:er.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# Skapa ett direktuppspelat dataflöde för rådata med [!DNL Flow Service] API

I den här självstudiekursen beskrivs stegen för att hämta rådata från en direktuppspelningskälla och överföra dem till Experience Platform med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Utvecklarhandbok för schemaregister](../../../../xdm/api/getting-started.md): Innehåller viktig information som du behöver känna till för att kunna utföra anrop till API:t för schemaregister. Detta inkluderar `{TENANT_ID}`, begreppet&quot;behållare&quot; och de rubriker som krävs för att göra en begäran (med särskild uppmärksamhet på rubriken Godkänn och dess möjliga värden).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Katalog är systemet för registrering av dataplatser och -länkar inom Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): Direktuppspelning för Platform ger användare en metod för att skicka data från klient- och serverenheter till Experience Platform i realtid.
- [Sandlådor](../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../landing/api-guide.md).

### Skapa en källanslutning {#source}

Den här självstudien kräver även att du har ett giltigt källanslutnings-ID för en direktuppspelningskontakt. Om du inte har den här informationen kan du titta i följande självstudiekurser om hur du skapar en direktuppspelningskällanslutning innan du försöker med den här självstudiekursen:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en plattformsdatauppsättning där källdata finns. Detta mål-XDM-schema utökar även XDM [!DNL Individual Profile] klassen.

Om du vill skapa ett mål-XDM-schema skickar du en POST till `/schemas` slutpunkt för [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**API-format**

```http
POST /tenant/schemas
```

**Begäran**

I följande exempelbegäran skapas ett XDM-schema som utökar XDM [!DNL Individual Profile] klassen.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**Svar**

Ett lyckat svar returnerar information om det nyligen skapade schemat inklusive dess unika identifierare (`$id`). Detta ID krävs i senare steg för att skapa en måldatauppsättning, mappning och ett dataflöde.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Skapa en måldatauppsättning

Med ett mål-XDM-schema skapat och dess unika `$id` du kan nu skapa en måldatauppsättning som innehåller dina källdata. Om du vill skapa en måldatauppsättning skickar du en POST till `dataSets` slutpunkt för [Katalogtjänstens API](https://www.adobe.io/experience-platform-apis/references/catalog/), samtidigt som ID:t för målschemat anges i nyttolasten.

**API-format**

```http
POST /catalog/dataSets
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på datauppsättningen som ska skapas. |
| `schemaRef.id` | URI `$id` för XDM-schemat kommer datauppsättningen att baseras på. |
| `schemaRef.contentType` | Schemats version. Värdet måste anges till `application/vnd.adobe.xed-full-notext+json;version=1`, som returnerar den senaste delversionen av schemat. Se avsnittet om [schemaversion](../../../../xdm/api/getting-started.md#versioning) i XDM API-guiden för mer information. |

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för den nya datauppsättningen i formatet `"@/datasets/{DATASET_ID}"`. Datauppsättnings-ID är en skrivskyddad, systemgenererad sträng som används för att referera till datauppsättningen i API-anrop. Måldatauppsättnings-ID krävs i senare steg för att skapa en målanslutning och ett dataflöde.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Skapa en målanslutning {#target-connection}

Målanslutningar skapar och hanterar en målanslutning till plattformen eller någon plats där de överförda data landas. Målanslutningar innehåller information om datamål, dataformat och det anslutnings-ID som krävs för att skapa ett dataflöde. Målanslutningens instanser är specifika för en klientorganisation och IMS-organisation.

Om du vill skapa en målanslutning skickar du en POST till `/targetConnections` slutpunkt för [!DNL Flow Service] API. Som en del av begäran måste du ange dataformatet, `dataSetId` hämtat i föregående steg och det fasta ID för anslutningsspecifikation som är knutet till [!DNL Data Lake]. Detta ID är `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API-format**

```http
POST /targetConnections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `connectionSpec.id` | Anslutningsspecifikations-ID som används för att ansluta till [!DNL Data Lake]. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Det angivna formatet för de data som du hämtar till [!DNL Data Lake]. |
| `params.dataSetId` | ID för måldatauppsättningen som hämtades i föregående steg. |

**Svar**

Ett godkänt svar returnerar den nya målanslutningens unika identifierare (`id`). Detta ID krävs i senare steg.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste den först mappas till målschemat som måldatamängden följer.

Skapa en mappningsuppsättning genom att göra en POST-förfrågan till `mappingSets` slutpunkt för [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) när du tillhandahöll ditt mål-XDM-schema `$id` och information om de mappningsuppsättningar som du vill skapa.

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
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
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
| `xdmSchema` | The `$id` av mål-XDM-schemat. |

**Svar**

Ett godkänt svar returnerar information om den nyligen skapade mappningen inklusive dess unika identifierare (`id`). Detta ID krävs i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Hämta en lista med dataflödesspecifikationer {#specs}

Ett dataflöde ansvarar för att samla in data från källor och föra in dem i plattformen. För att kunna skapa ett dataflöde måste du först få dataflödesspecifikationerna genom att göra en GET-förfrågan till [!DNL Flow Service] API.

**API-format**

```http
GET /flowSpecs
```

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med dataflödesspecifikationer. Det ID för dataflödesspecifikation som du behöver hämta för att skapa ett dataflöde med något av [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], eller  [!DNL Google PubSub], is `d69717ba-71b4-4313-b654-49f9cf126d7a`.

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        },
    ]
}
```

## Skapa ett dataflöde

Det sista steget mot att samla in strömmande data är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

- [Källanslutnings-ID](#source)
- [Målanslutnings-ID](#target)
- [Mappnings-ID](#mapping)
- [ID för dataflödesspecifikation](#specs)

Ett dataflöde ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en begäran om POST samtidigt som du anger de tidigare angivna värdena i nyttolasten.

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
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `flowSpec.id` | The [flödesspec-ID](#specs) hämtat i föregående steg. |
| `sourceConnectionIds` | The [källanslutnings-ID](#source) hämtat i ett tidigare steg. |
| `targetConnectionIds` | The [målanslutnings-ID](#target-connection) hämtat i ett tidigare steg. |
| `transformations.params.mappingId` | The [mappnings-ID](#mapping) hämtat i ett tidigare steg. |

**Svar**

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att samla in strömmande data från din strömningskontakt. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan som [!DNL Real-Time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../../../data-science-workspace/home.md)
