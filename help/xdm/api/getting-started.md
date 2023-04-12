---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;data model;schema register;schemaregister;
solution: Experience Platform
title: Komma igång med API:t för schemaregister
description: Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna till innan du försöker anropa API:t för schemaregister.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# Komma igång med [!DNL Schema Registry] API

The [!DNL Schema Registry] Med API kan du skapa och hantera olika XDM-resurser (Experience Data Model). Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till [!DNL Schema Registry] API.

## Förutsättningar

För att du ska kunna använda utvecklarhandboken måste du ha en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

XDM använder JSON-schemaformatering för att beskriva och validera strukturen för importerade kundupplevelsedata. Vi rekommenderar därför att du granskar [officiell dokumentation för JSON-schema](https://json-schema.org/) för en bättre förståelse av denna underliggande teknik.

## Läser exempel-API-anrop

The [!DNL Schema Registry] API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Schema Registry], isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform], se [sandlådedokumentation](../../sandboxes/home.md).

Alla sökbegäranden (GET) till [!DNL Schema Registry] kräver ytterligare `Accept` header, vars värde bestämmer formatet för den information som returneras av API:t. Se [Acceptera rubrik](#accept) för mer information.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Lär känna ditt TENANT_ID {#know-your-tenant_id}

I hela API-guiderna ser du referenser till en `TENANT_ID`. Detta ID används för att säkerställa att de resurser du skapar namnges korrekt och finns i din organisation. Om du inte känner till ditt ID kan du få åtkomst till det genom att utföra följande GET-förfrågan:

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett svar returnerar information om din organisations användning av [!DNL Schema Registry]. Detta inkluderar `tenantId` -attribut, vars värde är ditt `TENANT_ID`.

```JSON
{
  "imsOrg":"{ORG_ID}",
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
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
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
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
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

## Förstå `CONTAINER_ID` {#container}

Anropar [!DNL Schema Registry] API kräver att en `CONTAINER_ID`. Det finns två behållare som API-anrop kan göras mot: den `global` behållare och `tenant` behållare.

### Global behållare

The `global` behållaren innehåller alla Adobe och [!DNL Experience Platform] partnertillhandahållna klasser, schemafältgrupper, datatyper och scheman. Du får endast utföra list- och sökbegäranden (GET) mot `global` behållare.

Ett exempel på ett anrop som använder `global` container skulle se ut så här:

```http
GET /global/classes
```

### Klientbehållaren

Inte för att förväxlas med din unika `TENANT_ID`, `tenant` behållare innehåller alla klasser, fältgrupper, datatyper, scheman och beskrivningar som definierats av en organisation. De är unika för varje organisation, vilket innebär att de inte är synliga eller hanterbara av andra organisationer. Du kan utföra alla CRUD-åtgärder (GET, POST, PUT, PATCH, DELETE) mot resurser som du skapar i dialogrutan `tenant` behållare.

Ett exempel på ett anrop som använder `tenant` container skulle se ut så här:

```http
POST /tenant/fieldgroups
```

När du skapar en klass, fältgrupp, schema eller datatyp i `tenant` behållaren sparas den i [!DNL Schema Registry] och har tilldelats en `$id` URI som innehåller `TENANT_ID`. Detta `$id` används i hela API:t för att referera till specifika resurser. Exempel på `$id` värden anges i nästa avsnitt.

## Resursidentifiering {#resource-identification}

XDM-resurser identifieras med en `$id` i form av en URI, som följande exempel:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

För att göra URI:n mer REST-vänlig har scheman även en punktnotation-kodning av URI:n i en egenskap som kallas `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Anropar [!DNL Schema Registry] API har stöd för antingen URL-kodad `$id` URI eller `meta:altId` (punktnotationsformat). Det bästa sättet är att använda den URL-kodade `$id` URI när du gör ett REST-anrop till API:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Acceptera rubrik {#accept}

När du utför list- och uppslagsåtgärder (GET) i [!DNL Schema Registry] API, och `Accept` måste anges för att formatet för de data som returneras av API:t ska kunna fastställas. När du söker efter specifika resurser måste ett versionsnummer också inkluderas i `Accept` header.

I följande tabell visas kompatibla `Accept` rubrikvärden, inklusive de med versionsnummer, tillsammans med beskrivningar av vad API:t returnerar när de används.

| Acceptera | Beskrivning |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Returnerar endast en lista med ID:n. Detta används oftast för att lista resurser. |
| `application/vnd.adobe.xed+json` | Returnerar en lista med det fullständiga JSON-schemat med det ursprungliga `$ref` och `allOf` ingår. Detta används för att returnera en lista med fullständiga resurser. |
| `application/vnd.adobe.xed+json; version=1` | Raw XDM med `$ref` och `allOf`. Har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` attribut och `allOf` löstes. Har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw XDM med `$ref` och `allOf`. Inga rubriker eller beskrivningar. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` attribut och `allOf` löstes. Inga rubriker eller beskrivningar. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` attribut och `allOf` löstes. Beskrivningar ingår. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` och `allOf` har åtgärdats, har rubriker och beskrivningar. Föråldrade fält indikeras med en `meta:status` attribut för `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Plattformen har för närvarande bara stöd för en huvudversion för varje schema (`1`). Därför är värdet för `version` måste alltid vara `1` när sökningar utförs för att returnera den senaste delversionen av schemat. Mer information om schemaversion finns i underavsnittet nedan.

### Schemaversion {#versioning}

Schemaversioner refereras av `Accept` rubriker i API:t för schemaregister och i `schemaRef.contentType` egenskaper i API-nyttolaster för underordnade plattformstjänster.

För närvarande stöder Platform endast en större version (`1`) för varje schema. Enligt [regler för schemautveckling](../schema/composition.md#evolution)måste varje uppdatering av ett schema vara icke-förstörande, vilket innebär att nya mindre versioner av ett schema (`1.2`, `1.3`, osv.) är alltid bakåtkompatibla med tidigare mindre versioner. Därför, när du anger `version=1`returnerar schemaregistret alltid **senaste** huvudversion `1` för ett schema, vilket innebär att tidigare delversioner inte returneras.

>[!NOTE]
>
>Det icke-förstörande kravet för schemautveckling framtvingas först efter att schemat har refererats av en datauppsättning och ett av följande fall är sant:
>
>* Data har importerats till datauppsättningen.
>* Datauppsättningen har aktiverats för användning i kundprofilen i realtid (även om inga data har inhämtats).
>
>Om schemat inte har associerats med en datauppsättning som uppfyller något av ovanstående villkor, kan alla ändringar göras i det. I samtliga fall gäller dock att `version` finns fortfarande kvar på `1`.

## Begränsningar för XDM-fält och bästa praxis

Fälten i ett schema listas i dess `properties` -objekt. Varje fält är i sig ett objekt som innehåller attribut som beskriver och begränsar de data som fältet kan innehålla. Se guiden på [definiera anpassade fält i API](../tutorials/custom-fields-api.md) för kodexempel och valfria begränsningar för de vanligaste datatyperna.

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
* Fältet ska innehålla en `title`, skrivet i Title Case. Exempel: `Field Name`
* Fältet kräver en `type`.
   * Definiering av vissa typer kan kräva ett valfritt `format`.
   * Om en viss dataformatering krävs, `examples` kan läggas till som en array.
   * Fälttypen kan också definieras med valfri datatyp i registret. Se avsnittet om [skapa en datatyp](./data-types.md#create) i slutpunktshandboken för datatyper om du vill ha mer information.
* The `description` I förklaras fältet och relevant information om fältdata. Det bör skrivas i fullständiga meningar med tydligt språk så att alla som använder schemat kan förstå fältets avsikt.

## Nästa steg

Börja ringa samtal med [!DNL Schema Registry] API: välj en av de tillgängliga slutpunktsguiderna.
