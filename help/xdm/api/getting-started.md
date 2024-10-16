---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;data model;schema register;schemaregister;
solution: Experience Platform
title: Komma igång med API:t för schemaregister
description: Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna till innan du försöker anropa API:t för schemaregister.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: eb1cf204e95591082b27dc97cd3c709a23b20b08
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# Komma igång med [!DNL Schema Registry]-API:t

Med API:t [!DNL Schema Registry] kan du skapa och hantera olika XDM-resurser (Experience Data Model). Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t [!DNL Schema Registry].

## Förhandskrav

För att du ska kunna använda utvecklarhandboken måste du ha en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grunderna i schemakomposition](../schema/composition.md): Lär dig mer om grundläggande byggstenar i XDM-scheman.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

XDM använder JSON-schemaformatering för att beskriva och validera strukturen för importerade kundupplevelsedata. Vi rekommenderar därför starkt att du läser [JSON-schemats officiella dokumentation](https://json-schema.org/) för att få en bättre förståelse för den underliggande tekniken.

## Läser exempel-API-anrop

API-dokumentationen för [!DNL Schema Registry] innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Schema Registry], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i [sandlådedokumentationen](../../sandboxes/home.md).

Alla sökbegäranden (GET) till [!DNL Schema Registry] kräver ytterligare ett `Accept`-huvud, vars värde bestämmer vilket format som informationen returneras av API:t. Mer information finns i avsnittet [Acceptera rubrik](#accept) nedan.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Lär känna ditt TENANT_ID {#know-your-tenant_id}

Under hela API-guiderna ser du referenser till en `TENANT_ID`. Detta ID används för att säkerställa att de resurser du skapar namnges korrekt och finns i din organisation. Om du inte känner till ditt ID kan du få åtkomst till det genom att utföra följande GET-förfrågan:

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

Ett godkänt svar returnerar information om din organisations användning av [!DNL Schema Registry]. Detta inkluderar ett `tenantId`-attribut, vars värde är din `TENANT_ID`.

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

## `CONTAINER_ID` förstår {#container}

Anrop till API:t [!DNL Schema Registry] kräver att du använder en `CONTAINER_ID`. Det finns två behållare som API-anrop kan göras mot: behållaren `global` och behållaren `tenant`.

### Global behållare

Behållaren `global` innehåller alla standardklasser som tillhandahålls av Adobe och [!DNL Experience Platform] partner, schemafältgrupper, datatyper och scheman. Du får bara utföra list- och uppslagsbegäranden (GET) mot behållaren `global`.

Ett exempel på ett anrop som använder behållaren `global` skulle se ut så här:

```http
GET /global/classes
```

### Klientbehållaren

Behållaren `tenant` ska inte blandas ihop med din unika `TENANT_ID`. Den innehåller alla klasser, fältgrupper, datatyper, scheman och beskrivningar som definierats av en organisation. De är unika för varje organisation, vilket innebär att de inte är synliga eller hanterbara av andra organisationer. Du kan utföra alla CRUD-åtgärder (GET, POST, PUT, PATCH, DELETE) mot resurser som du skapar i behållaren `tenant`.

Ett exempel på ett anrop som använder behållaren `tenant` skulle se ut så här:

```http
POST /tenant/fieldgroups
```

När du skapar en klass, fältgrupp, schema eller datatyp i behållaren `tenant` sparas den i [!DNL Schema Registry] och tilldelas en `$id` URI som innehåller din `TENANT_ID`. `$id` används i hela API:t för att referera till specifika resurser. Exempel på `$id`-värden finns i nästa avsnitt.

## Resursidentifiering {#resource-identification}

XDM-resurser identifieras med ett `$id`-attribut i form av en URI, som i följande exempel:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

För att göra URI:n mer REST-vänlig har scheman även en punktnotation-kodning av URI:n i en egenskap med namnet `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Anrop till [!DNL Schema Registry]-API:t stöder antingen den URL-kodade `$id` URI:n eller `meta:altId` (punktnotation-format). Bästa sättet är att använda den URL-kodade `$id`-URI:n när du gör ett REST-anrop till API, så här:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Acceptera rubrik {#accept}

När du utför list- och lookup-åtgärder (GET) i API:t [!DNL Schema Registry] krävs en `Accept`-rubrik för att fastställa formatet för de data som returneras av API:t. När du söker efter specifika resurser måste ett versionsnummer också inkluderas i rubriken `Accept`.

I följande tabell visas kompatibla rubrikvärden för `Accept`, inklusive de med versionsnummer, tillsammans med beskrivningar av vad API:t returnerar när de används.

| Acceptera | Beskrivning |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Returnerar endast en lista med ID:n. Detta används oftast för att lista resurser. |
| `application/vnd.adobe.xed+json` | Returnerar en lista med det fullständiga JSON-schemat med det ursprungliga `$ref` och `allOf` inkluderade. Detta används för att returnera en lista med fullständiga resurser. |
| `application/vnd.adobe.xed+json; version=1` | Raw XDM med `$ref` och `allOf`. Har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` attribut och `allOf` matchades. Har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw XDM med `$ref` och `allOf`. Inga rubriker eller beskrivningar. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` attribut och `allOf` matchades. Inga rubriker eller beskrivningar. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` attribut och `allOf` matchades. Beskrivningar ingår. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` och `allOf` har matchats, har rubriker och beskrivningar. Föråldrade fält anges med attributet `meta:status` för `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Plattformen stöder för närvarande endast en huvudversion för varje schema (`1`). Därför måste värdet för `version` alltid vara `1` när sökförfrågningar utförs för att returnera den senaste delversionen av schemat. Mer information om schemaversion finns i underavsnittet nedan.

### Schemaversion {#versioning}

Schemaversioner refereras av `Accept` huvuden i API:t för schemaregister och i `schemaRef.contentType` egenskaper i underordnade API-nyttolaster för plattformstjänster.

För närvarande stöder Platform endast en huvudversion (`1`) för varje schema. Enligt [reglerna för schemautveckling](../schema/composition.md#evolution) måste varje uppdatering av ett schema vara icke-förstörande, vilket innebär att nya delversioner av ett schema (`1.2`, `1.3` osv.) är alltid bakåtkompatibla med tidigare mindre versioner. När du anger `version=1` returnerar schemaregistret därför alltid schemats **senaste** huvudversion `1` , vilket innebär att tidigare delversioner inte returneras.

>[!NOTE]
>
>Det icke-förstörande kravet för schemautveckling framtvingas först efter att schemat har refererats av en datauppsättning och ett av följande fall är sant:
>
>* Data har importerats till datauppsättningen.
>* Datauppsättningen har aktiverats för användning i kundprofilen i realtid (även om inga data har importerats).
>
>Om schemat inte har associerats med en datauppsättning som uppfyller något av ovanstående villkor, kan alla ändringar göras i det. I samtliga fall finns dock komponenten `version` kvar på `1`.

## Begränsningar för XDM-fält och bästa praxis

Fälten i ett schema visas i dess `properties`-objekt. Varje fält är i sig ett objekt som innehåller attribut som beskriver och begränsar de data som fältet kan innehålla. Se guiden [definiera anpassade fält i API](../tutorials/custom-fields-api.md) för kodexempel och valfria begränsningar för de vanligaste datatyperna.

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
* Fältnamn är inte skiftlägeskänsliga och måste ha olika namn på samma nivå i schemat.
* camelCase är att föredra som fältobjektets namn. Exempel: `fieldName`
* Fältet ska innehålla `title`, skrivet i versaler. Exempel: `Field Name`
* Fältet kräver `type`.
   * För att definiera vissa typer kan det krävas en valfri `format`.
   * Där en viss dataformatering krävs kan `examples` läggas till som en matris.
   * Fälttypen kan också definieras med valfri datatyp i registret. Mer information finns i avsnittet [Skapa en datatyp](./data-types.md#create) i slutpunktshandboken för datatyper.
* `description` förklarar fältet och relevant information om fältdata. Det bör skrivas i fullständiga meningar med tydligt språk så att alla som använder schemat kan förstå fältets avsikt.

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Schema Registry] väljer du en av de tillgängliga slutpunktsguiderna.
