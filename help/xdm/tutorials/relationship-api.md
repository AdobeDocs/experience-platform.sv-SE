---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;Experience data model;Experience data model;experience data model;data model;data model;schema register;schema Registry;schema;schema;scheman;scheman;scheman;schema;relation;relation;relation;relationsbeskrivare;relationsbeskrivare;referensidentitet;referensidentitet;
title: Definiera en relation mellan två scheman med API:t för schemaregister
description: Det här dokumentet innehåller en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med API:t för schemaregistret.
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# Definiera en relation mellan två scheman med [!DNL Schema Registry] API

Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Definiera dessa relationer inom strukturen för din [!DNL Experience Data Model] (XDM)-scheman gör att ni kan få komplexa insikter om era kunddata.

När schemarelationer kan härledas genom användning av unionsschemat och [!DNL Real-Time Customer Profile]gäller detta endast scheman som delar samma klass. För att upprätta en relation mellan två scheman som tillhör olika klasser måste ett dedikerat relationsfält läggas till i en **källschema**, som anger identiteten för en separat **referensschema**.

>[!NOTE]
>
>API:t för schemaregister refererar till referensscheman som&quot;målscheman&quot;. Dessa ska inte blandas ihop med målscheman i [Uppsättningar för datapunktsmappning](../../data-prep/mapping-set.md) eller scheman för [målanslutningar](../../destinations/home.md).

