---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;Experience data model;Experience data model;data model;data model;schema register;schema Registry;descriptor;descriptor;descriptors;descriptors;identity;identity;friendly name;Friendname;alternatedisplayinfo;reference;relation;relation;relation
solution: Experience Platform
title: API-slutpunkt för beskrivare
description: Med slutpunkten /descriptors i API:t för schemaregister kan du programmässigt hantera XDM-beskrivningar i ditt upplevelseprogram.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 02a22362b9ecbfc5fd7fcf17dc167309a0ea45d5
workflow-type: tm+mt
source-wordcount: '2886'
ht-degree: 0%

---

# Beskrivningsslutpunkt

Scheman definierar dataenheternas struktur, men anger inte hur datauppsättningar som skapats från dessa scheman relaterar till varandra. I Adobe Experience Platform kan du använda beskrivningar för att beskriva dessa relationer och lägga till tolkningsmetadata i ett schema.

Beskrivningar är metadataobjekt på tenant-nivå som tillämpas på scheman i Adobe Experience Platform. De definierar strukturella relationer, nycklar och beteendefält (t.ex. tidsstämplar eller versionshantering) som påverkar hur data valideras, förenas eller tolkas nedåt.

Ett schema kan ha en eller flera beskrivningar. Varje beskrivning definierar en `@type` och den `sourceSchema` som den gäller för. Beskrivningen gäller automatiskt för alla datauppsättningar som skapas från det schemat.

I Adobe Experience Platform är en beskrivning metadata som lägger till beteenderegler eller strukturell innebörd i ett schema.
Det finns flera typer av beskrivningar, bland annat:

