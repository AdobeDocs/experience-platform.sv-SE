---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definiera en relation mellan två scheman med API:t för schemaregister
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 0%

---


# Definiera en relation mellan två scheman med hjälp av [!DNL Schema Registry] API:t


Möjligheten att förstå relationen mellan era kunder och deras interaktioner med ert varumärke i olika kanaler är en viktig del av Adobe Experience Platform. Genom att definiera dessa relationer inom strukturen för era [!DNL Experience Data Model] (XDM) scheman kan ni få komplexa insikter i era kunddata.

Det här dokumentet innehåller en självstudiekurs för att definiera en 1:1-relation mellan två scheman som definierats av din organisation med hjälp av [!DNL Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av [!DNL Experience Data Model] (XDM) och [!DNL XDM System]. Läs följande dokumentation innan du börjar den här självstudiekursen:

* [XDM System i Experience Platform](../home.md): En översikt över XDM och dess implementering i Experience Platform.
   * [Grundläggande om schemakomposition](../schema/composition.md): En introduktion av byggstenarna i XDM-scheman.
* [!DNL Real-time Customer Profile](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Innan du startar den här självstudiekursen bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till [!DNL Schema Registry] API:t. Detta inkluderar ditt `{TENANT_ID}`, konceptet med&quot;behållare&quot; och de rubriker som krävs för att göra förfrågningar (med särskild uppmärksamhet på rubriken Godkänn och dess möjliga värden).

## Definiera en källa och ett målschema {#define-schemas}

Du förväntas redan ha skapat de två scheman som ska definieras i relationen. Den här självstudien skapar en relation mellan medlemmar i ett företags aktuella lojalitetsprogram (som definieras i ett&quot;Loyalty Members&quot;-schema) och deras favorithotell (som definieras i ett&quot;Hotels&quot;-schema).

Schemarelationer representeras av ett fält **[!UICONTROL source schema]** som refererar till ett annat fält i ett **[!UICONTROL destination schema]**. I de följande stegen blir &quot;[!UICONTROL Loyalty Members]&quot; källschemat, medan &quot;[!UICONTROL Hotels]&quot; fungerar som målschema.

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
>Rubriken Acceptera `application/vnd.adobe.xed-id+json` returnerar endast rubriker, ID:n och versioner av de resulterande scheman.

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

## Definiera referensfält för båda scheman

I [!DNL Schema Registry]fungerar relationsbeskrivningarna på liknande sätt som sekundärnycklar i SQL-tabeller: ett fält i källschemat fungerar som en referens till ett fält i ett målschema. När du definierar en relation måste varje schema ha ett dedikerat fält som ska användas som referens till det andra schemat.

>[!IMPORTANT]
>
>Om scheman ska aktiveras för användning i [!DNL Real-time Customer Profile](../../profile/home.md)måste referensfältet för målschemat vara dess **[!UICONTROL primary identity]**. Detta förklaras mer ingående senare i den här självstudiekursen.

Om något av schemana inte har något fält för detta ändamål, kan du behöva skapa en blandning med det nya fältet och lägga till det i schemat. Det nya fältet måste ha `type` värdet &quot;string&quot;.

I den här självstudiekursen innehåller målschemat &quot;Hotels&quot; redan ett fält för detta ändamål: `hotelId`. Källschemat &quot;Loyalty Members&quot; har dock inget sådant fält och måste få en ny blandning som lägger till ett nytt fält `favoriteHotel`under `TENANT_ID` namnutrymmet.

### Skapa en ny blandning

Om du vill lägga till ett nytt fält i ett schema måste det först definieras i en mixin. Du kan skapa en ny blandning genom att göra en POST-begäran till `/tenant/mixins` slutpunkten.

**API-format**

```http
POST /tenant/mixins
```

**Begäran**

Följande begäran skapar en ny blandning som lägger till ett `favoriteHotel` fält under `TENANT_ID` namnutrymmet för det schema som det läggs till i.

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

Följande begäran lägger till blandningen &quot;Favorite Hotel&quot; i schemat &quot;Loyalty Members&quot;.

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
| `op` | PATCH-åtgärden som ska utföras. Den här begäran använder `add` åtgärden. |
| `path` | Sökvägen till schemafältet där den nya resursen ska läggas till. När du lägger till blandningar i scheman måste värdet vara `/allOf/-`. |
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

## Definiera primära identitetsfält för båda scheman

>[!NOTE]
>
>Det här steget krävs bara för scheman som ska aktiveras för användning i [!DNL Real-time Customer Profile](../../profile/home.md). Om du inte vill att schemat ska ingå i en union, eller om dina scheman redan har primära identiteter definierade, kan du hoppa till nästa steg när du [skapar en referensidentitetsbeskrivning](#create-descriptor) för målschemat.

För att scheman ska kunna aktiveras för användning i måste [!DNL Real-time Customer Profile]de ha en primär identitet definierad. Dessutom måste en relations målschema använda sin primära identitet som referensfält.

I den här självstudiekursen har källschemat redan en primär identitet definierad, men målschemat har inte det. Du kan markera ett schemafält som ett primärt identitetsfält genom att skapa en identitetsbeskrivning. Detta görs genom att en POST-begäran görs till `/tenant/descriptors` slutpunkten.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran skapar en ny identitetsbeskrivning som definierar fältet `hotelId` i målschemat &quot;Hotels&quot; som ett primärt identitetsfält.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som ska skapas. Värdet `@type` för identitetsbeskrivningar är `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | Värdet `$id` för målschemat, som hämtades i [föregående steg](#define-schemas). |
| `xdm:sourceVersion` | Versionsnumret för schemat. |
| `sourceProperty` | Sökvägen till det specifika fält som ska fungera som schemats primära identitet. Den här sökvägen ska börja med ett &quot;/&quot; och inte sluta med ett, men inte med något &quot;properties&quot;-namnutrymme. I begäran ovan används till exempel `/_{TENANT_ID}/hotelId` istället för `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | Identitetsnamnområdet för identitetsfältet. `hotelId` är ett ECID-värde i det här exemplet och därför används namnutrymmet&quot;ECID&quot;. En lista över tillgängliga namnutrymmen finns i översikten [över](../../identity-service/home.md) identitetsnamnutrymmet. |
| `xdm:isPrimary` | En boolesk egenskap som avgör om identitetsfältet kommer att vara schemats primära identitet. Eftersom den här begäran definierar en primär identitet anges värdet till true. |

**Svar**

Ett godkänt svar returnerar information om den nyligen skapade identitetsbeskrivningen.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## Skapa en beskrivning av en referensidentitet

Schemafält måste ha en referensidentitetsbeskrivare om de används som referens från andra scheman i en relation. Eftersom `favoriteHotel` fältet i &quot;Lojalitetsmedlemmar&quot; refererar till `hotelId` fältet i &quot;Hotels&quot;, `hotelId` måste det anges en referensidentitetsbeskrivning.

Skapa en referensbeskrivning för målschemat genom att göra en POST-begäran till `/tenant/descriptors` slutpunkten.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran skapar en referensbeskrivning för `hotelId` fältet i målschemat &quot;Hotels&quot;.

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
    "xdm:identityNamespace": "ECID"
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `xdm:sourceSchema` | Målschemats `$id` URL. |
| `xdm:sourceVersion` | Målschemats versionsnummer. |
| `sourceProperty` | Sökvägen till målschemats primära identitetsfält. |
| `xdm:identityNamespace` | Referensfältets identitetsnamnområde. `hotelId` är ett ECID-värde i det här exemplet och därför används namnutrymmet&quot;ECID&quot;. En lista över tillgängliga namnutrymmen finns i översikten [över](../../identity-service/home.md) identitetsnamnutrymmet. |

**Svar**

Ett lyckat svar returnerar information om den nya referensbeskrivningen för målschemat.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Skapa en relationsbeskrivning {#create-descriptor}

Relationsbeskrivare skapar en 1:1-relation mellan ett källschema och ett målschema. Du kan skapa en ny relationsbeskrivare genom att göra en POST-begäran till `/tenant/descriptors` slutpunkten.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

I följande begäran skapas en ny relationsbeskrivare, med&quot;lojalitetsmedlemmar&quot; som källschema och&quot;Äldre lojalitetsmedlemmar&quot; som målschema.

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
| `@type` | Den typ av beskrivning som ska skapas. Värdet `@type` för relationsbeskrivare är `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | Källschemats `$id` URL. |
| `xdm:sourceVersion` | Källschemats versionsnummer. |
| `sourceProperty`: | Sökvägen till referensfältet i källschemat. |
| `xdm:destinationSchema` | Målschemats `$id` URL. |
| `xdm:destinationVersion` | Målschemats versionsnummer. |
| `destinationProperty`: | Sökvägen till referensfältet i målschemat. |

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

I den här självstudiekursen har du skapat en 1:1-relation mellan två scheman. Mer information om hur du arbetar med beskrivningar med API:t finns i utvecklarhandboken för [!DNL Schema Registry] schemaregister [](../api/getting-started.md). Anvisningar om hur du definierar schemarelationer i användargränssnittet finns i självstudiekursen om hur du [definierar schemarelationer med Schemaredigeraren](relationship-ui.md).