---
title: Lägg till specifika fält i ett schema med API:t för schemaregistret
description: Lär dig hur du lägger till enskilda fält från befintliga fältgrupper i ett XDM-schema (Experience Data Model) med API:t för schemaregistret.
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Lägga till specifika fält i ett schema med API:t för schemaregister

XDM-scheman (Experience Data Model) består av en basklass, där ytterligare fält inkluderas genom användning av standardfältgrupper som definieras av Adobe och anpassade fältgrupper som definieras av organisationen.

När du skapar ett schema kanske du vill använda vissa fält från en viss fältgrupp och utesluta andra från samma grupp som du inte behöver. I den här självstudiekursen visas hur du lägger till enskilda fält från en fältgrupp i ett schema med API:t för schemaregister.

>[!NOTE]
>
>Mer information om hur du lägger till och tar bort enskilda schemafält i användargränssnittet i Adobe Experience Platform finns i handboken om [fältbaserade arbetsflöden](../ui/field-based-workflows.md) (som för närvarande finns i betaversionen).

## Förhandskrav

I den här självstudiekursen görs anrop till [API:t för schemaregister](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Innan du startar bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för att få viktig information som du behöver känna till för att kunna anropa API:t, inklusive `{TENANT_ID}`, behållarkonceptet och de rubriker som krävs för att göra förfrågningar.

## Om fältet `meta:refProperty`

För varje givet schema refereras den klass och fältgrupper som utgör dess struktur under dess `allOf`-matris. Varje komponent representeras som ett objekt som innehåller en `$ref`-egenskap som refererar till komponentens URI `$id`.

Följande JSON representerar ett förenklat schema som använder en enda klass (`experienceevent`) och fältgrupp (`experienceevent-all`):

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

För alla objekt i `allOf`-arrayen som refererar till en fältgrupp kan du lägga till ett `meta:refProperty`-fält på samma nivå för att ange vilka fält i gruppen som ska inkluderas i schemat.

>[!NOTE]
>
>Varje fält anges med en JSON-pekarsträng, som representerar sökvägen till fältet i dess respektive fältgrupp. Strängen måste börja med ett inledande snedstreck (`/`) och får inte innehålla några `properties`-namnutrymmen. Till exempel: `/_experience/campaign/message/id`.

När `meta:refProperty` inkluderas som en sträng kan den referera till ett enskilt fält i en grupp. Andra fält från samma grupp kan inkluderas genom att använda samma `$ref`-värde i ett annat objekt med ett annat `meta:refProperty`-värde.

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

Alternativt kan `meta:refProperty` anges som en array, så att du kan ange flera fält som ska inkluderas från en viss grupp i ett enskilt `allOf`-listobjekt:

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## Lägga till fält med en PUT-åtgärd

Du kan använda en PUT-begäran för att skriva om ett helt schema och konfigurera fälten som du vill inkludera under `allOf`.

**API-format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` eller URL-kodad `$id` för schemat som du vill skriva om. |

**Begäran**

Följande begäran uppdaterar de specifika fält som ingår i fältgruppen under arrayen `allOf`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**Svar**

Ett lyckat svar returnerar information om det uppdaterade schemat.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Mer detaljerad information om schemaförfrågningar från PUT finns i [schemas slutpunktshandbok](../api/schemas.md#put).

## Lägga till fält med en PATCH-åtgärd

Du kan använda en PATCH-begäran för att lägga till enskilda fält i ett schema utan att skriva över andra. Schemaregistret stöder alla JSON-korrigeringsåtgärder som är standard, inklusive `add`, `remove` och `replace`. Mer information om JSON Patch finns i guiden [Grundläggande API](../../landing/api-fundamentals.md#json-patch).

**API-format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` eller URL-kodad `$id` för schemat som du vill skriva om. |

**Begäran**

Följande begäran lägger till ett nytt objekt i schemats `allOf`-matris och anger de fält som ska läggas till.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**Svar**

Ett lyckat svar returnerar information om det uppdaterade schemat.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Mer detaljerad information om schemaförfrågningar från PATCH finns i [schemas slutpunktshandbok](../api/schemas.md#patch).

## Nästa steg

I den här guiden beskrivs hur du använder API-anrop för att lägga till enskilda fält från en befintlig fältgrupp i ett schema. Mer information om hur du utför liknande fältbaserade åtgärder i plattformsgränssnittet finns i handboken om [fältbaserade arbetsflöden](../ui/field-based-workflows.md).

Mer information om funktionerna i API:t för schemaregister finns i [API-översikten](../api/overview.md) för en fullständig lista över slutpunkter och processer.
