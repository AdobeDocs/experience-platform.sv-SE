---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;relationship;Relationship;relationship descriptor;Relationship descriptor;reference identity;Reference identity;
solution: Experience Platform
title: Definiera en relation mellan två scheman med API:t för schemaregister
description: Det här dokumentet innehåller en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med API:t för schemaregistret.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---


# Definiera en relation mellan två scheman med hjälp av [!DNL Schema Registry] API:t

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer inom strukturen för era [!DNL Experience Data Model] (XDM) scheman kan ni få komplexa insikter i era kunddata.

Schemarelationer kan härledas genom användning av unionsschemat och [!DNL Real-time Customer Profile]detta gäller endast scheman som delar samma klass. Om du vill upprätta en relation mellan två scheman som tillhör olika klasser måste ett dedikerat relationsfält läggas till i ett källschema, som refererar till identiteten för ett målschema.

Det här dokumentet innehåller en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med hjälp av [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av [!DNL Experience Data Model] (XDM) och [!DNL XDM System]. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM System i Experience Platform](../home.md): En översikt över XDM och dess implementering i [!DNL Experience Platform].
   * [Grundläggande om schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Innan du startar den här självstudiekursen bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till [!DNL Schema Registry] API:t. Detta inkluderar ditt `{TENANT_ID}`, konceptet med&quot;behållare&quot; och de rubriker som krävs för att göra förfrågningar (med särskild uppmärksamhet på [!DNL Accept] rubriken och dess möjliga värden).

## Definiera en källa och ett målschema {#define-schemas}

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. Den här självstudien skapar en relation mellan medlemmar i ett företags aktuella lojalitetsprogram (definieras i ett&quot;[!DNL Loyalty Members]&quot; schema) och deras favorithotell (definieras i ett&quot;[!DNL Hotels]&quot;-schema).

Schemarelationer representeras av ett **källschema** med ett fält som refererar till ett annat fält i ett **målschema**. I de följande stegen blir &quot;[!DNL Loyalty Members]&quot; källschemat, medan &quot;[!DNL Hotels]&quot; fungerar som målschema.

>[!IMPORTANT]
>
>För att upprätta en relation måste båda scheman ha definierade primära identiteter och aktiveras för [!DNL Real-time Customer Profile]. Se avsnittet om [aktivering av ett schema för användning i profil](./create-schema-api.md#profile) i självstudiekursen för att skapa schema om du behöver hjälp med att konfigurera scheman därefter.

Om du vill definiera en relation mellan två scheman måste du först hämta `$id` värdena för båda scheman. Om du känner till visningsnamnen (`title`) för scheman kan du hitta deras `$id` värden genom att göra en GET-begäran till `/tenant/schemas` slutpunkten i [!DNL Schema Registry] API:t.

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
>Rubriken [!DNL Accept] `application/vnd.adobe.xed-id+json` returnerar bara rubriker, ID:n och versioner av de resulterande scheman.

**Svar**

Ett godkänt svar returnerar en lista med scheman som definierats av organisationen, inklusive deras `name`, `$id`, `meta:altId`och `version`.

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

Registrera `$id` värdena för de två scheman som du vill definiera en relation mellan. Dessa värden används i senare steg.

## Definiera ett referensfält för källschemat

I [!DNL Schema Registry]fungerar relationsbeskrivningarna på liknande sätt som sekundärnycklar i relationsdatabastabeller: ett fält i källschemat fungerar som en referens till det primära identitetsfältet i ett målschema. Om källschemat inte har något fält för detta ändamål, kan du behöva skapa en blandning med det nya fältet och lägga till det i schemat. Det nya fältet måste ha `type` värdet &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>Till skillnad från målschemat kan källschemat inte använda sin primära identitet som referensfält.

I den här självstudiekursen innehåller målschemat&quot;[!DNL Hotels]&quot; ett `email` fält som fungerar som schemats primära identitet och fungerar därför även som referensfält. Källschemat &quot;[!DNL Loyalty Members]&quot; har emellertid inget dedikerat fält som ska användas som referens och måste ges en ny blandning som lägger till ett nytt fält i schemat: `favoriteHotel`.

>[!NOTE]
>
>Om källschemat redan har ett dedikerat fält som du tänker använda som referensfält kan du hoppa till steget när du [skapar en referensbeskrivning](#reference-identity).

### Skapa en ny blandning

Om du vill lägga till ett nytt fält i ett schema måste det först definieras i en mixin. Du kan skapa en ny blandning genom att göra en POST-förfrågan till `/tenant/mixins` slutpunkten.

**API-format**

```http
POST /tenant/mixins
```

**Begäran**

Följande begäran skapar en ny blandning som lägger till ett `favoriteHotel` fält under `_{TENANT_ID}` namnutrymmet för det schema som det läggs till i.

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

Registrera `$id` URI:n för den blandning som ska användas i nästa steg när du lägger till mixinen i källschemat.

### Lägg till blandningen i källschemat

När du har skapat en blandning kan du lägga till den i källschemat genom att göra en PATCH-begäran till `/tenant/schemas/{SCHEMA_ID}` slutpunkten.

**API-format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` källschemat. |

**Begäran**

Följande begäran lägger till&quot;[!DNL Favorite Hotel]&quot;-blandningen i&quot;[!DNL Loyalty Members]&quot;-schemat.

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
| `op` | Den PATCH-åtgärd som ska utföras. Den här begäran använder `add` åtgärden. |
| `path` | Sökvägen till schemafältet där den nya resursen ska läggas till. När du lägger till blandningar i scheman måste värdet vara /allOf/-. |
| `value.$ref` | The `$id` of the mixin to be added. |

**Svar**

Ett lyckat svar returnerar detaljerna i det uppdaterade schemat, som nu inkluderar värdet `$ref` för den tillagda mixin under dess `allOf` array.

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

## Skapa en beskrivning av en referensidentitet {#reference-identity}

Schemafält måste ha en referensidentitetsbeskrivare om de används som referens från andra scheman i en relation. Eftersom `favoriteHotel` fältet i &quot;[!DNL Loyalty Members]&quot; refererar till `email` fältet i &quot;[!DNL Hotels]&quot;, måste du `email` ange en referensidentitetsbeskrivning.

Skapa en referensbeskrivning för målschemat genom att göra en POST-förfrågan till `/tenant/descriptors` slutpunkten.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran skapar en referensbeskrivning för `email` fältet i målschemat &quot;[!DNL Hotels]&quot;.

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
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email"
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För referensbeskrivare måste värdet vara &quot;xdm:descriptorReferenceIdentity&quot;. |
| `xdm:sourceSchema` | Målschemats `$id` URL. |
| `xdm:sourceVersion` | Målschemats versionsnummer. |
| `sourceProperty` | Sökvägen till målschemats primära identitetsfält. |
| `xdm:identityNamespace` | Referensfältets identitetsnamnområde. Detta måste vara samma namnutrymme som används när fältet definieras som schemats primära identitet. Mer information finns i [översikten](../../identity-service/home.md) över identitetsnamnen. |

**Svar**

Ett lyckat svar returnerar information om den nya referensbeskrivningen för målschemat.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Skapa en relationsbeskrivning {#create-descriptor}

Relationsbeskrivare skapar en 1:1-relation mellan ett källschema och ett målschema. När du har definierat en referensbeskrivning för målschemat kan du skapa en ny relationsbeskrivning genom att göra en POST-förfrågan till `/tenant/descriptors` slutpunkten.

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
    "xdm:destinationProperty": "/_{TENANT_ID}/email"
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som ska skapas. Värdet `@type` för relationsbeskrivare är &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | Källschemats `$id` URL. |
| `xdm:sourceVersion` | Källschemats versionsnummer. |
| `xdm:sourceProperty` | Sökvägen till referensfältet i källschemat. |
| `xdm:destinationSchema` | Målschemats `$id` URL. |
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

I den här självstudiekursen har du skapat en 1:1-relation mellan två scheman. Mer information om hur du arbetar med beskrivningar med API:t finns i utvecklarhandboken för [!DNL Schema Registry] schemaregister [](../api/descriptors.md). Anvisningar om hur du definierar schemarelationer i användargränssnittet finns i självstudiekursen om hur du [definierar schemarelationer med Schemaredigeraren](relationship-ui.md).
