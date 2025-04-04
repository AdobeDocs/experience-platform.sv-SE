---
keywords: Experience Platform;home;populära topics;data prep;api guide;schemas;
solution: Experience Platform
title: API-slutpunkt för scheman
description: Du kan använda ändpunkten "/schemas" i Adobe Experience Platform API för att hämta, skapa och uppdatera scheman för användning med Mapper i Experience Platform.
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---



# Schemas slutpunkt

Scheman kan användas med Mapper för att säkerställa att data som du har inhämtat till Adobe Experience Platform matchar det du vill importera. Du kan använda slutpunkten `/schemas` för att skapa, lista och hämta anpassade scheman för användning med Mapper i Experience Platform.

>[!NOTE]
>
>Scheman som skapas med den här slutpunkten används exklusivt med mappar- och mappningsuppsättningar. Om du vill skapa scheman som är tillgängliga för andra Experience Platform-tjänster läser du [utvecklarhandboken för schemaregister](../../xdm/api/schemas.md).

## Hämta alla scheman

Du kan hämta en lista över alla tillgängliga mappningsscheman för din organisation genom att göra en GET-begäran till slutpunkten `/schemas`.

**API-format**

Slutpunkten `/schemas` har stöd för flera frågeparametrar som hjälper dig att filtrera dina resultat. De flesta av dessa parametrar är valfria, men bör användas för att minska kostsamma overheadkostnader. Du måste dock inkludera både parametern `start` och parametern `limit` som en del av din begäran. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{LIMIT}` | **Krävs**. Anger antalet returnerade scheman. |
| `{START}` | **Krävs**. Anger förskjutningen för resultatsidorna. Om du vill hämta den första resultatsidan anger du värdet till `start=0`. |
| `{NAME}` | Filtrerar schemat baserat på namnet. |
| `{ORDER_BY}` | Sorterar resultatens ordning. De fält som stöds är `modifiedDate` och `createdDate`. Du kan lägga till egenskapen i `+` eller `-` för att sortera den i stigande eller fallande ordning. |

**Begäran**

Följande begäran hämtar de två senast skapade schemana för din organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Följande svar returnerar HTTP-status 200 med en lista över begärda scheman.

>[!NOTE]
>
>Följande svar har trunkerats för utrymme.

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## Skapa ett schema

Du kan skapa ett schema att validera mot genom att göra en POST-begäran till slutpunkten `/schemas`. Det finns tre sätt att skapa ett schema: skicka ett [JSON-schema](https://json-schema.org/), använda exempeldata eller referera till ett befintligt XDM-schema.

```http
POST /schemas
```

### Använda ett JSON-schema

**Begäran**

Med följande begäran kan du skapa ett schema genom att skicka ett [JSON-schema](https://json-schema.org/).

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade schema.

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### Använda exempeldata

**Begäran**

Med följande begäran kan du skapa ett schema med exempeldata som du tidigare har överfört.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `sampleId` | ID:t för exempeldata som du baserar schemat på. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade schema.

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### Se ett XDM-schema

**Begäran**

Med följande begäran kan du skapa ett schema genom att referera till ett befintligt XDM-schema.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på schemat som du vill skapa. |
| `schemaRef.id` | ID:t för schemat som du refererar till. |
| `schemaRef.contentType` | Bestämmer svarsformatet för det refererade schemat. Mer information om det här fältet finns i [utvecklarhandboken för schemaregister](../../xdm/api/schemas.md#lookup) |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade schema.

>[!NOTE]
>
>Följande svar har trunkerats för utrymme.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Skapa ett schema med filöverföring

Du kan skapa ett schema genom att överföra en JSON-fil som den kan konverteras från.

**API-format**

```http
POST /schemas/upload
```

**Begäran**

Med följande begäran kan du skapa ett schema från en överförd JSON-fil.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade schema.

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## Hämta ett specifikt schema

Du kan hämta information om ett specifikt schema genom att göra en GET-begäran till slutpunkten `/schemas` och ange det schema som du vill hämta i sökvägen till begäran.

**API-format**

```http
GET /schemas/{SCHEMA_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEMA_ID}` | ID:t för schemat som du söker efter. |

**Begäran**

Följande begäran hämtar information om det angivna schemat.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om det angivna schemat.

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
