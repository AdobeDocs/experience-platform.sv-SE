---
title: Skapa ett dataflöde för inmatning av Source-data i Experience Platform
description: Lär dig använda API:t för Flow Service för att skapa ett dataflöde och importera källdata till Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 4e9448170a6c3eb378e003bcd7520cb0e573e408
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 0%

---

# Skapa ett dataflöde för att importera data från en källa

Läs den här vägledningen när du vill lära dig hur du skapar ett dataflöde och importerar data till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Gruppinmatning](../../../../ingestion/batch-ingestion/overview.md): Upptäck hur du kan överföra stora datavolymer effektivt i grupper.
* [Katalogtjänst](../../../../catalog/datasets/overview.md): Ordna och håll reda på datauppsättningarna i Experience Platform.
* [Dataprep](../../../../data-prep/home.md): Omforma och mappa inkommande data så att de matchar schemakraven.
* [Dataflöden](../../../../dataflows/home.md): Konfigurera och hantera pipelines som flyttar dina data från källor till mål.
* [XDM-scheman (Experience Data Model)](../../../../xdm/home.md): Strukturera dina data med XDM-scheman så att de kan användas i Experience Platform.
* [Sandlådor](../../../../sandboxes/home.md): Testa och utveckla säkert i isolerade miljöer utan att påverka produktionsdata.
* [Källor](../../../home.md): Lär dig ansluta externa datakällor till Experience Platform.

### Använda Experience Platform API:er

Mer information om hur du kan ringa anrop till Experience Platform API:er finns i guiden [komma igång med Experience Platform API:er](../../../../landing/api-guide.md).

### Skapa basanslutning

Du måste ha ett fullständigt autentiserat källkonto och det är motsvarande basanslutnings-ID för att kunna skapa ett dataflöde för källan. Om du inte har det här ID:t kan du gå till [källkatalogen](../../../home.md) och se en lista över källor som du kan skapa en basanslutning med.

### Skapa ett mål-XDM-schema {#target-schema}

Ett XDM-schema (Experience Data Model) är ett standardiserat sätt att organisera och beskriva kundupplevelsedata i Experience Platform. Om du vill importera källdata till Experience Platform måste du först skapa ett mål-XDM-schema som definierar strukturen och datatyperna som du vill importera. Det här schemat fungerar som en plan för den Experience Platform-datauppsättning där dina inmatade data finns.

Ett mål-XDM-schema kan skapas genom att en POST-begäran till [schemats register-API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) utförs. Läs de här riktlinjerna för mer ingående information om hur du skapar ett XDM-målschema:

* [Skapa ett schema med API:t ](../../../../xdm/api/schemas.md).
* [Skapa ett schema med användargränssnittet](../../../../xdm/tutorials/create-schema-ui.md).

När du har skapat målschemat `$id` kommer det att krävas senare för måldatauppsättningen och målmappningen.

### Skapa en måldatauppsättning {#target-dataset}

En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Data som har importerats till Experience Platform lagras i datasjön som datauppsättningar. Under det här steget kan du skapa en ny datauppsättning eller använda en befintlig datauppsättning.

Du kan skapa en måldatamängd genom att göra en POST-begäran till [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), samtidigt som du anger målschemats ID i nyttolasten. Detaljerade steg om hur du skapar en måldatauppsättning finns i guiden om att [skapa en datauppsättning med API:t](../../../../catalog/api/create-dataset.md).

>[!TIP]
>
>Om du vill importera dina data till kundprofilen i realtid måste du se till att både dina mål-XDM-scheman och måldatauppsättningen är aktiverade för profilen.

+++Markera för att visa exempel

**API-format**

```HTTP
POST /dataSets
```

**Begäran**

I följande exempel visas hur du skapar en måldatauppsättning som är aktiverad för kundprofilsinmatning i realtid. I den här begäran är egenskapen `unifiedProfile` inställd på `true` (under objektet `tags`), vilket innebär att Experience Platform ska inkludera den här datauppsättningen i kundprofilen i realtid.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Target Dataset",
    "schemaRef": {
      "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
      "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "tags": {
      "unifiedProfile": [
        "enabled: true"
      ]
    }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Ett beskrivande namn för måldatauppsättningen. Använd ett tydligt och unikt namn för att göra det enklare att identifiera och hantera datauppsättningen i framtida åtgärder. |
| `schemaRef.id` | ID för ditt mål-XDM-schema. |
| `tags.unifiedProfile` | Ett booleskt värde som informerar Experience Platform om data ska hämtas till kundprofilen i realtid. |

**Svar**

Ett lyckat svar returnerar ditt måldataset-ID. Detta ID krävs senare för att skapa en målanslutning.

```json
[
    "@/dataSets/6889f4f89b982b2b90bc1207"
]
```

+++

## Skapa en källanslutning

