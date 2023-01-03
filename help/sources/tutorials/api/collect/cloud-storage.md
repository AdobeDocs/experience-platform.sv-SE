---
keywords: Experience Platform;hem;populära ämnen;molnlagringsdata
solution: Experience Platform
title: Skapa ett dataflöde för molnlagringskällor med API:t för flödestjänsten
topic-legacy: overview
type: Tutorial
description: I den här självstudiekursen beskrivs stegen för att hämta data från ett molnlagringsutrymme från tredje part och föra in dem på plattformen med hjälp av källanslutningar och API:er.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 0%

---

# Skapa ett dataflöde för molnlagringskällor med [!DNL Flow Service] API

I den här självstudiekursen beskrivs stegen för att hämta data från en molnlagringskälla och föra dem till plattformen med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Om du vill skapa ett dataflöde måste du redan ha ett giltigt ID för basanslutningen med en molnlagringskälla. Om du inte har detta ID kan du se [källöversikt](../../../home.md#cloud-storage) för en lista över molnlagringskällor som du kan skapa en basanslutning med.

## Komma igång

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Utvecklarhandbok för schemaregister](../../../../xdm/api/getting-started.md): Innehåller viktig information som du behöver känna till för att kunna utföra anrop till API:t för schemaregister. Detta inkluderar `{TENANT_ID}`, begreppet&quot;behållare&quot; och de rubriker som krävs för att göra en begäran (med särskild uppmärksamhet på rubriken Godkänn och dess möjliga värden).
- [[!DNL Catalog Service]](../../../../catalog/home.md): Katalog är systemet för registrering av dataplatser och -länkar inom Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Med API:t för gruppinmatning kan du importera data till Experience Platform som gruppfiler.
- [Sandlådor](../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../landing/api-guide.md).

## Skapa en källanslutning {#source}

Du kan skapa en källanslutning genom att göra en POST-förfrågan till `sourceConnections` slutpunkt för [!DNL Flow Service] API när du anger ditt basanslutnings-ID, sökvägen till källfilen som du vill importera och källans motsvarande anslutningsspecifikations-ID.

När du skapar en källanslutning måste du också definiera ett uppräkningsvärde för dataformatattributet.

Använd följande uppräkningsvärden för filbaserade källor:

| Dataformat | Uppräkningsvärde |
| ----------- | ---------- |
| Avgränsad | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

