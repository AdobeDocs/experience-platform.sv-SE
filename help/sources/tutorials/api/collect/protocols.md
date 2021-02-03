---
keywords: Experience Platform;hem;populära ämnen;Samla in protokolldata;protokolldata
solution: Experience Platform
title: Samla in protokolldata via källanslutningar och API:er
topic: overview
type: Tutorial
description: Den här självstudiekursen beskriver stegen för att hämta data från ett protokollprogram och hämta dem till plattformen via källanslutningar och API:er.
translation-type: tm+mt
source-git-commit: 478c73935d674ef4eb40511cc562b27df77f58c8
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 0%

---


# Samla in protokolldata via källanslutningar och API:er

I den här självstudiekursen beskrivs stegen för att hämta data från ett tredjepartsprotokollprogram och att hämta dem till Adobe Experience Platform via källanslutningar och API:t [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Komma igång

Den här självstudien kräver att du har tillgång till ett protokollsystem via en giltig basanslutning och information om filen som du vill hämta till plattformen, inklusive tabellens sökväg och struktur. Om du inte har den här informationen kan du gå till självstudiekursen om [hur du utforskar protokollsystem med API:t för Flow Service](../explore/protocols.md) innan du provar den här självstudiekursen.

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Utvecklarhandbok](../../../../xdm/api/getting-started.md) för schemaregister: Innehåller viktig information som du behöver känna till för att kunna utföra anrop till API:t för schemaregister. Detta inkluderar din `{TENANT_ID}`, begreppet &quot;behållare&quot; och de huvuden som krävs för att göra förfrågningar (med särskild uppmärksamhet på huvudet Godkänn och dess möjliga värden).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Katalog är systemet för registrering av dataplatser och -länkar inom Experience Platform.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Med API:t för gruppinmatning kan du importera data till Experience Platform som gruppfiler.
* [Sandlådor](../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till ett protokollprogram med API:t [!DNL Flow Service].

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Skapa en källanslutning {#source}

Du kan skapa en källanslutning genom att göra en POST-förfrågan till API:t [!DNL Flow Service]. En källanslutning består av ett anslutnings-ID, en sökväg till källdatafilen och ett anslutnings-spec-ID.

Om du vill skapa en källanslutning måste du också definiera ett uppräkningsvärde för dataformatattributet.

Använd följande uppräkningsvärden för filbaserade kopplingar:

| Dataformat | Uppräkningsvärde |
| ----------- | ---------- |
| Avgränsad | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

För alla tabellbaserade anslutningar anger du värdet `tabular`.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Generic OData source connection",
        "baseConnectionId": "a5c6b647-e784-4b58-86b6-47e784ab580b",
        "description": "Generic OData source connection",
        "data": {
            "format": "tabular",
        },
        "params": {
            "tableName": "Orders",
            "columns": [
                {
                "name": "OrderID",
                "type": "integer",
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
                },
                {
                    "name": "CustomerID",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "OrderDate",
                    "type": "string",
                    "meta:xdmType": "date-time",
                    "xdm": {
                        "type": "string",
                        "format": "date-time"
                    }
                },
                {
                    "name": "ShippedDate",
                    "type": "string",
                    "meta:xdmType": "date-time",
                    "xdm": {
                        "type": "string",
                        "format": "date-time"
                    }
                }
            ]
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `baseConnectionId` | Anslutnings-ID för protokollprogrammet |
| `params.path` | Källfilens sökväg. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för protokollprogrammet. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i senare steg för att skapa en målanslutning.

```json
{
    "id": "0a768941-ddfb-499d-b689-41ddfbf99db0",
    "etag": "\"8f00753e-0000-0200-0000-5e8a547d0000\""
}
```

## Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en plattformsdatauppsättning där källdata finns. Detta mål-XDM-schema utökar även klassen XDM [!DNL Individual Profile].

Ett mål-XDM-schema kan skapas genom att utföra en POST-begäran till [API:t för schemaregister](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

**API-format**

```http
POST /tenant/schemas
```

**Begäran**

Följande exempelbegäran skapar ett XDM-schema som utökar klassen XDM [!DNL Individual Profile].

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
        "title": "Generic OData target XDM schema",
        "description": "Generic OData target XDM schema",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:altId": "_{TENANT_ID}.schemas.e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Generic OData target XDM schema",
    "type": "object",
    "description": "Generic OData target XDM schema",
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
    "imsOrg": "{IMS_ORG}",
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
        "repo:createdDate": 1586124086523,
        "repo:lastModifiedDate": 1586124086523,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "8b281c23af03ff6a8b7d8061c62d73f7bcbfa1fc7dbabebfb4d8ca77130576ca"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Skapa en måldatauppsättning

En måldatamängd kan skapas genom att utföra en POST-begäran till [katalogtjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), som anger målschemats ID i nyttolasten.

**API-format**

```http
POST /dataSets
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
        "name": "Generic OData target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `schemaRef.id` | `$id` för mål-XDM-schemat. |

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för den nya datauppsättningen i formatet `"@/datasets/{DATASET_ID}"`. Datauppsättnings-ID är en skrivskyddad, systemgenererad sträng som används för att referera till datauppsättningen i API-anrop. Lagra måldatauppsättnings-ID som det krävs i senare steg för att skapa en målanslutning och ett dataflöde.

```json
[
    "@/dataSets/5e8a55ca53662c18af37a83a"
]
```

## Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inkapslade data kommer in. Om du vill skapa en målanslutning måste du ange det fasta anslutnings-spec-ID som är associerat med datasjön. Detta anslutningsspec-ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Nu har du de unika identifierarna ett målschema, en måldatamängd och ett anslutningsspec-ID till datasjön. Med API:t [!DNL Flow Service] kan du skapa en målanslutning genom att ange dessa identifierare tillsammans med den datauppsättning som kommer att innehålla inkommande källdata.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for protocols",
        "description": "Target Connection for protocols",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            }
        },
        "params": {
            "dataSetId": "5e8a55ca53662c18af37a83a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `data.schema.id` | `$id` för mål-XDM-schemat. |
| `params.dataSetId` | ID för måldatauppsättningen. |
| `connectionSpec.id` | Anslutningens spec-ID som används för att ansluta till Data Lake. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Svar**

Ett lyckat svar returnerar den nya målanslutningens unika identifierare (`id`). Detta värde krävs i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "576d5ecf-f114-4587-ad5e-cff1144587f4",
    "etag": "\"13013506-0000-0200-0000-5e8a56d80000\""
}
```

## Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste de först mappas till målschemat som måldatamängden följer. Detta uppnås genom att utföra en begäran om POST till [API:t för konverteringstjänsten](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) med datamappningar definierade i nyttolasten för begäran.

**API-format**

```http
POST /mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "OrderID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "CustomerID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "EmployeeID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "createdByBatchID",
                "sourceAttribute": "OrderDate",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
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
    "id": "37409d3017e24a3eb4a2dc21020f7a5b",
    "version": 0,
    "createdDate": 1586124873209,
    "modifiedDate": 1586124873209,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Söka efter dataflödesspecifikationer {#specs}

Ett dataflöde ansvarar för att samla in data från källor och föra in dem i plattformen. För att kunna skapa ett dataflöde måste du först få de dataflödesspecifikationer som ansvarar för att samla in data från ditt protokollprogram.

**API-format**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om dataflödesspecifikationen som ansvarar för att hämta data från källan till plattformen. Svaret innehåller den unika flödesspecifikation `id` som krävs för att skapa ett nytt dataflöde.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "221c7626-58f6-4eec-8ee2-042b0226f03b",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "102706fb-a5cd-42ee-afe0-bc42f017ff43",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "optionSpec": {
                "name": "OptionSpec",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "errorDiagnosticsEnabled": {
                            "title": "Error diagnostics.",
                            "description": "Flag to enable detailed and sample error diagnostics summary.",
                            "type": "boolean",
                            "default": false
                        },
                        "partialIngestionPercent": {
                            "title": "Partial ingestion threshold.",
                            "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                            "type": "number",
                            "exclusiveMinimum": 0
                        }
                    }
                }
            },
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
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
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "once",
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "once"
                            }
                        }
                    },
                    "then": {
                        "allOf": [
                            {
                                "not": {
                                    "required": [
                                        "interval"
                                    ]
                                }
                            },
                            {
                                "not": {
                                    "required": [
                                        "backfill"
                                    ]
                                }
                            }
                        ]
                    },
                    "else": {
                        "required": [
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
            },
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Skapa ett dataflöde

Det sista steget mot att samla in data är att skapa ett dataflöde. Nu bör du ha förberett följande obligatoriska värden:

* [Källanslutnings-ID](#source)
* [Målanslutnings-ID](#target)
* [Mappnings-ID](#mapping)
* [ID för dataflödesspecifikation](#specs)

Ett dataflöde ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en begäran om POST samtidigt som du anger de tidigare angivna värdena i nyttolasten.

Om du vill schemalägga ett intag måste du först ange starttidsvärdet till epok time i sekunder. Sedan måste du ange frekvensvärdet till ett av de fem alternativen: `once`, `minute`, `hour`, `day` eller `week`. Intervallvärdet anger perioden mellan två på varandra följande inmatningar och att skapa en engångsinmatning kräver inget intervall. För alla andra frekvenser måste intervallvärdet anges till lika med eller större än `15`.

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
        "name": "Creating a dataflow for a protocols source",
        "description": "Creating a dataflow for a protocols source",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "0a768941-ddfb-499d-b689-41ddfbf99db0"
        ],
        "targetConnectionIds": [
            "576d5ecf-f114-4587-ad5e-cff1144587f4"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "7409d3017e24a3eb4a2dc21020f7a5b",
                    "mappingVersion": "0"
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
| -------- | ----------- |
| `flowSpec.id` | Det [flödesspec-ID](#specs) som hämtades i föregående steg. |
| `sourceConnectionIds` | Det [källanslutnings-ID](#source) som hämtades i ett tidigare steg. |
| `targetConnectionIds` | [målanslutnings-ID](#target-connection) har hämtats i ett tidigare steg. |
| `transformations.params.mappingId` | [mappnings-ID](#mapping) har hämtats i ett tidigare steg. |
| `transformations.params.deltaColum` | Den angivna kolumnen används för att skilja mellan nya och befintliga data. Inkrementella data importeras baserat på tidsstämpeln för den markerade kolumnen. Formatet som stöds för `deltaColumn` när du använder Generic OData är `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | Det mappnings-ID som är kopplat till databasen. |
| `scheduleParams.startTime` | Starttiden för dataflödet i epok-tid. |
| `scheduleParams.frequency` | Frekvensen med vilken dataflödet samlar in data. Godtagbara värden är: `once`, `minute`, `hour`, `day` eller `week`. |
| `scheduleParams.interval` | Intervallet anger perioden mellan två på varandra följande flödeskörningar. Intervallets värde ska vara ett heltal som inte är noll. Intervall krävs inte när frekvens har angetts som `once` och ska vara större än eller lika med `15` för andra frekvensvärden. |

**Svar**

Ett godkänt svar returnerar ID `id` för det nya dataflödet.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om flödeskörningar, slutförandestatus och fel. Mer information om hur du övervakar dataflöden finns i självstudiekursen om [övervakning av dataflöden i API ](../monitor.md)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en källanslutning för att samla in data från ett protokollprogram schemalagt. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan, t.ex. [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

* [Översikt över kundprofiler i realtid](../../../../profile/home.md)
* [Översikt över arbetsytan Datavetenskap](../../../../data-science-workspace/home.md)