En källanslutning definierar hur data hämtas till Experience Platform från en extern källa. Den anger både källsystemet och formatet för inkommande data och refererar till en basanslutning som innehåller autentiseringsinformation. Varje källanslutning är unik för din organisation.

* För filbaserade källor (till exempel molnlagring) kan en källanslutning innehålla inställningar som kolumnavgränsare, kodningstyp, komprimeringstyp, reguljära uttryck för filval och huruvida filer ska importeras rekursivt.
* För tabellbaserade källor (t.ex. databaser, CRM och leverantörer av automatiserad marknadsföring) kan en källanslutning ange detaljer som tabellnamn och kolumnmappningar.

Om du vill skapa en källanslutning gör du en POST-begäran till `/sourceConnections`-slutpunkten för [!DNL Flow Service] API:t och anger ditt grundläggande anslutnings-ID, anslutningsspecifikations-ID och sökväg till källdatafilen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME source connection",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "description": "A source connection for ACME contact data",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "Contact",
      "columns": [
        {
          "name": "TestID",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Name",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Datefield",
          "type": "string",
          "meta:xdmType": "date-time",
          "xdm": {
            "type": "string",
            "format": "date-time"
          }
        }
      ],
      "cdcEnabled": true
    },
    "connectionSpec": {
      "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
      "version": "1.0"
    }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Ett beskrivande namn för källanslutningen. Använd ett tydligt och unikt namn för att göra det enklare att identifiera och hantera anslutningen i framtida åtgärder. |
| `description` | En valfri beskrivning som du kan lägga till för att ge ytterligare information om din källanslutning. |
| `baseConnectionId` | `id` för din basanslutning. Du kan hämta detta ID genom att autentisera källan till Experience Platform med API:t [!DNL Flow Service]. |
| `data.format` | Dataformatet. Ange det här värdet till `tabular` för tabellbaserade källor (t.ex. databaser, CRM och leverantörer av automatiserad marknadsföring). |
| `params.tableName` | Namnet på tabellen i källkontot som du vill importera till Experience Platform. |
| `params.columns` | De specifika tabellkolumnerna med data som du vill importera till Experience Platform. |
| `params.cdcEnabled` | Ett booleskt värde som anger om registrering av ändringshistorik är aktiverat eller inte. Den här egenskapen stöds av följande datakällor: <ul><li>[!DNL Azure Databricks]</li><li>[!DNL Google BigQuery]</li><li>[!DNL Snowflake]</li></ul> Mer information finns i guiden om hur du använder [ändring av datainhämtning i källor](../change-data-capture.md). |
| `connectionSpec.id` | Anslutningsspecifikations-ID för källan som du använder. |

**Svar**

Ett lyckat svar returnerar ID:t för din källanslutning. Detta ID krävs för att skapa ett dataflöde och importera dina data.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inkapslade data kommer in. Om du vill skapa en målanslutning måste du ange det fasta anslutnings-spec-ID som är associerat med datasjön. Anslutningens spec-ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
      "name": "ACME target connection",
      "description": "ACME target connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Ett beskrivande namn för målanslutningen. Använd ett tydligt och unikt namn för att göra det enklare att identifiera och hantera anslutningen i framtida åtgärder. |
| `description` | En valfri beskrivning som du kan lägga till för att ge ytterligare information om målanslutningen. |
| `data.schema.id` | ID för ditt mål-XDM-schema. |
| `params.dataSetId` | ID för måldatauppsättningen. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för datasjön. Detta ID har åtgärdats: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

## Mappning {#mapping}

