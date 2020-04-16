---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Samla in molnlagringsdata via källanslutningar och API:er
topic: overview
translation-type: tm+mt
source-git-commit: 4309d668acf43a237648b405973ebd0701b6f977

---


# Samla in molnlagringsdata via källanslutningar och API:er

I den här självstudiekursen beskrivs stegen för att hämta data från en tredjeparts molnlagring och föra in dem på plattformen via källanslutningar och API:er.

## Komma igång

I den här självstudiekursen måste du ha tillgång till ett molnlagringsutrymme från tredje part via en giltig basanslutning och information om filen som du vill hämta till plattformen, inklusive filens sökväg och struktur. Om du inte har den här informationen kan du gå till självstudiekursen om hur du [utforskar molnlagring från tredje part med API:t](../explore/cloud-storage.md) för Flow Service innan du försöker med den här självstudiekursen.

Den här självstudien kräver också att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Utvecklarhandbok](../../../../xdm/api/getting-started.md)för schemaregister: Innehåller viktig information som du behöver känna till för att kunna utföra anrop till API:t för schemaregister. Detta inkluderar ditt `{TENANT_ID}`, konceptet med&quot;behållare&quot; och de rubriker som krävs för att göra förfrågningar (med särskild uppmärksamhet på rubriken Godkänn och dess möjliga värden).
* [Katalogtjänst](../../../../catalog/home.md): Katalog är ett system för registrering av dataplats och datalänkning inom Experience Platform.
* [Batchförtäring](../../../../ingestion/batch-ingestion/overview.md): Med API:t för gruppinmatning kan du importera data till Experience Platform som gruppfiler.
* [Sandlådor](../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till ett molnlagringsutrymme med API:t för Flow Service.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör Flow Service, isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Skapa en ad hoc XDM-klass och ett schema

För att externa data ska kunna hämtas till plattformen via källanslutningar måste en ad hoc XDM-klass och ett schema skapas för råkälldata.

Om du vill skapa en ad hoc-klass och ett ad hoc-schema följer du stegen som beskrivs i [ad hoc-schemautstudiekursen](../../../../xdm/tutorials/ad-hoc.md). När du skapar en ad hoc-klass måste alla fält i källdata beskrivas i begärandetexten.

Fortsätt att följa stegen som beskrivs i utvecklarhandboken tills du har skapat ett ad hoc-schema. Hämta och lagra den unika identifieraren (`$id`) för ad hoc-schemat och fortsätt sedan till nästa steg i kursen.

## Skapa en källanslutning {#source}

När ett ad hoc-XDM-schema har skapats kan en källanslutning skapas med hjälp av en POST-begäran till API:t för Flow Service. En källanslutning består av en basanslutning, en källdatafil och en referens till schemat som beskriver källdata.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection for a cloud storage",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "description": "Source Connection to ingest data.csv",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/140c03de81b959db95879033945cfd4c",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/some/path/data.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `baseConnectionId` | ID:t för en basanslutning för ett molnlagringssystem. |
| `data.schema.id` | ID för ad hoc-XDM-schemat. |
| `params.path` | Källfilens sökväg. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Lagra det här värdet som det krävs i senare steg för att skapa en målanslutning.

```json
{
    "id": "9a603322-19d2-4de9-89c6-c98bd54eb184"
}
```

## Skapa ett mål-XDM-schema {#target}

I tidigare steg skapades ett ad hoc-XDM-schema för att strukturera källdata. För att källdata ska kunna användas i Platform måste ett målschema också skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en plattformsdatauppsättning där källdata finns.

Om du föredrar att använda användargränssnittet i Experience Platform finns det stegvisa instruktioner [i](../../../../xdm/tutorials/create-schema-ui.md) schemaredigeraren för att utföra liknande åtgärder i schemaredigeraren.

**API-format**

```http
POST /schemaregistry/tenant/schemas
```

**Begäran**

Följande exempelbegäran skapar ett XDM-schema som utökar klassen för enskild XDM-profil.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Target schema for cloud storage source connector",
        "description": "",
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

Ett lyckat svar returnerar information om det nyligen skapade schemat inklusive dess unika identifierare (`$id`). Lagra det här ID:t så som det behövs i senare steg för att skapa en måldatauppsättning, mappning och ett dataflöde.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
    "meta:altId": "{TENANT_ID}.schemas.417a33eg81a221bd10495920574gfa2d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for cloud storage source connector",
    "description": "",
    "type": "object",
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
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "meta:containerId": "tenant",
    "meta:registryMetadata": {
        "eTag": "6m/FrIlXYU2+yH6idbcmQhKSlMo="
    }
}
```

## Skapa en måldatauppsättning

En måldatauppsättning kan skapas genom att en POST-begäran till katalogtjänstens API utförs, med målschemats ID i nyttolasten.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `schemaRef.id` | ID:t för mål-XDM-schemat. |

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för den nya datauppsättningen i formatet `"@/datasets/{DATASET_ID}"`. Datauppsättnings-ID är en skrivskyddad, systemgenererad sträng som används för att referera till datauppsättningen i API-anrop. Lagra måldatauppsättnings-ID som det krävs i senare steg för att skapa en målanslutning och ett dataflöde.

```json
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Skapa en datauppsättningsbasanslutning