Det här dokumentet innehåller en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av [!DNL Experience Data Model] (XDM) och [!DNL XDM System]. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM-system i Experience Platform](../home.md): En översikt över XDM och dess implementering i [!DNL Experience Platform].
   * [Grunderna för schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Innan du startar den här självstudiekursen bör du gå igenom [utvecklarhandbok](../api/getting-started.md) för viktig information som du behöver känna till för att kunna ringa [!DNL Schema Registry] API. Detta inkluderar `{TENANT_ID}`, begreppet &quot;behållare&quot; och de rubriker som krävs för att göra en förfrågan (med särskild uppmärksamhet på [!DNL Accept] header och dess möjliga värden).

## Definiera en källa och ett referensschema {#define-schemas}

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. Den här självstudien skapar en relation mellan medlemmar i en organisations aktuella lojalitetsprogram (definieras i en[!DNL Loyalty Members]&quot; schema) och deras favorithotell (definieras i en[!DNL Hotels]&quot; schema).

Schemarelationer representeras av en **källschema** ha ett fält som refererar till ett annat fält i ett **referensschema**. I följande steg: &quot;[!DNL Loyalty Members]&quot; blir källschemat, medan &quot;[!DNL Hotels]&quot; fungerar som referensschema.

>[!IMPORTANT]
>
>För att upprätta en relation måste båda scheman ha definierade primära identiteter och vara aktiverade för [!DNL Real-Time Customer Profile]. Se avsnittet om [aktivera ett schema för användning i profil](./create-schema-api.md#profile) i självstudiekursen för att skapa scheman om du behöver hjälp med att konfigurera dina scheman därefter.

Om du vill definiera en relation mellan två scheman måste du först skaffa `$id` värden för båda scheman. Om du känner till visningsnamnen (`title`) av scheman kan du hitta deras `$id` genom att göra en GET-förfrågan till `/tenant/schemas` slutpunkt i [!DNL Schema Registry] API.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>The [!DNL Accept] header `application/vnd.adobe.xed-id+json` returnerar bara rubriker, ID:n och versioner av de resulterande scheman.

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

Spela in `$id` värden för de två scheman som du vill definiera en relation mellan. Dessa värden används i senare steg.

## Definiera ett referensfält för källschemat

I [!DNL Schema Registry]fungerar relationsbeskrivare på liknande sätt som sekundärnycklar i relationsdatabastabeller: ett fält i källschemat fungerar som en referens till det primära identitetsfältet i ett referensschema. Om källschemat inte har något fält för detta ändamål, kan du behöva skapa en schemafältgrupp med det nya fältet och lägga till den i schemat. Det nya fältet måste ha en `type` värde för `string`.

>[!IMPORTANT]
>
>Källschemat kan inte använda sin primära identitet som referensfält.

I den här självstudiekursen finns referensschemat &quot;[!DNL Hotels]&quot; innehåller `hotelId` fält som fungerar som schemats primära identitet. Källschemat[!DNL Loyalty Members]&quot; har inget dedikerat fält att använda som referens till `hotelId`och därför måste en anpassad fältgrupp skapas för att ett nytt fält ska kunna läggas till i schemat: `favoriteHotel`.

>[!NOTE]
>
>Om källschemat redan har ett dedikerat fält som du tänker använda som referensfält kan du hoppa fram till steget på [skapa en referensbeskrivning](#reference-identity).

### Skapa en ny fältgrupp

Om du vill lägga till ett nytt fält i ett schema måste det först definieras i en fältgrupp. Du kan skapa en ny fältgrupp genom att göra en POST-förfrågan till `/tenant/fieldgroups` slutpunkt.

**API-format**

```http
POST /tenant/fieldgroups
```

**Begäran**

Följande begäran skapar en ny fältgrupp som lägger till en `favoriteHotel` fält under `_{TENANT_ID}` namnområde för alla scheman som det läggs till i.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
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

Ett godkänt svar returnerar information om den nyligen skapade fältgruppen.

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
    "description": "Favorite hotel field group for the Loyalty Members schema.",
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
| `$id` | Den skrivskyddade, systemgenererade unika identifieraren för den nya fältgruppen. Tar formen av en URI. |

{style=&quot;table-layout:auto&quot;}

Spela in `$id` URI för fältgruppen, som ska användas i nästa steg när fältgruppen läggs till i källschemat.

### Lägg till fältgruppen i källschemat

När du har skapat en fältgrupp kan du lägga till den i källschemat genom att göra en PATCH-begäran i `/tenant/schemas/{SCHEMA_ID}` slutpunkt.

**API-format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | URL-kodad `$id` URI eller `meta:altId` för källschemat. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran lägger till &quot;[!DNL Favorite Hotel]fältgrupp till[!DNL Loyalty Members]schemat.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Den PATCH-åtgärd som ska utföras. Den här begäran använder `add` operation. |
| `path` | Sökvägen till schemafältet där den nya resursen ska läggas till. När du lägger till fältgrupper i scheman måste värdet vara /allOf/-. |
| `value.$ref` | The `$id` för den fältgrupp som ska läggas till. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar informationen om det uppdaterade schemat, som nu innehåller `$ref` värdet för den tillagda fältgruppen under dess `allOf` array.

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
    "imsOrg": "{ORG_ID}",
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

Schemafält måste ha en referensidentitetsbeskrivning tillämpad på dem om de används som referens till ett annat schema i en relation. Sedan `favoriteHotel` fält i &quot;[!DNL Loyalty Members]&quot; kommer att referera till `hotelId` fält i &quot;[!DNL Hotels]&quot;, `favoriteHotel` måste anges som en referensidentitetsbeskrivning.

Skapa en referensbeskrivning för källschemat genom att göra en POST-förfrågan till `/tenant/descriptors` slutpunkt.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran skapar en referensbeskrivning för `favoriteHotel` i källschemat[!DNL Loyalty Members]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För referensbeskrivare måste värdet vara `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | The `$id` Källschemats URL. |
| `xdm:sourceVersion` | Källschemats versionsnummer. |
| `sourceProperty` | Sökvägen till fältet i källschemat som ska användas för att referera till referensschemats primära identitet. |
| `xdm:identityNamespace` | Referensfältets identitetsnamnområde. Detta måste vara samma namnutrymme som referensschemats primära identitet. Se [Översikt över namnutrymmet identity](../../identity-service/home.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar information om den nya referensbeskrivningen för källfältet.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Skapa en relationsbeskrivning {#create-descriptor}

Relationsbeskrivare skapar en 1:1-relation mellan ett källschema och ett referensschema. När du har definierat en referensidentitetsbeskrivning för rätt fält i källschemat kan du skapa en ny relationsbeskrivning genom att göra en POST-förfrågan till `/tenant/descriptors` slutpunkt.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran skapar en ny relationsbeskrivning med &quot;[!DNL Loyalty Members]&quot; som källschema och &quot;[!DNL Hotels]&quot; som referensschema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `@type` | Den typ av beskrivning som ska skapas. The `@type` värdet för relationsbeskrivningar är `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | The `$id` Källschemats URL. |
| `xdm:sourceVersion` | Källschemats versionsnummer. |
| `xdm:sourceProperty` | Sökvägen till referensfältet i källschemat. |
| `xdm:destinationSchema` | The `$id` URL för referensschemat. |
| `xdm:destinationVersion` | Referensschemats versionsnummer. |
| `xdm:destinationProperty` | Sökvägen till det primära identitetsfältet i referensschemat. |

{style=&quot;table-layout:auto&quot;}

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

I den här självstudiekursen har du skapat en 1:1-relation mellan två scheman. Mer information om hur du arbetar med beskrivningar med [!DNL Schema Registry] API, se [Utvecklarhandbok för schemaregister](../api/descriptors.md). Anvisningar om hur du definierar schemarelationer i användargränssnittet finns i självstudiekursen om [definiera schemarelationer med Schemaredigeraren](relationship-ui.md).
