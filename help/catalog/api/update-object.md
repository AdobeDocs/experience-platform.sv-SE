---
keywords: Experience Platform;hem;populära ämnen;katalog;api;uppdatera ett objekt
solution: Experience Platform
title: Uppdatera ett katalogobjekt
description: Du kan uppdatera en del av ett Catalog-objekt genom att ta med dess ID i sökvägen för en PATCH-begäran. Det här dokumentet innehåller information om hur du använder fält och JSON Patch-notation för att utföra PATCH-åtgärder på katalogobjekt.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Uppdatera ett katalogobjekt

Du kan uppdatera en del av ett [!DNL Catalog]-objekt genom att ta med dess ID i sökvägen för en PATCH-begäran. Det här dokumentet innehåller två metoder för att utföra PATCH-åtgärder på katalogobjekt:

* Använda fält
* Använda JSON Patch-notation

>[!NOTE]
>
>PATCH-åtgärder för ett objekt kan inte ändra dess utökningsbara fält, som representerar relaterade objekt. Ändringar av sammanhörande objekt måste göras direkt.

## Uppdatera med fält

I följande exempelanrop visas hur du uppdaterar ett objekt med hjälp av fält och värden.

**API-format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska uppdateras. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar fälten `name` och `description` i en datamängd till värdena som anges i nyttolasten. Objektfält som inte ska uppdateras kan uteslutas från nyttolasten.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickas i PATCH-begäran. När en GET-begäran utförs för den här datauppsättningen visas nu att endast `name` och `description` har uppdaterats medan alla andra värden förblir oförändrade.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Uppdatera med JSON Patch-notation {#patch-notation}

I följande exempelanrop visas hur du uppdaterar ett objekt med JSON Patch, enligt beskrivningen i [RFC-6902](https://tools.ietf.org/html/rfc6902).

Mer information om JSON Patch-syntax finns i [API-handboken ](../../landing/api-fundamentals.md#json-patch).

**API-format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska uppdateras. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar fälten `name` och `description` i en datauppsättning till de värden som anges i varje JSON Patch-objekt. När du använder JSON Patch måste du även ange Content-Type-huvudet till `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för det uppdaterade objektet. Detta ID ska matcha det som skickas i PATCH-begäran. När en GET-begäran utförs för det här objektet visas nu att endast `name` och `description` har uppdaterats medan alla andra värden förblir oförändrade.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Uppdatera med PATCH v2-notering {#patch-v2-notation}

Slutpunkten `/v2/dataSets/{DATASET_ID}` är ett mer flexibelt sätt att uppdatera komplexa eller djupt inkapslade datauppsättningsattribut.

När du uppdaterar ett djupt inkapslat fält (till exempel `a.b.c.d`) måste vanligtvis varje nivå i sökvägen redan finnas. Om någon nivå saknas måste du skapa varje nivå manuellt innan du anger det slutgiltiga värdet. Detta kräver ofta flera åtgärder, vilket ökar komplexiteten och risken för fel.

Slutpunkten `/v2/dataSets/{DATASET_ID}` skapar automatiskt nivåer som saknas i banan. I stället för att kontrollera och lägga till `b` och `c` innan du anger `d` manuellt, gör PATCH `v2`-åtgärden det här åt dig.

När du skickar en PATCH-begäran till `/v2/dataSets/{DATASET_ID}`-slutpunkten behöver du bara skicka den slutliga strukturen, och systemet fyller i de delar som saknas innan du tillämpar uppdateringen.

>[!NOTE]
>
>`If-Match` och `If-None-Match` huvuden är valfria för slutpunkten `/v2/dataSets/{id}`. PATCH-begäranden till den här slutpunkten sammanfogar uppdateringar dynamiskt, vilket tillåter ändringar utan att hämta den senaste datauppsättningsversionen. Detta minskar risken för dataförlust vid samtidiga uppdateringar, men du kan använda `If-Match` med den senaste `etag` för att se till att ändringarna bara gäller för en viss version. Alternativt kan `If-None-Match` förhindra uppdateringar om datauppsättningen inte har ändrats sedan den senaste kända versionen.

**API-format**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Identifieraren för den datauppsättning som ska uppdateras. |

**Begäran**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för den uppdaterade datauppsättningen, som ska matcha det ID som skickades i PATCH-begäran. När en GET-begäran utförs för det här objektet visas nu att `extensions.adobe_lakeHouse.rowExpiration`-objektet har skapats utan att föregående manuella steg behöver skapas.

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### En exempeldatauppsättning före och efter uppdatering

I exemplet JSON nedan illustreras datauppsättningsstrukturen **före** PATCH-begäran, där `extensions.adobe_lakeHouse.rowExpiration`-objektet inte finns i datauppsättningen.

+++Markera för att visa exempel

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

I följande JSON visas datauppsättningsstrukturen **efter** PATCH-begäran. Uppdateringen skapar automatiskt det saknade `extensions.adobe_lakeHouse.rowExpiration`-objektet utan föregående steg för att skapa manuellt. I det här exemplet visas hur PATCH-begäran `/v2/` eliminerar behovet av flera åtgärder, vilket gör uppdateringarna enklare och effektivare.


+++Markera för att visa exempel

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