För alla tabellbaserade källor anger du värdet till `tabular`.

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
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `baseConnectionId` | Basanslutnings-ID för molnlagringskällan. |
| `data.format` | Formatet på de data du vill hämta till plattformen. Värden som stöds är: `delimited`, `JSON`och `parquet`. |
| `data.properties` | (Valfritt) En uppsättning egenskaper som du kan använda på dina data när du skapar en källanslutning. |
| `data.properties.columnDelimiter` | (Valfritt) En kolumnavgränsare för ett tecken som du kan ange när du samlar in platta filer. Ett teckenvärde är en tillåten kolumnavgränsare. Om inget anges, ett komma (`,`) används som standardvärde. **Anteckning**: The `columnDelimiter` -egenskapen kan bara användas vid inhämtning av avgränsade filer. |
| `data.properties.encoding` | (Valfritt) En egenskap som definierar den kodningstyp som ska användas när data hämtas till plattformen. Följande kodningstyper stöds: `UTF-8` och `ISO-8859-1`. **Anteckning**: The `encoding` -parametern är bara tillgänglig vid inhämtning av avgränsade CSV-filer. Andra filtyper kommer att importeras med standardkodningen, `UTF-8`. |
| `data.properties.compressionType` | (Valfritt) En egenskap som definierar den komprimerade filtypen för förtäring. Komprimerade filtyper som stöds är: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`och `tar`. **Anteckning**: The `compressionType` -egenskapen kan bara användas vid inhämtning av avgränsade filer eller JSON-filer. |
| `params.path` | Sökvägen till källfilen som du försöker komma åt. Den här parametern pekar på en enskild fil eller en hel mapp.  **Anteckning**: Du kan använda en asterisk i stället för filnamnet om du vill ange att en hel mapp ska tas emot. Till exempel: `/acme/summerCampaign/*.csv` kommer att importera hela `/acme/summerCampaign/` mapp. |
| `params.type` | Filtypen för den källdatafil som du vill importera. Använd typ `file` för att importera en enskild fil och använda typ `folder` om du vill importera en hel mapp. |
| `connectionSpec.id` | Det ID för anslutningsspecifikation som är kopplat till din specifika molnlagringskälla. Se [appendix](#appendix) för en lista över anslutningsspecifikations-ID:n. |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Använd reguljära uttryck för att välja en specifik uppsättning filer för förtäring {#regex}

Du kan använda reguljära uttryck för att importera en viss uppsättning filer från källan till plattformen när du skapar en källanslutning.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

I exemplet nedan används reguljära uttryck i filsökvägen för att ange att alla CSV-filer som har `premium` i deras namn.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### Konfigurera en källanslutning för rekursiv inmatning av data

När du skapar en källanslutning kan du använda `recursive` parameter för att importera data från djupt inkapslade mappar.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

I exemplet nedan är `recursive: true` parameterinformation [!DNL Flow Service] om du vill läsa alla undermappar rekursivt under importen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## Skapa ett mål-XDM-schema {#target-schema}

För att källdata ska kunna användas i Platform måste ett målschema skapas för att strukturera källdata efter dina behov. Målschemat används sedan för att skapa en plattformsdatauppsättning där källdata finns.

Ett mål-XDM-schema kan skapas genom att utföra en POST-begäran till [API för schemaregister](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Detaljerade anvisningar om hur du skapar ett XDM-målschema finns i självstudiekursen om [skapa ett schema med API](../../../../xdm/api/schemas.md).

## Skapa en måldatauppsättning {#target-dataset}

En måldatauppsättning kan skapas genom att en POST till [Katalogtjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), med ID:t för målschemat i nyttolasten.

Detaljerade anvisningar om hur du skapar en måldatauppsättning finns i självstudiekursen om [skapa en datauppsättning med API](../../../../catalog/api/create-dataset.md).

## Skapa en målanslutning {#target-connection}

En målanslutning representerar anslutningen till målet där inkapslade data kommer in. Om du vill skapa en målanslutning måste du ange det fasta anslutnings-spec-ID som är associerat med datasjön. Detta anslutningsspec-ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Nu har du de unika identifierarna ett målschema, en måldatamängd och ett anslutningsspec-ID till datasjön. Med dessa identifierare kan du skapa en målanslutning med [!DNL Flow Service] API för att ange den datauppsättning som ska innehålla inkommande källdata.

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `data.schema.id` | The `$id` av mål-XDM-schemat. |
| `data.schema.version` | Schemats version. Det här värdet måste anges `application/vnd.adobe.xed-full+json;version=1`, som returnerar den senaste delversionen av schemat. |
| `params.dataSetId` | ID för måldatauppsättningen. |
| `connectionSpec.id` | Det fasta anslutningens spec-ID till Data Lake. Detta ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Svar**

Ett godkänt svar returnerar den nya målanslutningens unika identifierare (`id`). Detta ID krävs i senare steg.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Skapa en mappning {#mapping}

För att källdata ska kunna hämtas till en måldatamängd måste den först mappas till målschemat som måldatamängden följer.

Skapa en mappningsuppsättning genom att göra en POST-förfrågan till `mappingSets` slutpunkt för [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) när du tillhandahöll ditt mål-XDM-schema `$id` och information om de mappningsuppsättningar som du vill skapa.

>[!TIP]
>
>Du kan mappa komplexa datatyper som arrayer i JSON-filer med hjälp av en anslutning till en molnlagringskälla.

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
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
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
            }
        ]
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdmSchema` | ID:t för mål-XDM-schemat. |

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

## Hämta dataflödesspecifikationer {#specs}

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!NOTE]
>
>Nyttolasten för JSON-svar nedan är dold av utrymmesskäl. Välj &quot;nyttolast&quot; för att se svarsnyttolasten.

+++ Visa nyttolast

**Svar**

Ett lyckat svar returnerar information om dataflödesspecifikationen som ansvarar för att hämta data från källan till plattformen. Svaret innehåller den unika flödesspecifikationen `id` krävs för att skapa ett nytt dataflöde.

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
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
  },
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
  "transformationSpec": [
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
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## Skapa ett dataflöde

Det sista steget mot att samla in molnlagringsdata är att skapa ett dataflöde. Nu har du förberett följande obligatoriska värden:

- [Källanslutnings-ID](#source)
- [Målanslutnings-ID](#target)
- [Mappnings-ID](#mapping)
- [ID för dataflödesspecifikation](#specs)

Ett dataflöde ansvarar för att schemalägga och samla in data från en källa. Du kan skapa ett dataflöde genom att utföra en begäran om POST samtidigt som du anger de tidigare angivna värdena i nyttolasten.

>[!NOTE]
>
>För batchimport väljer varje efterföljande dataflöde filer som ska importeras från källan baserat på deras **senast ändrad** tidsstämpel. Detta innebär att gruppdataflöden hämtar valda filer från källan som antingen är nya eller har ändrats sedan den senaste dataflödeskörningen.

Om du vill schemalägga ett intag måste du först ange starttidsvärdet till epok time i sekunder. Sedan måste du ange frekvensvärdet till ett av de fem alternativen: `once`, `minute`, `hour`, `day`, eller `week`. Intervallvärdet anger perioden mellan två på varandra följande inmatningar och att skapa en engångsinmatning kräver inget intervall. För alla andra frekvenser måste intervallvärdet anges till lika med eller större än `15`.

>[!IMPORTANT]
>
>Vi rekommenderar att du schemalägger dataflödet för engångsbruk när du använder [FTP-anslutning](../../../connectors/cloud-storage/ftp.md).

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
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `flowSpec.id` | The [flödesspec-ID](#specs) hämtat i föregående steg. |
| `sourceConnectionIds` | The [källanslutnings-ID](#source) hämtat i ett tidigare steg. |
| `targetConnectionIds` | The [målanslutnings-ID](#target-connection) hämtat i ett tidigare steg. |
| `transformations.params.mappingId` | The [mappnings-ID](#mapping) hämtat i ett tidigare steg. |
| `scheduleParams.startTime` | Starttiden för dataflödet i epok-tid. |
| `scheduleParams.frequency` | Frekvensen med vilken dataflödet samlar in data. Godtagbara värden är: `once`, `minute`, `hour`, `day`, eller `week`. |
| `scheduleParams.interval` | Intervallet anger perioden mellan två på varandra följande flödeskörningar. Intervallets värde ska vara ett heltal som inte är noll. Intervall krävs inte när frekvens har angetts som `once` och ska vara större än eller lika med `15` för andra frekvensvärden. |

**Svar**

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om flödeskörningar, slutförandestatus och fel. Mer information om hur du övervakar dataflöden finns i självstudiekursen om [övervaka dataflöden i API](../monitor.md)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en källanslutning för att samla in data från din molnlagring på schemalagd basis. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan som [!DNL Real-Time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

- [Översikt över kundprofiler i realtid](../../../../profile/home.md)
- [Översikt över arbetsytan Datavetenskap](../../../../data-science-workspace/home.md)

## Bilaga {#appendix}

I följande avsnitt visas de olika anslutningarna till molnlagringskällan och deras anslutningsspecifikationer.

### Anslutningsspecifikation

| Anslutningsnamn | Anslutningsspecifikation |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (Händelsehubbar) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
