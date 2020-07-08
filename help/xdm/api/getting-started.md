---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för API för schematabell
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---


# Utvecklarhandbok för API för schematabell

Schemaregistret används för att komma åt schemabiblioteket i Adobe Experience Platform, med ett användargränssnitt och RESTful API som alla tillgängliga biblioteksresurser kan nås från.

Med API:t för schemaregister kan du utföra grundläggande CRUD-åtgärder för att visa och hantera alla scheman och relaterade resurser som är tillgängliga för dig i Adobe Experience Platform. Detta gäller även dem som definieras av Adobe, Experience Platform partners och leverantörer vars program du använder. Du kan också använda API-anrop för att skapa nya scheman och resurser för organisationen, samt visa och redigera resurser som du redan har definierat.

Den här utvecklarhandboken innehåller steg som hjälper dig att börja använda API:t för schemaregister. Guiden innehåller sedan exempel på API-anrop för att utföra nyckelåtgärder med schemaregistret.

## Förutsättningar

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman.
* [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:t för schemaregister.

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör schemaregistret, är isolerade till specifika virtuella sandlådor. Alla förfrågningar till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla GET-begäranden (lookup) till schemaregistret kräver en extra Accept-rubrik, vars värde bestämmer vilket format som informationen returneras av API:t. Mer information finns i avsnittet [Acceptera sidhuvud](#accept) nedan.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Lär känna ditt TENANT_ID {#know-your-tenant_id}

I hela den här guiden ser du referenser till en `TENANT_ID`. Detta ID används för att säkerställa att de resurser du skapar namnges korrekt och finns i IMS-organisationen. Om du inte känner till ditt ID kan du få åtkomst till det genom att utföra följande GET-begäran:

**API-format**

```http
GET /stats
```

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett svar returnerar information om din organisations användning av schemaregistret. Detta inkluderar ett `tenantId` -attribut, vars värde är ditt `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

* `tenantId`: Värdet `TENANT_ID` för din IMS-organisation.

## Förstå `CONTAINER_ID` {#container}

Anrop till API:t för schemaregister kräver användning av en `CONTAINER_ID`. Det finns två behållare som API-anrop kan göras mot: den **globala behållaren** och **innehavarbehållaren**.

### Global behållare

Den globala behållaren innehåller alla standardklasser, mixins, datatyper och scheman som tillhandahålls av Adobe och Experience Platform partner. Du får bara utföra list- och sökbegäranden (GET) mot den globala behållaren.

### Klientbehållaren

Klientbehållaren ska inte förväxlas med din unika `TENANT_ID`eftersom den innehåller alla klasser, blandningar, datatyper, scheman och beskrivningar som definieras av en IMS-organisation. De är unika för varje organisation, vilket innebär att de inte är synliga eller hanterbara av andra IMS-organisationer. Du kan utföra alla CRUD-åtgärder (GET, POST, PUT, PATCH, DELETE) mot resurser som du skapar i innehavarbehållaren.

När du skapar en klass, mixin, schema eller datatyp i klientbehållaren, sparas den i schemaregistret och tilldelas en `$id` URI som innehåller din `TENANT_ID`. Detta `$id` används i hela API:t för att referera till specifika resurser. Exempel på `$id` värden finns i nästa avsnitt.

## Schemaidentifiering {#schema-identification}

Scheman identifieras med ett `$id` attribut i form av en URI, som:
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

För att göra URI:n mer REST-vänlig har scheman även en punktnotation-kodning av URI:n i en egenskap med namnet `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Anrop till API:t för schemaregister stöder antingen den URL-kodade `$id` URI:n eller `meta:altId` (punktnotation-format). Bästa sättet är att använda den URL-kodade `$id` URI:n när du gör ett REST-anrop till API:t, så här:
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Acceptera rubrik {#accept}

När du utför list- och lookup-åtgärder (GET) i API:t för schemaregister krävs en Accept-rubrik för att fastställa formatet för de data som returneras av API:t. När du söker efter specifika resurser måste ett versionsnummer också inkluderas i rubriken Godkänn.

I följande tabell visas kompatibla värden för Acceptera sidhuvud, inklusive de med versionsnummer, tillsammans med beskrivningar av vad API:t returnerar när de används.

| Acceptera | Beskrivning |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Returnerar endast en lista med ID:n. Detta används oftast för att lista resurser. |
| `application/vnd.adobe.xed+json` | Returnerar en lista med fullständigt JSON-schema med ursprungligt `$ref` och `allOf` inkluderat. Detta används för att returnera en lista med fullständiga resurser. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw XDM med `$ref` och `allOf`. Har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` attribut och `allOf` lösta. Har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw XDM med `$ref` och `allOf`. Inga rubriker eller beskrivningar. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` attribut och `allOf` lösta. Inga rubriker eller beskrivningar. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` attribut och `allOf` lösta. Beskrivningar ingår. |

>[!NOTE]
>
>Om endast `major` versionen tillhandahålls (t.ex. 1, 2, 3) returnerar registret den senaste `minor` versionen (t.ex. .1, .2, .3) automatiskt.

## Begränsningar för XDM-fält och bästa praxis

Fälten i ett schema visas i dess `properties` objekt. Varje fält är i sig ett objekt som innehåller attribut som beskriver och begränsar de data som fältet kan innehålla.

Mer information om hur du definierar fälttyper i API finns i [bilagan](appendix.md) till den här guiden, inklusive kodexempel och valfria begränsningar för de vanligaste datatyperna.

I följande exempelfält visas ett korrekt formaterat XDM-fält, med mer information om namnbegränsningar och de bästa metoderna som anges nedan. Dessa metoder kan också användas när du definierar andra resurser som innehåller liknande attribut.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* Namnet på ett fältobjekt kan innehålla alfanumeriska tecken, bindestreck eller understreck, men **får inte** börja med ett understreck.
   * **Korrekt:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Felaktigt:** `_fieldName`
* camelCase är att föredra som fältobjektets namn. Exempel: `fieldName`
* Fältet ska innehålla en `title`, skriven i versaler. Exempel: `Field Name`
* Fältet kräver ett `type`.
   * Du kan behöva ange en valfri typ `format`.
   * Där en viss dataformatering krävs kan `examples` läggas till som en array.
   * Fälttypen kan också definieras med valfri datatyp i registret. Mer information finns i avsnittet om [att skapa en datatyp](create-data-type.md) i den här handboken.
* Fältet `description` och relevant information om fältdata förklaras. Det bör skrivas i fullständiga meningar med tydligt språk så att alla som använder schemat kan förstå fältets avsikt.

Mer information om hur du definierar fälttyper i API finns i [bilagan](appendix.md) .

## Nästa steg

Det här dokumentet innehöll den nödvändiga kunskapen för att anropa API:t för schemaregister, inklusive nödvändiga autentiseringsuppgifter. Du kan nu gå vidare till exempelsamtalen i den här utvecklarhandboken och följa med i instruktionerna för dessa. En fullständig stegvis genomgång av hur du skapar ett schema i API:t finns i följande [självstudiekurs](../tutorials/create-schema-api.md).
