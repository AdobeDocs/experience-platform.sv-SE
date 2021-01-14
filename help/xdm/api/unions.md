---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;union;Union;unions;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Unions
description: Med slutpunkten /union i API:t för schemaregister kan du programmässigt hantera XDM-föreningsscheman i ditt upplevelseprogram.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---


# Unions slutpunkt

Unioner (eller unionsvyer) är systemgenererade, skrivskyddade scheman som sammanställer fälten för alla scheman som delar samma klass ([!DNL XDM ExperienceEvent] eller [!DNL XDM Individual Profile]) och är aktiverade för [[!DNL Real-time Customer Profile]](../../profile/home.md).

Det här dokumentet innehåller viktiga koncept för att arbeta med fackföreningar i API:t för schemaregister, inklusive exempelanrop för olika åtgärder. Mer allmän information om fackföreningar i XDM finns i avsnittet om fackföreningar i [grunderna för schemakomposition](../schema/composition.md#union).

## Unionsschemafält

[!DNL Schema Registry] innehåller automatiskt tre nyckelfält i ett unionsschema: `identityMap`, `timeSeriesEvents` och `segmentMembership`.

### Identitetskarta

Ett unionsschemats `identityMap` är en representation av de kända identiteterna i unionens associerade postscheman. Identitetskartan delar upp identiteter i olika arrayer som skrivs med namnutrymme. Varje angiven identitet är i sig ett objekt som innehåller ett unikt `id`-värde. Mer information finns i [identitetstjänstens dokumentation](../../identity-service/home.md).

### Tidsseriehändelser

Arrayen `timeSeriesEvents` är en lista med händelser för tidsserier som relaterar till postscheman som associeras med unionen. När profildata exporteras till datauppsättningar inkluderas den här arrayen för varje post. Detta är användbart för olika användningsområden, t.ex. maskininlärning där modeller behöver en profils hela beteendehistorik utöver dess postattribut.

### Segmentmedlemskapskarta

Mappningen `segmentMembership` lagrar resultaten av segmentutvärderingar. När segmentjobben körs med [Segmenterings-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) uppdateras kartan. `segmentMembership` lagrar också alla förutvärderade målgruppssegment som är inkapslade i Platform, vilket möjliggör integrering med andra lösningar som Adobe Audience Manager. Mer information finns i självstudiekursen om att [skapa segment med API:er](../../segmentation/tutorials/create-a-segment.md).

## Hämta en lista över föreningar {#list}

När du anger taggen `union` i ett schema lägger [!DNL Schema Registry] automatiskt till schemat i unionen för den klass som schemat baseras på. Om det inte finns någon union för den aktuella klassen skapas en ny union automatiskt. `$id` för unionen liknar standarden `$id` för andra [!DNL Schema Registry]-resurser. Den enda skillnaden är att den läggs till med två understreck och ordet &quot;union&quot; (`__union`).

Du kan visa en lista över tillgängliga fackföreningar genom att göra en GET-förfrågan till `/tenant/unions`-slutpunkten.

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

Svarsformatet beror på det `Accept`-huvud som skickas i begäran. Följande `Accept`-huvuden är tillgängliga för att lista fackföreningar:

| `Accept` header | Beskrivning |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| `application/vnd.adobe.xed+json` | Returnerar den fullständiga JSON-klassen för varje resurs, med ursprunglig `$ref` och `allOf` inkluderad. (Gräns: 300) |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) och en `results`-array i svarstexten. Om facken har definierats, anges informationen för varje union som objekt i arrayen. Om inga fackföreningar har definierats returneras HTTP-status 200 (OK), men `results`-arrayen är tom.

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

## Söka efter en union {#lookup}

Du kan visa en specifik union genom att utföra en GET-förfrågan som innehåller `$id` och, beroende på accepteringshuvudet, en del eller all information om unionen.

>[!NOTE]
>
>Unionssökningar är tillgängliga med slutpunkten `/unions` och `/schemas` för att aktivera dem för användning i [!DNL Profile]-exporter till en datamängd.

**API-format**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{UNION_ID}` | URL-kodad `$id` URI för den union som du vill söka efter. URI:er för föreningsscheman läggs till med &quot;__union&quot;. |

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

Förfrågningar om unionssökning kräver att `version` inkluderas i huvudet Godkänn.

Följande accepterande huvuden är tillgängliga för fackschemasökningar:

| Acceptera | Beskrivning |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Raw med `$ref` och `allOf`. Innehåller rubriker och beskrivningar. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` attribut och  `allOf` lösta. Innehåller rubriker och beskrivningar. |

**Svar**

Ett lyckat svar returnerar unionsvyn för alla scheman som implementerar klassen vars `$id` angavs i sökvägen till begäran.

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

## Aktivera ett schema för unionsmedlemskap {#enable}

För att ett schema ska kunna inkluderas i unionen för sin klass måste en `union`-tagg läggas till i schemats `meta:immutableTags`-attribut. Du kan uppnå detta genom att göra en PATCH-begäran om att lägga till en `meta:immutableTags`-matris med ett strängvärde på `union` i det aktuella schemat. Ett detaljerat exempel finns i [schemas slutpunktshandbok](./schemas.md#union).

## Visa scheman i en union {#list-schemas}

För att se vilka scheman som ingår i en specifik union kan du utföra en GET-begäran till `/tenant/schemas`-slutpunkten. Med frågeparametern `property` kan du konfigurera svaret så att det bara returnerar scheman som innehåller ett `meta:immutableTags`-fält och ett `meta:class` som är lika med den klass vars union du använder.

**API-format**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CLASS_ID}` | `$id` för den klass vars unionsaktiverade scheman du vill visa. |

**Begäran**

Följande begäran hämtar en lista med alla scheman som är en del av unionen för klassen [!DNL XDM Individual Profile].

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på det `Accept`-huvud som skickas i begäran. Följande `Accept` rubriker är tillgängliga för listscheman:

| `Accept` header | Beskrivning |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| `application/vnd.adobe.xed+json` | Returnerar det fullständiga JSON-schemat för varje resurs, med det ursprungliga `$ref` och `allOf` inkluderat. (Gräns: 300) |

**Svar**

Ett lyckat svar returnerar en filtrerad lista med scheman, som bara innehåller de som tillhör den angivna klassen som har aktiverats för medlemskap i unionen. Kom ihåg att när du använder flera frågeparametrar antas en AND-relation vara.

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