- [Identitetsbeskrivning](#identity-descriptor) - markerar ett fält som en identitet
- [Primär nyckelbeskrivning](#primary-key-descriptor) - använder unikhet
- [Relationsbeskrivning](#relationship-descriptor) - definierar en koppling med sekundärnyckel
- [Beskrivning av alternativ visningsinformation](#friendly-name) - du kan byta namn på ett fält i användargränssnittet
- [Version](#version-descriptor)- och [timestamp](#timestamp-descriptor)-beskrivningar - spåra händelseordning och ändringsidentifiering

Med slutpunkten `/descriptors` i API:t [!DNL Schema Registry] kan du programmässigt hantera beskrivningar i ditt upplevelseprogram.

## Komma igång

Slutpunkten som används i den här guiden ingår i [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett Experience Platform-API.

Förutom standardbeskrivningar har [!DNL Schema Registry] stöd för beskrivningstyper för modellbaserade scheman, till exempel **primärnyckel**, **version** och **tidsstämpel**. Dessa lägger in unika funktioner, styr versionshantering och definierar tidsseriefält på schemanivå. Om du inte känner till modellbaserade scheman kan du förhandsgranska [Data Mirror översikt](../data-mirror/overview.md) och [modellbaserade scheman ](../schema/model-based.md) innan du fortsätter.

>[!IMPORTANT]
>
>Mer information om alla beskrivningstyper finns i [Bilaga](#defining-descriptors).

## Hämta en lista med beskrivningar {#list}

Du kan visa alla beskrivningar som har definierats av din organisation genom att göra en GET-begäran till `/tenant/descriptors`.

**API-format**

```http
GET /tenant/descriptors
```

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

Svarsformatet beror på det `Accept`-huvud som skickas i begäran. Observera att slutpunkten `/descriptors` använder `Accept` rubriker som skiljer sig från alla andra slutpunkter i API:t [!DNL Schema Registry].

>[!IMPORTANT]
>
>Beskrivningar kräver unika `Accept`-huvuden som ersätter `xed` med `xdm` och erbjuder även ett `link`-alternativ som är unikt för beskrivningar. Rätt `Accept` rubriker har inkluderats i exempelanropen nedan, men var extra försiktig för att se till att rätt rubriker används när du arbetar med beskrivningar.

| `Accept` huvud | Beskrivning |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Returnerar en array med beskrivande ID:n |
| `application/vnd.adobe.xdm-link+json` | Returnerar en array med API-sökvägar för beskrivningar |
| `application/vnd.adobe.xdm+json` | Returnerar en array med expanderade beskrivningsobjekt |
| `application/vnd.adobe.xdm-v2+json` | Det här `Accept`-huvudet måste användas för att växlingsfunktioner ska kunna användas. |

{style="table-layout:auto"}

**Svar**

Svaret innehåller en array för varje beskrivningstyp som har definierade beskrivningar. Om det inte finns några beskrivningar av en viss `@type` definierad returnerar registret alltså inte en tom matris för den beskrivningstypen.

När du använder rubriken `link` `Accept` visas varje beskrivning som ett arrayobjekt i formatet `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## Söka efter en beskrivning {#lookup}

Om du vill visa information om en viss beskrivning skickar du en GET-begäran med hjälp av dess `@id`.

**API-format**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | `@id` för beskrivningen som du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar en beskrivning med dess `@id`-värde. Beskrivningar har ingen version, därför krävs ingen `Accept`-rubrik i sökningsbegäran.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om beskrivningen, inklusive dess `@type` och `sourceSchema`, samt ytterligare information som varierar beroende på typen av beskrivning. Den returnerade `@id` ska matcha beskrivningen `@id` som anges i begäran.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Skapa en beskrivning {#create}

Du kan skapa en ny beskrivning genom att göra en POST-begäran till slutpunkten `/tenant/descriptors`.

>[!IMPORTANT]
>
>Med [!DNL Schema Registry] kan du definiera flera olika beskrivningstyper. Varje beskrivningstyp kräver att dess egna specifika fält skickas i begärandetexten. I [bilagan](#defining-descriptors) finns en fullständig lista över beskrivningar och de fält som krävs för att definiera dem.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran definierar en identitetsbeskrivning i ett e-postadressfält i ett exempelschema. Detta anger för [!DNL Experience Platform] att använda e-postadressen som en identifierare för att hjälpa till att sammanfoga information om personen.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och information om den nyskapade beskrivningen, inklusive `@id`. `@id` är ett skrivskyddat fält som tilldelats av [!DNL Schema Registry] och används för att referera till beskrivningen i API:t.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Uppdatera en beskrivning {#put}

Du kan uppdatera en beskrivning genom att ta med dess `@id` i sökvägen till en PUT-begäran.

**API-format**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | `@id` för beskrivningen som du vill uppdatera. |

{style="table-layout:auto"}

**Begäran**

Denna begäran skriver i princip om beskrivningen, så begärandetexten måste innehålla alla fält som krävs för att definiera en beskrivning av den typen. Med andra ord är nyttolasten som ska uppdatera (PUT) en beskrivning densamma som nyttolasten för att [skapa (POST) en beskrivning](#create) av samma typ.

>[!IMPORTANT]
>
>Precis som när du skapar beskrivningar med POST-begäranden, kräver varje beskrivningstyp att egna specifika fält skickas i PUT-begärannyttolaster. I [bilagan](#defining-descriptors) finns en fullständig lista över beskrivningar och de fält som krävs för att definiera dem.

I följande exempel uppdateras en identitetsbeskrivning så att den refererar till en annan `xdm:sourceProperty` (`mobile phone`) och `xdm:namespace` ändras till `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och `@id` för den uppdaterade beskrivningen (som ska matcha `@id` som skickades i begäran).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Om du utför en [sökbegäran (GET)](#lookup) för att visa beskrivningen visas att fälten nu har uppdaterats för att återspegla de ändringar som har skickats i PUT-begäran.

## Ta bort en beskrivning {#delete}

Ibland kan du behöva ta bort en beskrivning som du har definierat från [!DNL Schema Registry]. Detta görs genom att en DELETE-begäran refererar till `@id` för den beskrivning som du vill ta bort.

**API-format**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | `@id` för beskrivningen som du vill ta bort. |

{style="table-layout:auto"}

**Begäran**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Om du vill bekräfta att beskrivningen har tagits bort kan du utföra en [uppslagsbegäran](#lookup) mot beskrivningen `@id`. Svaret returnerar HTTP-status 404 (Hittades inte) eftersom beskrivningen har tagits bort från [!DNL Schema Registry].

## Bilaga {#appendix}

Följande avsnitt innehåller ytterligare information om hur du arbetar med beskrivningar i API:t [!DNL Schema Registry].

### Definiera beskrivningar {#defining-descriptors}

>[!NOTE]
>
>Det maximala antalet beskrivningar som kan tillämpas på en organisations sandlåda är 4000.

I följande avsnitt ges en översikt över tillgängliga beskrivningstyper, inklusive de fält som krävs för att definiera en beskrivning av varje typ.

>[!IMPORTANT]
>
>Du kan inte etikettera klientnamnområdesobjektet eftersom systemet skulle tillämpa den etiketten på alla anpassade fält i den sandlådan. I stället måste du ange den lövnod under det objektet som du vill etikettera.

#### Identitetsbeskrivare {#identity-descriptor}

En identitetsbeskrivare signalerar att [!UICONTROL sourceProperty] för [!UICONTROL sourceSchema] är ett [!DNL Identity]-fält enligt beskrivningen i [Experience Platform Identity Service](../../identity-service/home.md).

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För en identitetsbeskrivning måste det här värdet anges till `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | URI `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökvägen till den specifika egenskap som ska vara identiteten. Sökvägen ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med &quot;egenskaper&quot; i sökvägen (använd till exempel &quot;/personalEmail/address&quot; istället för &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | Värdet `id` eller `code` för identitetsnamnområdet. En lista med namnutrymmen kan hittas med [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
| `xdm:property` | Antingen `xdm:id` eller `xdm:code`, beroende på vilken `xdm:namespace` som används. |
| `xdm:isPrimary` | Ett booleskt värde (tillval). När värdet är true anges fältet som primär identitet. Scheman får endast innehålla en primär identitet. |

{style="table-layout:auto"}

#### Egen namnbeskrivning {#friendly-name}

Med egna namnbeskrivningar kan en användare ändra värdena `title`, `description` och `meta:enum` för huvudbibliotekets schemafält. Detta är särskilt användbart när du arbetar med&quot;eVars&quot; och andra&quot;generiska&quot; fält som du vill märka som innehåller information som är specifik för din organisation. Gränssnittet kan använda dessa för att visa ett mer användarvänligt namn eller för att endast visa fält som har ett eget namn.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. Värdet måste anges till `xdm:alternateDisplayInfo` för en egen namnbeskrivning. |
| `xdm:sourceSchema` | URI `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökvägen till den specifika egenskap vars information du vill ändra. Sökvägen ska börja med ett snedstreck (`/`) och inte sluta med ett. Ta inte med `properties` i sökvägen (använd till exempel `/personalEmail/address` i stället för `/properties/personalEmail/properties/address`). |
| `xdm:title` | Den nya rubriken som du vill visa för det här fältet, skriven i Inledande versal. |
| `xdm:description` | En valfri beskrivning kan läggas till tillsammans med titeln. |
| `meta:enum` | Om fältet som anges av `xdm:sourceProperty` är ett strängfält kan `meta:enum` användas för att lägga till föreslagna värden för fältet i segmenteringsgränssnittet. Observera att `meta:enum` inte deklarerar en uppräkning eller tillhandahåller någon datavalidering för XDM-fältet.<br><br>Detta ska endast användas för XDM-fält som definieras av Adobe. Om källegenskapen är ett anpassat fält som definieras av din organisation bör du i stället redigera fältets `meta:enum`-egenskap direkt via en PATCH-begäran till fältets överordnade resurs. |
| `meta:excludeMetaEnum` | Om fältet som anges av `xdm:sourceProperty` är ett strängfält som har befintliga föreslagna värden i ett `meta:enum`-fält, kan du inkludera det här objektet i en egen namnbeskrivning för att utesluta vissa eller alla dessa värden från segmenteringen. Nyckeln och värdet för varje post måste matcha de som finns i fältets ursprungliga `meta:enum` för att posten ska kunna uteslutas. |

{style="table-layout:auto"}

#### Relationsbeskrivning {#relationship-descriptor}

Relationsbeskrivare beskriver en relation mellan två olika scheman, som är aktiverade för egenskaperna som beskrivs i `xdm:sourceProperty` och `xdm:destinationProperty`. Mer information finns i självstudiekursen [om hur du definierar en relation mellan två scheman](../tutorials/relationship-api.md).

Använd de här egenskaperna för att deklarera hur ett källfält (sekundärnyckel) relaterar till ett målfält ([primärnyckel](#primary-key-descriptor) eller kandidatnyckel).

>[!TIP]
>
>En **sekundärnyckel** är ett fält i källschemat (definierat av `xdm:sourceProperty`) som refererar till ett nyckelfält i ett annat schema. En **kandidatnyckel** är ett fält (eller en uppsättning fält) i målschemat som unikt identifierar en post och kan användas i stället för primärnyckeln.

API:t har stöd för två mönster:

- `xdm:descriptorOneToOne`: standardrelation med :1.
- `xdm:descriptorRelationship`: allmänt mönster för nytt arbete och modellbaserade scheman (stöder kardinalitet, namngivning och icke-primära nyckelmål).

##### Ett-till-ett-förhållande (standardscheman)

Använd det här när du behåller befintliga standardschemaintegreringar som redan är beroende av `xdm:descriptorOneToOne`.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

I följande tabell beskrivs de fält som krävs för att definiera en 1:1-relationsbeskrivning.

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För en relationsbeskrivare måste det här värdet anges till `xdm:descriptorOneToOne`, såvida du inte har åtkomst till Real-Time CDP B2B edition. Med B2B edition har du möjlighet att använda `xdm:descriptorOneToOne` eller [`xdm:descriptorRelationship`](#b2b-relationship-descriptor). |
| `xdm:sourceSchema` | URI `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökväg till fältet i källschemat där relationen definieras. Bör börja med &quot;/&quot; och inte sluta med &quot;/&quot;. Ta inte med&quot;egenskaper&quot; i sökvägen (till exempel&quot;/personalEmail/address&quot; istället för&quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI `$id` för det referensschema som den här beskrivningen definierar en relation med. |
| `xdm:destinationVersion` | Huvudversionen av referensschemat. |
| `xdm:destinationProperty` | (Valfritt) Sökväg till ett målfält i referensschemat. Om den här egenskapen utelämnas härleds målfältet av alla fält som innehåller en matchande identitetsbeskrivning för referens (se nedan). |

##### Allmän relation (modellbaserade scheman och rekommenderas för nya projekt)

Använd den här beskrivningen för alla nya implementeringar och för modellbaserade scheman. Du kan definiera relationens kardinalitet (t.ex. en-till-en eller många-till-en), ange relationsnamn och länka till ett målfält som inte är primärnyckeln (icke-primärnyckel).

I följande exempel visas hur du definierar en allmän relationsbeskrivning.

**Minimalt exempel:**

Det här minimala exemplet innehåller bara de obligatoriska fälten för att definiera en många-till-ett-relation mellan två scheman.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceProperty": "/customer_ref",
  "xdm:sourceVersion": 1,
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:cardinality": "M:1"
}
```

**Exempel med alla valfria fält:**

Det här exemplet innehåller alla valfria fält, till exempel relationsnamn, visningsrubriker och ett explicit målfält för icke-primärnyckel.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/customer_ref",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationProperty": "/customer_id",
  "xdm:sourceToDestinationName": "CampaignToCustomer",
  "xdm:destinationToSourceName": "CustomerToCampaign",
  "xdm:sourceToDestinationTitle": "Customer campaigns",
  "xdm:destinationToSourceTitle": "Campaign customers",
  "xdm:cardinality": "M:1"
}
```

##### Välja en relationsbeskrivning

Använd följande riktlinjer för att bestämma vilken relationsbeskrivning som ska användas:

| Situationen | Beskrivning som ska användas |
| --------------------------------------------------------------------- | ----------------------------------------- |
| Nytt arbete eller modellbaserade scheman | `xdm:descriptorRelationship` |
| Befintlig :1-mappning i standardscheman | Fortsätt använda `xdm:descriptorOneToOne` om du inte behöver funktioner som bara stöds av `xdm:descriptorRelationship`. |
| Behöver många-till-ett eller valfri kardinalitet (`1:1`, `1:0`, `M:1`, `M:0`) | `xdm:descriptorRelationship` |
| Relationsnamn eller titlar för läsbarhet i användargränssnittet/nedladdningsbart | `xdm:descriptorRelationship` |
| Behöver ett målmål som inte är en identitet | `xdm:descriptorRelationship` |

>[!NOTE]
>
>Om det finns befintliga `xdm:descriptorOneToOne`-beskrivningar i standardscheman kan du fortsätta använda dem om du inte behöver funktioner som icke-primära mål för identitetsmål, anpassade namn eller utökade kardinalitetsalternativ.

##### Funktionsjämförelse

I följande tabell jämförs funktionerna för de två beskrivningstyperna:

| Funktion | `xdm:descriptorOneToOne` | `xdm:descriptorRelationship` |
| ------------------ | ------------------------ | ------------------------------------------------------------------------ |
| Kardinalitet | 1:1 | 1:1, 1:0, M:1, M:0 (informativt) |
| Målmål | Identitet/explicit fält | Primärnyckel som standard, eller icke-primärnyckel via `xdm:destinationProperty` |
| Namngivningsfält | Stöds inte | `xdm:sourceToDestinationName`, `xdm:destinationToSourceName` och titlar |
| Relationell anpassning | Begränsad | Primärt mönster för modellbaserade scheman |

##### Begränsningar och validering

Följ dessa krav och rekommendationer när du definierar en allmän relationsbeskrivning:

- För modellbaserade scheman placerar du källfältet (sekundärnyckeln) på rotnivån. Detta är för närvarande en teknisk begränsning för konsumtion, inte bara en rekommendation om god praxis.
- Kontrollera att datatyperna för käll- och målfält är kompatibla (numeriskt, datum, booleskt, sträng).
- Kom ihåg att kardinalitet är informativt; lagring tvingar inte till det. Ange kardinalitet i formatet `<source>:<destination>`. Godkända värden är: `1:1`, `1:0`, `M:1` eller `M:0`.

#### Primär nyckelbeskrivning {#primary-key-descriptor}

Den primära nyckelbeskrivningen (`xdm:descriptorPrimaryKey`) tillämpar unikhet och begränsningar som inte är null i ett eller flera fält i ett schema.

```json
{
  "@type": "xdm:descriptorPrimaryKey",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": ["/orderId", "/orderLineId"]
}
```

| Egenskap | Beskrivning |
| -------------------- | ----------------------------------------------------------------------------- |
| `@type` | Måste vara `xdm:descriptorPrimaryKey`. |
| `xdm:sourceSchema` | `$id` URI för schemat. |
| `xdm:sourceProperty` | JSON-pekare till primärnyckelfält. Använd en array för sammansatta nycklar. För scheman i tidsserier måste den sammansatta nyckeln innehålla tidsstämpelfältet för att säkerställa att alla händelseposter är unika. |

#### Versionsbeskrivare {#version-descriptor}

>[!NOTE]
>
>I UI-schemaredigeraren visas versionsbeskrivningen som [!UICOTRNOL Versionsidentifierare].

Versionsbeskrivningen (`xdm:descriptorVersion`) anger ett fält som identifierar och förhindrar konflikter från oordnade ändringshändelser.

```json
{
  "@type": "xdm:descriptorVersion",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/versionNumber"
}
```

| Egenskap | Beskrivning |
| -------------------- | ------------------------------------------------------------- |
| `@type` | Måste vara `xdm:descriptorVersion`. |
| `xdm:sourceSchema` | `$id` URI för schemat. |
| `xdm:sourceProperty` | JSON-pekare till versionsfältet. Måste markeras som `required`. |

#### Tidsstämpelbeskrivning {#timestamp-descriptor}

>[!NOTE]
>
>I UI-schemaredigeraren visas tidsstämpelbeskrivningen som [!UICOTRNOL Tidsstämpelidentifierare].

Tidsstämpelbeskrivningen (`xdm:descriptorTimestamp`) anger ett datum/tid-fält som tidsstämpel för scheman med `"meta:behaviorType": "time-series"`.

```json
{
  "@type": "xdm:descriptorTimestamp",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/eventTime"
}
```

| Egenskap | Beskrivning |
| -------------------- | ------------------------------------------------------------------------------------------ |
| `@type` | Måste vara `xdm:descriptorTimestamp`. |
| `xdm:sourceSchema` | `$id` URI för schemat. |
| `xdm:sourceProperty` | JSON-pekare till tidsstämpelfältet. Måste vara markerad som `required` och vara av typen `date-time`. |

##### B2B-relationsbeskrivning {#B2B-relationship-descriptor}

Real-Time CDP B2B edition introducerar ett alternativt sätt att definiera relationer mellan scheman, vilket möjliggör många-till-ett-relationer. Den nya relationen måste ha typen `@type: xdm:descriptorRelationship` och nyttolasten måste innehålla fler fält än relationen `@type: xdm:descriptorOneToOne`. Mer information finns i självstudiekursen [Definiera en schemarelation för B2B edition](../tutorials/relationship-b2b.md).

```json
{
   "@type": "xdm:descriptorRelationship",
   "xdm:sourceSchema" : "https://ns.adobe.com/{TENANT_ID}/schemas/9f2b2f225ac642570a110d8fd70800ac0c0573d52974fa9a",
   "xdm:sourceVersion" : 1,
   "xdm:sourceProperty" : "/person-ref",
   "xdm:destinationSchema" : "https://ns.adobe.com/{TENANT_ID/schemas/628427680e6b09f1f5a8f63ba302ee5ce12afba8de31acd7",
   "xdm:destinationVersion" : 1,
   "xdm:destinationProperty": "/personId",
   "xdm:destinationNamespace" : "People", 
   "xdm:destinationToSourceTitle" : "Opportunity Roles",
   "xdm:sourceToDestinationTitle" : "People",
   "xdm:cardinality": "M:1"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För oss med följande fält måste värdet anges till `xdm:descriptorRelationship`. Mer information om ytterligare typer finns i avsnittet [Relationsbeskrivningar](#relationship-descriptor). |
| `xdm:sourceSchema` | URI `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökväg till fältet i källschemat där relationen definieras. Bör börja med &quot;/&quot; och inte sluta med &quot;/&quot;. Ta inte med&quot;egenskaper&quot; i sökvägen (till exempel&quot;/personalEmail/address&quot; istället för&quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI `$id` för det referensschema som den här beskrivningen definierar en relation med. |
| `xdm:destinationVersion` | Huvudversionen av referensschemat. |
| `xdm:destinationProperty` | (Valfritt) Sökväg till ett målfält i referensschemat. Detta måste matcha schemats primära ID eller ett annat fält med en kompatibel datatyp till `xdm:sourceProperty`. Om det utelämnas kanske relationen inte fungerar som förväntat. |
| `xdm:destinationNamespace` | Namnområdet för det primära ID:t från referensschemat. |
| `xdm:destinationToSourceTitle` | Visningsnamnet för relationen från referensschemat till källschemat. |
| `xdm:sourceToDestinationTitle` | Visningsnamnet för relationen från källschemat till referensschemat. |
| `xdm:cardinality` | Kopplingsförhållandet mellan scheman. Det här värdet ska anges till `M:1`, vilket hänvisar till en många-till-en-relation. |

{style="table-layout:auto"}

#### Referens för identitetsbeskrivning

Referensidentitetsbeskrivningar ger en referenskontext till den primära identiteten för ett schemafält, vilket gör att det kan refereras till av fält i andra scheman. Referensschemat måste redan ha ett primärt identitetsfält definierat innan det kan refereras till av andra scheman via den här beskrivningen.

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För en referensidentitetsbeskrivning måste det här värdet anges till `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | URI `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökväg till fältet i källschemat som ska användas för att referera till referensschemat. Ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med &quot;egenskaper&quot; i sökvägen (till exempel `/personalEmail/address` i stället för `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Identitetsnamnområdeskoden för egenskapen source. |

{style="table-layout:auto"}

#### Borttagen fältbeskrivning

Du kan [ta bort ett fält i en anpassad XDM-resurs](../tutorials/field-deprecation-api.md#custom) genom att lägga till ett `meta:status`-attribut med värdet `deprecated` i fältet i fråga. Om du vill ta bort fält från standard-XDM-resurser i dina scheman kan du tilldela schemat en inaktuell fältbeskrivning för att uppnå samma effekt. Med [korrekt `Accept` header](../tutorials/field-deprecation-api.md#verify-deprecation) kan du sedan visa vilka standardfält som är inaktuella för ett schema när du söker efter det i API:t.

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Beskrivningstypen. För en deskriptor för fältborttagning måste värdet anges till `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` för schemat som du tillämpar beskrivningen på. |
| `xdm:sourceVersion` | Den version av schemat som du tillämpar beskrivningen på. Ska anges till `1`. |
| `xdm:sourceProperty` | Sökvägen till egenskapen i schemat som du tillämpar beskrivningen på. Om du vill tillämpa beskrivningen på flera egenskaper kan du tillhandahålla en lista med sökvägar i form av en array (till exempel `["/firstName", "/lastName"]`). |

{style="table-layout:auto"}