Därefter måste du mappa källdata till målschemat som måldatauppsättningen följer. Om du vill skapa en mappning gör du en POST-begäran till `mappingSets`-slutpunkten för [[!DNL Data Prep]  API](https://developer.adobe.com/experience-platform-apis/references/data-prep/), anger ditt mål-XDM-schema-ID och information om de mappningsuppsättningar som du vill skapa.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [
          {
              "destinationXdmPath": "_id",
              "sourceAttribute": "TestID",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.fullName",
              "sourceAttribute": "Name",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.birthDate",
              "sourceAttribute": "Datefield",
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
    "id": "93ddfa69c4864d978832b1e5ef6ec3b9",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Hämta dataflödesspecifikationer

Innan du kan skapa ett dataflöde måste du först hämta de dataflödesspecifikationer som motsvarar källan. Om du vill hämta den här informationen skickar du en GET-begäran till `/flowSpecs`-slutpunkten för API:t [!DNL Flow Service].

**API-format**

```http
GET /flowSpecs?property=name=="{NAME}"
```

| Frågeparameter | Beskrivning |
| --- | --- |
| `property=name=="{NAME}"` | Namnet på dataflödesspecifikationen. <ul><li>För filbaserade källor (till exempel molnlagring) anger du värdet `CloudStorageToAEP`.</li><li>Ange det här värdet till `CRMToAEP` för tabellbaserade källor (t.ex. databaser, CRM och leverantörer av automatiserad marknadsföring).</li></ul> |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om dataflödesspecifikationen som ansvarar för att hämta data från källan till Experience Platform. Svaret innehåller den unika flödesspecifikation `id` som krävs för att skapa ett nytt dataflöde.

Kontrollera `items.sourceConnectionSpecIds`-arrayen i svaret för att försäkra dig om att du använder rätt dataflödesspecifikation. Bekräfta att källans anslutningsspec-ID finns med i listan.

+++Välj att visa

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
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "fcad62f3-09b0-41d3-be11-449d5a621b69",
                "ea1c2a08-b722-11eb-8529-0242ac130003",
                "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
                "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
                "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
                "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
                "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b"
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
            "runSpec": {
                "name": "ProviderParams",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines various params required for creating flow run.",
                    "properties": {
                        "startTime": {
                            "type": "integer",
                            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
                        },
                        "windowStartTime": {
                            "type": "integer",
                            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
                        },
                        "windowEndTime": {
                            "type": "integer",
                            "description": "An integer that defines the end time of the window against which data is to be pulled. The value is represented in Unix epoch time."
                        },
                        "deltaColumn": {
                            "type": "object",
                            "description": "The delta column is required to partition the data and separate newly ingested data from historic data.",
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
                        "startTime",
                        "windowStartTime",
                        "windowEndTime",
                        "deltaColumn"
                    ]
                }
            },
            "attributes": {
                "recordTypeEnabled": true,
                "defaultRecordType": "profile",
                "isSourceFlow": true,
                "flacValidationSupported": true,
                "isDraftModeSupported": true,
                "frequency": "batch",
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

## Skapa ett dataflöde

Ett dataflöde är en konfigurerad pipeline som överför data mellan Experience Platform-tjänster. Det definierar hur data hämtas från externa källor (som databaser, molnlagring eller API:er), bearbetas och dirigeras till måldatamängder. Dessa datauppsättningar används sedan av tjänster som identitetstjänst, kundprofil i realtid och destinationer för aktivering och analys.

Om du vill skapa ett dataflöde måste du ha värden för följande objekt:

* Source-anslutnings-ID
* Målanslutnings-ID
* Mappnings-ID
* ID för dataflödesspecifikation

Under det här steget kan du använda följande parametrar i `scheduleParams` för att konfigurera ett intag-schema för ditt dataflöde:

| Schemaläggningsparameter | Beskrivning |
| --- | --- |
| `startTime` | epoktiden (i sekunder) när dataflödet ska starta. |
| `frequency` | Hur ofta du har fått i dig läkemedlet. Konfigurera frekvens för att ange hur ofta dataflödet ska köras. Du kan ange frekvensen till: <ul><li>`once`: Ställ in din frekvens på `once` för att skapa en engångsinmatning. Konfigurationer för intervall och bakåtfyllnad är inte tillgängliga när ett dataflöde för engångsinmatning skapas. Som standard är schemaläggningsfrekvensen inställd på en gång.</li><li>`minute`: Ställ in din frekvens på `minute` för att schemalägga ditt dataflöde att importera data per minut.</li><li>`hour`: Ställ in din frekvens på `hour` för att schemalägga ditt dataflöde att importera data per timme.</li><li>`day`: Ställ in din frekvens på `day` för att schemalägga ditt dataflöde att importera data per dag.</li><li>`week`: Ställ in din frekvens på `week` för att schemalägga ditt dataflöde att importera data per vecka.</li></ul> |
| `interval` | Intervallet mellan efterföljande inmatningar (krävs för alla frekvenser utom `once`). Konfigurera intervallinställningen för att fastställa tidsramen mellan varje intag. Om du t.ex. anger din frekvens som dag och konfigurerar intervallet till 15, kommer dataflödet att köras var 15:e dag. Du kan inte ange intervallet till noll. Det minsta tillåtna intervallvärdet för varje frekvens är följande:<ul><li>`once`: ingen</li><li>`minute`: 15</li><li>`hour`: 1</li><li>`day`: 1</li><li>`week`: 1</li></ul> |
| `backfill` | Anger om historiska data ska importeras före `startTime`. |

{style="table-layout:auto"}


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
      "name": "ACME Contact Dataflow",
      "description": "A dataflow for ACME contact data",
      "flowSpec": {
          "id": "14518937-270c-4525-bdec-c2ba7cce3860",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "b7581b59-c603-4df1-a689-d23d7ac440f3"
      ],
      "targetConnectionIds": [
          "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
      ],
      "transformations": [
          {
              "name": "Copy",
              "params": {
                  "deltaColumn": {
                      "name": "Datefield",
                      "dateFormat": "YYYY-MM-DD",
                      "timezone": "UTC"
                  }
              }
          },
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "93ddfa69c4864d978832b1e5ef6ec3b9",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1612310466",
          "frequency":"minute",
          "interval":"15",
          "backfill": "true"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Ett beskrivande namn för dataflödet. Använd ett tydligt och unikt namn för att göra det enklare att identifiera och hantera dataflödet i framtida åtgärder. |
| `description` | En valfri beskrivning som du kan lägga till för att ge ytterligare information om dataflödet. |
| `flowSpec.id` | ID:t för den flödesspecifikation som motsvarar källan. |
| `sourceConnectionIds` | Källanslutnings-ID som genererades i ett tidigare steg. |
| `targetConnectionIds` | Målanslutnings-ID som genererades i ett tidigare steg. |
| `transformations.params.deltaColum` | Den angivna kolumnen används för att skilja mellan nya och befintliga data. Inkrementella data importeras baserat på tidsstämpeln för den markerade kolumnen. Det format som stöds för `deltaColumn` är `yyyy-MM-dd HH:mm:ss`. För [!DNL Microsoft Dynamics] är det format som stöds för `deltaColumn` `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.deltaColumn.dateFormat` | Datumformatet som ska följas för deltakolumnen. |
| `transformations.params.deltaColumn.timeZone` | Tidszonen som ska användas vid tolkning av värdena i deltakolumnen. |
| `transformations.params.mappingId` | Mappnings-ID som genererades i ett tidigare steg. |
| `scheduleParams.startTime` | Starttiden för dataflödet i epok-tid (sekunder sedan Unix-epok). Avgör när dataflödet börjar sin första körning. |
| `scheduleParams.frequency` | Den frekvens som dataflödet körs med. Godtagbara värden är: `once`, `minute`, `hour`, `day` eller `week`. |
| `scheduleParams.interval` | Intervallet mellan på varandra följande dataflöden körs, baserat på vald frekvens. Måste vara ett heltal som inte är noll. Ett intervall på `15` med frekvensen `minute` innebär till exempel att dataflödet körs var 15:e minut. |
| `scheduleParams.backfill` | Ett booleskt värde (`true` eller `false`) som avgör om historiska data (bakåtfyllnad) ska importeras när dataflödet skapas. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar ID:t (`id`) för det nyskapade dataflödet.

```json
{
    "id": "ae0a9777-b322-4ac1-b0ed-48ae9e497c7e",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

### Använd gränssnittet för att validera API-arbetsflödet

Du kan använda Experience Platform användargränssnitt för att validera skapandet av dataflödet. Navigera till katalogen *[!UICONTROL Sources]* i Experience Platform-gränssnittet och välj sedan **[!UICONTROL Dataflows]** på rubrikflikarna. Använd sedan kolumnen [!UICONTROL Dataflow Name] och leta reda på dataflödet som du skapade med API:t [!DNL Flow Service].

![Dataflödsgränssnittet för källarbetsytan i Experience Platform-gränssnittet ](../../../images/tutorials/validations/dataflows-interface.png)

Du kan validera ditt dataflöde ytterligare via gränssnittet [!UICONTROL Dataflow activity]. Använd den högra listen för att visa [!UICONTROL API usage]-information om dataflödet. I det här avsnittet visas samma dataflödes-ID, datauppsättnings-ID och mappnings-ID som genererades när dataflödet skapades i [!DNL Flow Service].

![Dataflödesvisningssidan för källarbetsytan.](../../../images/tutorials/validations/api-usage.png)

## Nästa steg

I den här självstudiekursen får du hjälp med att skapa ett dataflöde i Experience Platform med hjälp av API:t [!DNL Flow Service]. Du lärde dig att skapa och konfigurera nödvändiga komponenter, inklusive mål-XDM-schema, datauppsättning, källanslutning, målanslutning och själva dataflödet. Genom att följa dessa steg kan du automatisera inmatningen av data från externa källor till Experience Platform, vilket gör att underordnade tjänster som kundprofil och destinationer i realtid kan utnyttja dina inmatade data för avancerade användningsfall.

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det för att visa information om hur mycket data som har importerats, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen [Övervaka konton och dataflöden](../../../../dataflows/ui/monitor-sources.md).

### Uppdatera ditt dataflöde

Om du vill uppdatera konfigurationer för schemaläggning, mappning och allmän information för dina dataflöden går du till självstudiekursen [Uppdatera källfilens dataflöden](../../api/update-dataflows.md).

## Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med funktionen **[!UICONTROL Delete]** som finns på arbetsytan i **[!UICONTROL Dataflows]**. Mer information om hur du tar bort dataflöden finns i självstudiekursen [Ta bort dataflöden](../../api/delete.md).