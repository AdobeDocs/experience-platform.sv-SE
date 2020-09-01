---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;union;Union;unions;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Unions
description: Unioner (eller unionsvyer) är systemgenererade, skrivskyddade scheman som sammanställer fälten för alla scheman som delar samma klass (XDM ExperienceEvent eller XDM Individual Profile) och är aktiverade för kundprofil i realtid.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---


# Unions

Unioner (eller unionsvyer) är systemgenererade, skrivskyddade scheman som sammanställer fälten för alla scheman som delar samma klass ([!DNL XDM ExperienceEvent] eller [!DNL XDM Individual Profile]) och är aktiverade för [[!DNL-kundprofil i realtid]](../../profile/home.md).

Det här dokumentet innehåller viktiga koncept för att arbeta med fackföreningar i API:t för schemaregister, inklusive exempelanrop för olika åtgärder. Mer allmän information om fackföreningar i XDM finns i avsnittet om fackföreningar i [grunderna för schemakomposition](../schema/composition.md#union).

## Unionens blandningar

I [!DNL Schema Registry] den ingår automatiskt tre mixar i unionsschemat: `identityMap`, `timeSeriesEvents`och `segmentMembership`.

### Identitetskarta

Ett unionsschema `identityMap` är en representation av kända identiteter inom unionens associerade postscheman. Identitetskartan delar upp identiteter i olika arrayer som skrivs med namnutrymme. Varje angiven identitet är i sig ett objekt som innehåller ett unikt `id` värde.

Mer information finns i dokumentationen [för](../../identity-service/home.md) identitetstjänsten.

### Tidsseriehändelser

Arrayen `timeSeriesEvents` är en lista med händelser i tidsserier som relaterar till postscheman som är associerade med unionen. När [!DNL Profile] data exporteras till datauppsättningar inkluderas den här arrayen för varje post. Detta är användbart för olika användningsområden, t.ex. maskininlärning där modeller behöver en profils hela beteendehistorik utöver dess postattribut.

### Segmentmedlemskapskarta

Kartan innehåller resultaten av `segmentMembership` segmentutvärderingar. När segmentjobben körs med [segmenterings-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)uppdateras kartan. `segmentMembership` lagrar också alla förutvärderade målgruppssegment som är inkapslade i Platform, vilket möjliggör integrering med andra lösningar som Adobe Audience Manager.

Mer information finns i självstudiekursen om hur du [skapar segment med API:er](../../segmentation/tutorials/create-a-segment.md) .

## Aktivera ett schema för fackmedlemskap

För att ett schema ska kunna inkluderas i den sammanfogade unionsvyn måste taggen &quot;union&quot; läggas till i schemats `meta:immutableTags` attribut. Detta görs genom en PATCH-begäran om att uppdatera schemat och lägga till `meta:immutableTags` arrayen med värdet &quot;union&quot;.

>[!NOTE]
>
>Oändringsbara taggar är taggar som ska anges, men aldrig tas bort.

**API-format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` det schema som du vill aktivera för användning i [!DNL Profile]. |

**Begäran**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Svar**

Ett lyckat svar returnerar detaljerna för det uppdaterade schemat, som nu innehåller en `meta:immutableTags` array som innehåller strängvärdet &quot;union&quot;.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Lista föreningar

När du ställer in &quot;union&quot;-taggen på ett schema skapar och underhåller [!DNL Schema Registry] automatiskt en union för den klass som schemat baseras på. Facken `$id` liknar standarden `$id` för en klass, där den enda skillnaden är den som läggs till med två understreck och ordet &quot;union&quot; (`"__union"`).

Om du vill visa en lista över tillgängliga fackföreningar kan du utföra en GET-förfrågan till `/unions` slutpunkten.

**API-format**

```http
GET /tenant/unions
```

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) och en `results` array i svarstexten. Om facken har definierats, anges `title`, `$id`, `meta:altId`och `version` för varje union som objekt i arrayen. Om inga fackföreningar har definierats returneras HTTP-status 200 (OK), men arrayen kommer att vara tom `results` .

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## Söka efter en specifik union

Du kan visa en specifik union genom att utföra en GET-förfrågan som innehåller fackets `$id` huvud och, beroende på vad som gäller för Acceptera, vissa eller alla detaljer om unionen.

>[!NOTE]
>
>Unionssökningar är tillgängliga med hjälp av `/unions` - och `/schemas` slutpunkterna för att de ska kunna användas vid [!DNL Profile] export till en datauppsättning.

**API-format**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{UNION_ID}` | Den URL-kodade `$id` URI:n för den union som du vill söka efter. URI:er för föreningsscheman läggs till med &quot;__union&quot;. |

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Förfrågningar om unionssökning kräver att en `version` tas med i huvudet Godkänn.

Följande accepterande huvuden är tillgängliga för fackschemasökningar:

| Acceptera | Beskrivning |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Raw med `$ref` och `allOf`. Innehåller rubriker och beskrivningar. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` attribut och `allOf` lösta. Innehåller rubriker och beskrivningar. |

**Svar**

Ett lyckat svar returnerar unionsvyn för alla scheman som implementerar den klass vars `$id` tillhandahölls i begärandesökvägen.

Svarsformatet beror på vilket Acceptera-huvud som skickas i begäran. Experimentera med olika Acceptera-huvuden för att jämföra svaren och ta reda på vilken rubrik som är bäst för dig.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## Visa scheman i en union

För att se vilka scheman som ingår i en viss union kan du utföra en GET-förfrågan med hjälp av frågeparametrar för att filtrera scheman i innehavarbehållaren.

Med hjälp av frågeparametern kan du konfigurera svaret så att det bara returnerar scheman som innehåller ett `property` fält och en `meta:immutableTags` `meta:class` som är lika med den klass vars union du använder.

**API-format**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CLASS_ID}` | Den klass `$id` vars union du vill komma åt. |

**Begäran**

Följande begäran söker upp alla scheman som ingår i [!DNL XDM Individual Profile] klassunionen.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en filtrerad lista med scheman, som endast innehåller de som uppfyller båda kraven. Kom ihåg att när du använder flera frågeparametrar antas en AND-relation vara. Svarets format beror på vilket Acceptera-huvud som skickas i begäran.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
