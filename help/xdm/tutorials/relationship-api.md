---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;Experience data model;Experience data model;experience data model;data model;data model;schema register;schema Registry;schema;schema;scheman;scheman;scheman;schema;relation;relation;relation;relationsbeskrivare;relationsbeskrivare;referensidentitet;referensidentitet;
solution: Experience Platform
title: Definiera en relation mellan två scheman med API:t för schemaregister
description: Det här dokumentet innehåller en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med API:t för schemaregistret.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---


# Definiera en relation mellan två scheman med hjälp av API:t [!DNL Schema Registry]

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer inom strukturen för dina [!DNL Experience Data Model] (XDM)-scheman kan du få komplexa insikter i dina kunddata.

Schemarelationer kan härledas genom användning av unionsschemat och [!DNL Real-time Customer Profile], men detta gäller endast scheman som delar samma klass. Om du vill upprätta en relation mellan två scheman som tillhör olika klasser måste ett dedikerat relationsfält läggas till i ett källschema, som refererar till identiteten för ett målschema.

Det här dokumentet innehåller en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Komma igång

Den här självstudien kräver en fungerande förståelse för [!DNL Experience Data Model] (XDM) och [!DNL XDM System]. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM System i Experience Platform](../home.md): En översikt över XDM och dess implementering i  [!DNL Experience Platform].
   * [Grundläggande om schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Innan du startar den här självstudiekursen bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för viktig information som du behöver känna till för att kunna ringa anrop till API:t [!DNL Schema Registry]. Detta inkluderar din `{TENANT_ID}`, begreppet &quot;behållare&quot; och de huvuden som krävs för att göra förfrågningar (med särskild uppmärksamhet på [!DNL Accept]-huvudet och dess möjliga värden).

## Definiera en källa och ett målschema {#define-schemas}

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. Den här självstudien skapar en relation mellan medlemmar i ett företags aktuella lojalitetsprogram (definierat i ett [!DNL Loyalty Members]-schema) och deras favorithotell (definierade i ett [!DNL Hotels]-schema).

Schemarelationer representeras av ett **källschema** med ett fält som refererar till ett annat fält i ett **målschema**. I de följande stegen kommer &quot;[!DNL Loyalty Members]&quot; att vara källschemat, medan &quot;[!DNL Hotels]&quot; fungerar som målschema.

>[!IMPORTANT]
>
>För att kunna etablera en relation måste båda scheman ha definierade primära identiteter och vara aktiverade för [!DNL Real-time Customer Profile]. Se avsnittet [Aktivera ett schema för användning i profilen](./create-schema-api.md#profile) i självstudiekursen för att skapa schema om du behöver hjälp med hur du konfigurerar scheman därefter.

Om du vill definiera en relation mellan två scheman måste du först hämta `$id`-värdena för båda scheman. Om du känner till visningsnamnen (`title`) för scheman kan du hitta deras `$id`-värden genom att göra en GET-begäran till `/tenant/schemas`-slutpunkten i [!DNL Schema Registry]-API:t.

**API-format**

```http
GET /tenant/schemas
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>[!DNL Accept]-huvudet `application/vnd.adobe.xed-id+json` returnerar bara rubriker, ID:n och versioner av de resulterande scheman.

**Svar**

Ett lyckat svar returnerar en lista med scheman som definierats av din organisation, inklusive deras `name`, `$id`, `meta:altId` och `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

Registrera `$id`-värdena för de två scheman som du vill definiera en relation mellan. Dessa värden används i senare steg.

## Definiera ett referensfält för källschemat

I [!DNL Schema Registry] fungerar relationsbeskrivare på liknande sätt som sekundärnycklar i relationsdatabastabeller: ett fält i källschemat fungerar som en referens till det primära identitetsfältet i ett målschema. Om källschemat inte har något fält för detta ändamål, kan du behöva skapa en blandning med det nya fältet och lägga till det i schemat. Det nya fältet måste ha `type`-värdet [!DNL string].

>[!IMPORTANT]
>
>Till skillnad från målschemat kan källschemat inte använda sin primära identitet som referensfält.

I den här självstudiekursen innehåller målschemat [!DNL Hotels] ett `hotelId`-fält som fungerar som schemats primära identitet och fungerar därför även som referensfält. Källschemat [!DNL Loyalty Members] har emellertid inget dedikerat fält som ska användas som referens, och måste ges en ny blandning som lägger till ett nytt fält i schemat: `favoriteHotel`.

>[!NOTE]
>
>Om källschemat redan har ett dedikerat fält som du tänker använda som referensfält kan du hoppa fram till steget när du [skapar en referensbeskrivare](#reference-identity).

### Skapa en ny blandning

Om du vill lägga till ett nytt fält i ett schema måste det först definieras i en mixin. Du kan skapa en ny blandning genom att göra en POST-förfrågan till `/tenant/mixins`-slutpunkten.

**API-format**

```http
POST /tenant/mixins
```

**Begäran**

Följande begäran skapar en ny blandning som lägger till ett `favoriteHotel`-fält under namnutrymmet `_{TENANT_ID}` för alla scheman som det läggs till i.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**Svar**

Ett godkänt svar returnerar information om den nyligen skapade mixen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `$id` | Den skrivskyddade, systemgenererade unika identifieraren för den nya mixen. Tar formen av en URI. |

Registrera URI:n `$id` för mixinen, som ska användas i nästa steg när du lägger till mixinen i källschemat.

### Lägg till blandningen i källschemat

När du har skapat en blandning kan du lägga till den i källschemat genom att göra en PATCH-begäran till `/tenant/schemas/{SCHEMA_ID}`-slutpunkten.

**API-format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | URL-kodad `$id` URI eller `meta:altId` för källschemat. |

**Begäran**

Följande begäran lägger till blandningen [!DNL Favorite Hotel] i schemat [!DNL Loyalty Members].

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `op` | Den PATCH-åtgärd som ska utföras. Denna begäran använder åtgärden `add`. |
| `path` | Sökvägen till schemafältet där den nya resursen ska läggas till. När du lägger till blandningar i scheman måste värdet vara /allOf/-. |
| `value.$ref` | `$id` för den blandning som ska läggas till. |

**Svar**

Ett lyckat svar returnerar informationen om det uppdaterade schemat, som nu innehåller `$ref`-värdet för den tillagda mixin under dess `allOf`-array.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
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
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## Skapa en referensidentitetsbeskrivning {#reference-identity}

Schemafält måste ha en referensidentitetsbeskrivare om de används som referens från andra scheman i en relation. Eftersom `favoriteHotel`-fältet i [!DNL Loyalty Members] refererar till `hotelId`-fältet i [!DNL Hotels] måste `hotelId` ges en referensidentitetsbeskrivning.

Skapa en referensbeskrivning för målschemat genom att göra en POST-förfrågan till `/tenant/descriptors`-slutpunkten.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran skapar en referensbeskrivning för fältet `hotelId` i målschemat [!DNL Hotels].

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För referensbeskrivare måste värdet vara &quot;xdm:descriptorReferenceIdentity&quot;. |
| `xdm:sourceSchema` | Målschemats `$id`-URL. |
| `xdm:sourceVersion` | Målschemats versionsnummer. |
| `sourceProperty` | Sökvägen till målschemats primära identitetsfält. |
| `xdm:identityNamespace` | Referensfältets identitetsnamnområde. Detta måste vara samma namnutrymme som används när fältet definieras som schemats primära identitet. Mer information finns i [översikten över identitetsnamnrymden](../../identity-service/home.md). |

**Svar**

Ett lyckat svar returnerar information om den nya referensbeskrivningen för målschemat.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Skapa en relationsbeskrivning {#create-descriptor}

Relationsbeskrivare skapar en 1:1-relation mellan ett källschema och ett målschema. När du har definierat en referensbeskrivning för målschemat kan du skapa en ny relationsbeskrivning genom att göra en POST-förfrågan till slutpunkten `/tenant/descriptors`.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran skapar en ny relationsbeskrivare med &quot;[!DNL Loyalty Members]&quot; som källschema och &quot;[!DNL Legacy Loyalty Members]&quot; som målschema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som ska skapas. Värdet `@type` för relationsbeskrivare är &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | URL:en `$id` för källschemat. |
| `xdm:sourceVersion` | Källschemats versionsnummer. |
| `xdm:sourceProperty` | Sökvägen till referensfältet i källschemat. |
| `xdm:destinationSchema` | Målschemats `$id`-URL. |
| `xdm:destinationVersion` | Målschemats versionsnummer. |
| `xdm:destinationProperty` | Sökvägen till referensfältet i målschemat. |

### Svar

Ett lyckat svar returnerar information om den nyligen skapade relationsbeskrivningen.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## Nästa steg

I den här självstudiekursen har du skapat en 1:1-relation mellan två scheman. Mer information om hur du arbetar med beskrivningar med API:t [!DNL Schema Registry] finns i [Utvecklarhandbok för schemaregister](../api/descriptors.md). Anvisningar om hur du definierar schemarelationer i användargränssnittet finns i självstudiekursen om att [definiera schemarelationer med Schemaredigeraren](relationship-ui.md).
