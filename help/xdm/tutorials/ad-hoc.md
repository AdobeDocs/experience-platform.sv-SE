---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa ett ad hoc-schema
topic: tutorials
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---


# Skapa ett ad hoc-schema

Under särskilda omständigheter kan det vara nödvändigt att skapa ett XDM-schema (Experience Data Model) med fält som bara namnges av en enda datauppsättning. Detta kallas för ett ad hoc-schema. Ad-hoc-scheman används i olika arbetsflöden för dataöverföring för Experience Platform, inklusive inhämtning av CSV-filer och skapande av vissa typer av källanslutningar.

Det här dokumentet innehåller allmänna steg för att skapa ett ad hoc-schema med API:t för [schemaregister](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Den är avsedd att användas tillsammans med andra självstudiekurser på Experience Platform som kräver att ett ad hoc-schema skapas som en del av arbetsflödet. Var och en av dessa dokument innehåller detaljerad information om hur man konfigurerar ett ad hoc-schema för sitt specifika användningsfall.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för Experience Data Model (XDM) System. Läs följande XDM-dokumentation innan du startar den här självstudiekursen:

- [XDM - systemöversikt](../home.md): Översikt över XDM och dess implementering i Experience Platform.
- [Grundläggande om schemakomposition](../schema/composition.md): En översikt över de grundläggande komponenterna i XDM-scheman.

Innan du startar den här självstudiekursen bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för att få viktig information som du behöver känna till för att kunna anropa API:t för schemaregister. Detta inkluderar ditt `{TENANT_ID}`, konceptet med&quot;behållare&quot; och de rubriker som krävs för att göra förfrågningar (med särskild uppmärksamhet på rubriken Godkänn och dess möjliga värden).

## Skapa en ad hoc-klass

Databeteendet för ett XDM-schema bestäms av dess underliggande klass. Det första steget i att skapa ett ad hoc-schema är att skapa en klass baserat på `adhoc` beteendet. Detta görs genom att en POST-begäran görs till `/tenant/classes` slutpunkten.

**API-format**

```http
POST /tenant/classes
```

**Begäran**

Följande begäran skapar en ny XDM-klass som konfigurerats med attributen som anges i nyttolasten. Genom att ange en `$ref` egenskap som anges `https://ns.adobe.com/xdm/data/adhoc` i `allOf` arrayen ärver den här klassen `adhoc` beteendet. Begäran definierar också ett `_adhoc` objekt som innehåller anpassade fält för klassen.

>[!NOTE]
>
>De anpassade fälten som definieras under `_adhoc` varierar beroende på hur ad hoc-schemat används. Se det specifika arbetsflödet i rätt självstudiekurs för obligatoriska anpassade fält baserat på användningsfall.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `$ref` | Databeteendet för den nya klassen. För ad hoc-klasser måste det här värdet anges till `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Ett objekt som innehåller anpassade fält för klassen, uttryckt som nyckelvärdepar med fältnamn och datatyper. |

**Svar**

Ett lyckat svar returnerar informationen om den nya klassen och ersätter `properties._adhoc` objektets namn med ett GUID som är en systemgenererad, skrivskyddad unik identifierare för klassen. Attributet `meta:datasetNamespace` genereras också automatiskt och inkluderas i svaret.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `$id` | En URI som fungerar som en skrivskyddad, systemgenererad unik identifierare för den nya ad hoc-klassen. Det här värdet används i nästa steg när du skapar ett ad hoc-schema. |

## Skapa ett ad hoc-schema

När du har skapat en ad hoc-klass kan du skapa ett nytt schema som implementerar den klassen genom att göra en POST-begäran till `/tenant/schemas` slutpunkten.

**API-format**

```http
POST /tenant/schemas
```

**Begäran**

Följande begäran skapar ett nytt schema som ger en referens (`$ref`) till `$id` den tidigare skapade ad hoc-klassen i dess nyttolast.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**Svar**

Ett lyckat svar returnerar information om det nyligen skapade schemat, inklusive dess systemgenererade, skrivskyddade `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## Se hela ad hoc-schemat

>[!NOTE]
>
>Det här steget är valfritt. Om du inte vill inspektera fältstrukturen i ditt ad hoc-schema kan du hoppa till [nästa steg](#next-steps) i slutet av kursen.

När ad hoc-schemat har skapats kan du göra en sökbegäran (GET) för att visa schemat i dess utökade form. Detta görs genom att använda rätt Accept-huvud i GET-begäran, vilket visas nedan.

**API-format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` det ad hoc-schema som du vill komma åt. |

**Begäran**

Följande begäran använder rubriken Godkänn `application/vnd.adobe.xed-full+json; version=1`som returnerar den utökade formen av schemat. Observera, att när en viss resurs hämtas från schemaregistret, måste begärans Accept-huvud innehålla en större version av resursen i fråga.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar information om schemat, inklusive alla fält som är kapslade under `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du skapat ett nytt ad hoc-schema. Om du kommer till det här dokumentet som en del av en annan självstudiekurs kan du nu använda `$id` ditt ad hoc-schema för att slutföra arbetsflödet enligt anvisningarna.

Mer information om hur du arbetar med API:t för schemaregister finns i [utvecklarhandboken](../api/getting-started.md).