För att kunna importera externa data till plattformen måste en Experience Platform-datauppsättningsbaserad anslutning först hämtas.

Om du vill skapa en datauppsättningsbasanslutning följer du de steg som beskrivs i självstudiekursen för [datauppsättningsbasanslutningar](../create-dataset-base-connection.md).

Fortsätt att följa stegen som beskrivs i utvecklarhandboken tills du har skapat en datauppsättningsbasanslutning. Hämta och lagra den unika identifieraren (`$id`) och fortsätt att använda den som bas-anslutnings-ID i nästa steg för att skapa en målanslutning.

## Skapa en målanslutning

Du har nu unika identifierare för en datauppsättningsbasanslutning, ett målschema och en måldatauppsättning. Med dessa identifierare kan du skapa en målanslutning med API:t för Flow Service för att ange den datauppsättning som ska innehålla inkommande källdata.

**API-format**

```http
POST /targetConnections
```

**Begäran**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection",
        "description": "Target Connection for cloud storage data",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5c8c3c555033b814b69f947f"
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `baseConnectionId` | ID:t för datauppsättningsbasanslutningen. |
| `data.schema.id` | The `$id` of the target XDM schema. |
| `params.dataSetId` | ID för måldatauppsättningen. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för ditt molnlagringsutrymme. |

>[!NOTE] När du skapar en målanslutning måste du se till att du använder basanslutningsvärdet för datasjön för basanslutningen `id` i stället för basanslutningen för källkopplingen från tredje part.

**Svar**

Ett lyckat svar returnerar den nya målanslutningens unika identifierare (`id`). Lagra det här värdet som det behövs i senare steg.

```json
{
    "id": "4ee890c7-519c-4291-bd20-d64186b62da8",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste de först mappas till målschemat som måldatamängden följer. Detta uppnås genom att utföra en POST-begäran till konverteringstjänsten med datamappningar definierade i nyttolasten för begäran.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
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
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Phone",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "Email",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
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
| `xdmSchema` | ID:t för mål-XDM-schemat. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade mappningen inklusive dess unika identifierare (`id`). Lagra det här värdet som det krävs i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
    "version": 1,
    "createdDate": 1568047685000,
    "modifiedDate": 1568047703000,
    "inputSchemaRef": {
        "id": null,
        "contentType": null
    },
    "outputSchemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "contentType": "1.0"
    },
    "mappings": [
        {
            "id": "7bbea5c0f0ef498aa20aa2e2e5c22290",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "Id",
            "destination": "_id",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "Id",
            "destinationXdmPath": "_id"
        },
        {
            "id": "def7fd7db2244f618d072e8315f59c05",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "FirstName",
            "destination": "person.name.firstName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "FirstName",
            "destinationXdmPath": "person.name.firstName"
        },
        {
            "id": "e974986b28c74ed8837570f421d0b2f4",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "LastName",
            "destination": "person.name.lastName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "LastName",
            "destinationXdmPath": "person.name.lastName"
        }
    ],
    "status": "PUBLISHED",
    "xdmVersion": "1.0",
    "schemaRef": {
        "id": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## Söka efter dataflödesspecifikationer {#specs}

Ett dataflöde ansvarar för att samla in data från källor och föra in dem i plattformen. För att kunna skapa ett dataflöde måste du först få de dataflödesspecifikationer som ansvarar för att samla in molnlagringsdata.

**API-format**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar detaljerna om dataflödesspecifikationen som ansvarar för att överföra data från ditt molnlagringsutrymme till plattformen. Lagra värdet för `id` fältet som det är nödvändigt i nästa steg för att skapa ett nytt dataflöde.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
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
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            }
        }
    ]
}
```

## Skapa ett dataflöde

Det sista steget mot att samla in molnlagringsdata är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

* [Källanslutnings-ID](#source)
* [Målanslutnings-ID](#target)
* [Mappnings-ID](#mapping)
* [ID för dataflödesspecifikation](#specs)

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataflow between cloud storage and Platform",
        "description": "collecting data.csv",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "9a603322-19d2-4de9-89c6-c98bd54eb184"
        ],
        "targetConnectionIds": [
            "4ee890c7-519c-4291-bd20-d64186b62da8"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "mode": "append"
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `flowSpec.id` | ID för dataflödesspecifikation |
| `sourceConnectionIds` | Källanslutnings-ID |
| `targetConnectionIds` | Målanslutnings-ID |
| `transformations.params.mappingId` | Mappnings-ID |

**Svar**

Ett godkänt svar returnerar ID:t (`id`) för det nya dataflödet.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en källanslutning för att samla in data från din molnlagring på schemalagd basis. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan, t.ex. kundprofil i realtid och datavetenskapen. Mer information finns i följande dokument:

* [Översikt över kundprofiler i realtid](../../../../profile/home.md)
* [Översikt över arbetsytan Datavetenskap](../../../../data-science-workspace/home.md)