---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;Experience data model;Experience data model;data model;data model;schema register;schema Registry;ad hoc;adhoc;adhoc;ad hoc;adhoc;adhoc;Adhoc;tutorial;Tutorial;create;create;schema;schema
solution: Experience Platform
title: Skapa ett ad hoc-schema
description: Under särskilda omständigheter kan det vara nödvändigt att skapa ett XDM-schema (Experience Data Model) med fält som bara namnges av en enda datauppsättning. Detta kallas för ett ad hoc-schema. Ad-hoc-scheman används i olika arbetsflöden för dataöverföring för Experience Platform, inklusive inhämtning av CSV-filer och skapande av vissa typer av källanslutningar.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Skapa ett ad hoc-schema

Under särskilda omständigheter kan det vara nödvändigt att skapa ett [!DNL Experience Data Model] (XDM)-schema med fält som bara får namnges av en enda datauppsättning. Detta kallas för ett ad hoc-schema. Ad-hoc-scheman används i olika arbetsflöden för dataöverföring för [!DNL Experience Platform], inklusive inhämtning av CSV-filer och skapande av vissa typer av källanslutningar.

Det här dokumentet innehåller allmänna steg för att skapa ett ad hoc-schema med [API:t för schemaregister](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Den är avsedd att användas tillsammans med andra [!DNL Experience Platform] självstudiekurser som kräver att ett ad hoc-schema skapas som en del av arbetsflödet. Var och en av dessa dokument innehåller detaljerad information om hur man konfigurerar ett ad hoc-schema för sitt specifika användningsfall.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för [!DNL Experience Data Model] (XDM) System. Läs följande XDM-dokumentation innan du startar den här självstudiekursen:

- [XDM-systemöversikt](../home.md): En översikt på hög nivå över XDM och dess implementering i [!DNL Experience Platform].
- [Grundläggande om schemakomposition](../schema/composition.md): En översikt över de grundläggande komponenterna i XDM-scheman.

Innan du startar den här självstudiekursen bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t för [!DNL Schema Registry]. Detta inkluderar din `{TENANT_ID}`, konceptet med behållare och de huvuden som krävs för att göra förfrågningar (med särskild uppmärksamhet på huvudet Godkänn och dess möjliga värden).

## Skapa en ad hoc-klass

Databeteendet för ett XDM-schema bestäms av dess underliggande klass. Det första steget i att skapa ett ad hoc-schema är att skapa en klass baserat på `adhoc`-beteendet. Detta görs genom att en POST begärs till slutpunkten `/tenant/classes`.

**API-format**

```http
POST /tenant/classes
```

**Begäran**

Följande begäran skapar en ny XDM-klass, konfigurerad med attributen som anges i nyttolasten. Genom att ange en `$ref`-egenskap som är inställd på `https://ns.adobe.com/xdm/data/adhoc` i arrayen `allOf` ärver den här klassen beteendet `adhoc`. Begäran definierar också ett `_adhoc`-objekt, som innehåller anpassade fält för klassen.

>[!NOTE]
>
>De anpassade fälten som definieras under `_adhoc` varierar beroende på hur ad hoc-schemat används. Se det specifika arbetsflödet i rätt självstudiekurs för obligatoriska anpassade fält baserat på användningsfall.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `$ref` | Databeteendet för den nya klassen. För ad hoc-klasser måste värdet anges till `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Ett objekt som innehåller anpassade fält för klassen, uttryckt som nyckelvärdepar med fältnamn och datatyper. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar informationen om den nya klassen och ersätter `properties._adhoc`-objektets namn med ett GUID som är en systemgenererad, skrivskyddad unik identifierare för klassen. Attributet `meta:datasetNamespace` genereras också automatiskt och inkluderas i svaret.

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
    "imsOrg": "{ORG_ID}",
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

{style="table-layout:auto"}

## Skapa ett ad hoc-schema

När du har skapat en ad hoc-klass kan du skapa ett nytt schema som implementerar den klassen genom att göra en POST-förfrågan till slutpunkten `/tenant/schemas`.

**API-format**

```http
POST /tenant/schemas
```

**Begäran**

Följande begäran skapar ett nytt schema som ger en referens (`$ref`) till `$id` för den tidigare skapade ad hoc-klassen i dess nyttolast.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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
>Det här steget är valfritt. Om du inte vill inspektera fältstrukturen i ditt ad hoc-schema kan du hoppa till avsnittet [Nästa steg](#next-steps) i slutet av den här självstudiekursen.

När ad hoc-schemat har skapats kan du göra en sökning (GET)-begäran för att visa schemat i dess utökade form. Detta görs genom att använda rätt Accept-huvud i GET-begäran, vilket visas nedan.

**API-format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | Den URL-kodade `$id` URI eller `meta:altId` för det ad hoc-schema som du vill komma åt. |

{style="table-layout:auto"}

**Begäran**

Följande begäran använder huvudet Godkänn `application/vnd.adobe.xed-full+json; version=1`, som returnerar den utökade formen av schemat. Observera, att när en specifik resurs hämtas från [!DNL Schema Registry] måste begärans Accept-huvud innehålla en större version av resursen i fråga.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Genom att följa den här självstudiekursen har du skapat ett nytt ad hoc-schema. Om du kommer till det här dokumentet som en del av en annan självstudiekurs kan du nu använda `$id` i ditt ad hoc-schema för att slutföra arbetsflödet enligt instruktionerna.

Mer information om hur du arbetar med API:t [!DNL Schema Registry] finns i [utvecklarhandboken](../api/getting-started.md).
