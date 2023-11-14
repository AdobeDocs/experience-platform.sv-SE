---
keywords: Experience Platform;hemmabruk;populära ämnen;api;API;XDM;XDM system;Experience data model;Experience data model;data model;data model;schema register;schema Registry;union;union;union;union;segment;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Unisions API-slutpunkt
description: Med slutpunkten /union i API:t för schemaregister kan du programmässigt hantera XDM-föreningsscheman i ditt upplevelseprogram.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 3da2e8f66f08a7bb9533795f7854ad583734911c
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# Unions slutpunkt

Unioner (eller unionsvyer) är systemgenererade, skrivskyddade scheman som sammanställer fälten för alla scheman som delar samma klass ([!DNL XDM ExperienceEvent] eller [!DNL XDM Individual Profile]) och aktiveras för [[!DNL Real-Time Customer Profile]](../../profile/home.md).

Det här dokumentet innehåller viktiga koncept för att arbeta med fackföreningar i API:t för schemaregister, inklusive exempelanrop för olika åtgärder. Mer allmän information om fackföreningar i XDM finns i avsnittet om fackföreningar i [grunderna för schemakomposition](../schema/composition.md#union).

## Unionsschemafält

The [!DNL Schema Registry] innehåller automatiskt tre nyckelfält i ett unionsschema: `identityMap`, `timeSeriesEvents`och `segmentMembership`.

### Identitetskarta

Ett unionsschema `identityMap` är en representation av kända identiteter inom unionens associerade postscheman. Identitetskartan delar upp identiteter i olika arrayer som skrivs med namnutrymme. Varje angiven identitet är i sig ett objekt som innehåller ett unikt `id` värde. Se [Identitetstjänstens dokumentation](../../identity-service/home.md) för mer information.

### Tidsseriehändelser

The `timeSeriesEvents` arrayen är en lista över händelser i tidsserier som relaterar till postscheman som är associerade med unionen. När profildata exporteras till datauppsättningar inkluderas den här arrayen för varje post. Detta är användbart för olika användningsområden, t.ex. maskininlärning där modeller behöver en profils hela beteendehistorik utöver dess postattribut.

### Segmentmedlemskapskarta

The `segmentMembership` kartan lagrar resultatet av en utvärdering av en segmentdefinition. När segmentjobben har körts med [Segmenterings-API](https://www.adobe.io/experience-platform-apis/references/segmentation/)uppdateras kartan. `segmentMembership` lagrar även alla förutvärderade målgrupper som är inkapslade i Platform, vilket möjliggör integrering med andra lösningar som Adobe Audience Manager. Se självstudiekursen om [skapa målgrupper med API:er](../../segmentation/tutorials/create-a-segment.md) för mer information.

## Hämta en lista över föreningar {#list}

När du anger `union` -taggen i ett schema, [!DNL Schema Registry] lägger automatiskt till schemat i unionen för den klass som schemat baseras på. Om det inte finns någon union för den aktuella klassen skapas en ny union automatiskt. The `$id` for the union is similar to the standard `$id` andra [!DNL Schema Registry] , där den enda skillnaden är att det finns två understreck och ordet &quot;union&quot; (`__union`).

Du kan visa en lista över tillgängliga fackföreningar genom att göra en GET-förfrågan till `/tenant/unions` slutpunkt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

Svarsformatet beror på `Accept` huvud som skickades i begäran. Följande `Accept` Det finns rubriker för fackliga listor:

| `Accept` header | Beskrivning |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| `application/vnd.adobe.xed+json` | Returnerar en fullständig JSON-klass för varje resurs, med ursprunglig `$ref` och `allOf` ingår. (Gräns: 300) |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar HTTP-status 200 (OK) och en `results` i svarstexten. Om facken har definierats, anges informationen för varje union som objekt i arrayen. Om inga fackföreningar har definierats returneras HTTP-status 200 (OK) men `results` matrisen kommer att vara tom.

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

## Slå upp en union {#lookup}

Du kan visa en specifik union genom att utföra en GET-förfrågan som innehåller `$id` och, beroende på sidhuvudet Godkänn, en del eller all information om unionen.

>[!NOTE]
>
>Unionssökningar är tillgängliga med `/unions` och `/schemas` slutpunkt för att aktivera dem för användning i [!DNL Profile] exporterar till en datauppsättning.

**API-format**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{UNION_ID}` | Den URL-kodade `$id` URI för den union som du vill söka efter. URI:er för föreningsscheman läggs till med &quot;__union&quot;. |

{style="table-layout:auto"}

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Unionssökningsbegäranden kräver en `version` tas med i sidhuvudet Godkänn.

Följande accepterande huvuden är tillgängliga för fackschemasökningar:

| Acceptera | Beskrivning |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw med `$ref` och `allOf`. Innehåller rubriker och beskrivningar. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` attribut och `allOf` löstes. Innehåller rubriker och beskrivningar. |

{style="table-layout:auto"}

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

## Aktivera ett schema för fackmedlemskap {#enable}

För att ett schema ska inkluderas i unionen för sin klass, är en `union` -taggen måste läggas till i schemats `meta:immutableTags` -attribut. Du kan uppnå detta genom att göra en PATCH-förfrågan om att lägga till en `meta:immutableTags` array med ett strängvärde på `union` till det aktuella schemat. Se [slutpunktshandbok för scheman](./schemas.md#union) för ett detaljerat exempel.

## Visa scheman i en union {#list-schemas}

Om du vill se vilka scheman som ingår i en viss union kan du göra en GET-förfrågan till `/tenant/schemas` slutpunkt. Använda `property` frågeparameter, du kan konfigurera svaret så att endast returnerade scheman som innehåller en `meta:immutableTags` fält och en `meta:class` är lika med klassen vars union du går till.

**API-format**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CLASS_ID}` | The `$id` för den klass vars unionsaktiverade scheman du vill visa. |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar en lista med alla scheman som är en del av unionen för [!DNL XDM Individual Profile] klassen.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på `Accept` huvud som skickades i begäran. Följande `Accept` rubriker är tillgängliga för listscheman:

| `Accept` header | Beskrivning |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| `application/vnd.adobe.xed+json` | Returnerar det fullständiga JSON-schemat för varje resurs, med det ursprungliga `$ref` och `allOf` ingår. (Gräns: 300) |

{style="table-layout:auto"}

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
