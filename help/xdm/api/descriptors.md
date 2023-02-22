---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;schema register;schema Registry;descriptor;descriptor;descriptors;descriptors;identity;identity;friendly name;Friendname;alternatedisplayinfo;reference;relationship;relationship
solution: Experience Platform
title: API-slutpunkt för beskrivare
description: Med slutpunkten /descriptors i API:t för schemaregister kan du programmässigt hantera XDM-beskrivningar i ditt upplevelseprogram.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 81b53d2bd84eacb32999b957bee9b5e9aa77d5f7
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

# Beskrivningsslutpunkt

Scheman definierar en statisk vy av datatabeller, men ger inga specifika detaljer om hur data som baseras på dessa scheman (till exempel datauppsättningar) kan relateras till varandra. Med Adobe Experience Platform kan du beskriva dessa relationer och andra tolka metadata om ett schema med hjälp av beskrivningar.

Schemabeskrivare är metadata på tenant-nivå, vilket innebär att de är unika för IMS-organisationen och alla beskrivningsåtgärder utförs i klientbehållaren.

Varje schema kan ha en eller flera schemabeskrivningsentiteter tillämpade. Varje schemabeskrivningsentitet innehåller en beskrivning `@type` och `sourceSchema` som den är tillämplig på. När dessa beskrivningar har tillämpats gäller de alla datauppsättningar som har skapats med schemat.

The `/descriptors` slutpunkt i [!DNL Schema Registry] Med API kan ni programmässigt hantera beskrivningar i ert upplevelseprogram.

## Komma igång

Slutpunkten som används i den här guiden är en del av [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Läs igenom [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med beskrivningar {#list}

Du kan visa alla beskrivningar som har definierats av din organisation genom att göra en GET-förfrågan till `/tenant/descriptors`.

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

Svarsformatet beror på `Accept` huvud som skickades i begäran. Observera att `/descriptors` slutpunktsanvändning `Accept` huvuden som inte är samma som alla andra slutpunkter i [!DNL Schema Registry] API.

>[!IMPORTANT]
>
>Beskrivningar kräver unika `Accept` rubriker som ersätter `xed` med `xdm`och erbjuder `link` som är unikt för beskrivningar. Den rätta `Accept` rubrikerna har tagits med i exempelanropen nedan, men var extra försiktig för att se till att rätt rubriker används när du arbetar med beskrivningar.

| `Accept` header | Beskrivning |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Returnerar en array med beskrivande ID:n |
| `application/vnd.adobe.xdm-link+json` | Returnerar en array med API-sökvägar för beskrivningar |
| `application/vnd.adobe.xdm+json` | Returnerar en array med expanderade beskrivningsobjekt |
| `application/vnd.adobe.xdm-v2+json` | Detta `Accept` sidhuvudet måste användas för att sidindelningsfunktionerna ska kunna användas. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Svaret innehåller en array för varje beskrivningstyp som har definierade beskrivningar. Med andra ord, om det inte finns några beskrivningar av en viss `@type` definierade returnerar registret inte en tom array för den beskrivningstypen.

När du använder `link` `Accept` header visas varje beskrivning som ett arrayobjekt i formatet `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

Om du vill visa information om en viss beskrivning kan du söka efter (GET) en enskild beskrivning med hjälp av dess `@id`.

**API-format**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | The `@id` för den beskrivning som du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran hämtar en beskrivning med dess `@id` värde. Beskrivningar har ingen version och därför behöver de inte `Accept` header krävs i sökbegäran.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om beskrivningen, inklusive dess `@type` och `sourceSchema`samt ytterligare information som varierar beroende på typen av beskrivning. Den returnerade `@id` ska matcha beskrivningen `@id` anges i begäran.

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

Du kan skapa en ny beskrivning genom att göra en POST-förfrågan till `/tenant/descriptors` slutpunkt.

>[!IMPORTANT]
>
>The [!DNL Schema Registry] I kan du definiera flera olika beskrivningstyper. Varje beskrivningstyp kräver att dess egna specifika fält skickas i begärandetexten. Se [appendix](#defining-descriptors) för en fullständig lista över beskrivningar och de fält som behövs för att definiera dem.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran definierar en identitetsbeskrivning i ett e-postadressfält i ett exempelschema. Det här säger [!DNL Experience Platform] om du vill använda e-postadressen som en identifierare för att sammanfoga information om den enskilda personen.

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

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och information om den nyskapade beskrivningen, inklusive dess `@id`. The `@id` är ett skrivskyddat fält som tilldelats av [!DNL Schema Registry] och används för att referera till beskrivningen i API:t.

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

Du kan uppdatera en beskrivning genom att inkludera dess `@id` på sökvägen till en begäran från PUT.

**API-format**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | The `@id` för den beskrivning som du vill uppdatera. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Denna begäran skriver i princip om beskrivningen, så begärandetexten måste innehålla alla fält som krävs för att definiera en beskrivning av den typen. Med andra ord är nyttolasten för begäran om att uppdatera (PUT) en beskrivning samma som nyttolasten som [skapa (POST) en beskrivning](#create) av samma typ.

>[!IMPORTANT]
>
>Precis som när du skapar beskrivningar med hjälp av POST-begäranden, kräver varje beskrivningstyp att egna specifika fält skickas i nyttolasterna för PUT-begäran. Se [appendix](#defining-descriptors) för en fullständig lista över beskrivningar och de fält som behövs för att definiera dem.

I följande exempel uppdateras en identitetsbeskrivning så att den refererar till en annan `xdm:sourceProperty` (`mobile phone`) och ändra `xdm:namespace` till `Phone`.

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

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och `@id` för den uppdaterade beskrivningen (som ska matcha `@id` skickas i begäran).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Utföra en [sökbegäran (GET)](#lookup) om du vill visa beskrivningen visar du att fälten nu har uppdaterats för att återspegla de ändringar som skickats i PUT-begäran.

## Ta bort en beskrivning {#delete}

Ibland kan du behöva ta bort en beskrivning som du har definierat från [!DNL Schema Registry]. Detta görs genom att en DELETE-begäran som refererar till `@id` för den beskrivning som du vill ta bort.

**API-format**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | The `@id` för den beskrivning som du vill ta bort. |

{style=&quot;table-layout:auto&quot;}

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

Om du vill bekräfta att beskrivningen har tagits bort kan du utföra en [sökförfrågan](#lookup) mot beskrivningen `@id`. Svaret returnerar HTTP-status 404 (Hittades inte) eftersom beskrivningen har tagits bort från [!DNL Schema Registry].

## Bilaga

I följande avsnitt finns ytterligare information om hur du arbetar med beskrivningar i [!DNL Schema Registry] API.

### Definiera beskrivningar {#defining-descriptors}

I följande avsnitt ges en översikt över tillgängliga beskrivningstyper, inklusive de fält som krävs för att definiera en beskrivning av varje typ.

#### Identitetsbeskrivare

En identitetsbeskrivning signalerar att[!UICONTROL sourceProperty]&quot; i &quot;[!UICONTROL sourceSchema]&quot; är en [!DNL Identity] fält enligt beskrivning [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `xdm:sourceSchema` | The `$id` URI för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökvägen till den specifika egenskap som ska vara identiteten. Sökvägen ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med &quot;egenskaper&quot; i sökvägen (använd t.ex. &quot;/personalEmail/address&quot; istället för &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | The `id` eller `code` identitetsnamnutrymmets värde. En lista med namnutrymmen finns med [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | Antingen `xdm:id` eller `xdm:code`, beroende på `xdm:namespace` används. |
| `xdm:isPrimary` | Ett booleskt värde (tillval). När värdet är true anges fältet som primär identitet. Scheman får endast innehålla en primär identitet. |

{style=&quot;table-layout:auto&quot;}

#### Egen namnbeskrivning {#friendly-name}

Med egna namnbeskrivningar kan användaren ändra `title`, `description`och `meta:enum` värden för huvudbibliotekets schemafält. Detta är särskilt användbart när du arbetar med&quot;eVars&quot; och andra&quot;generiska&quot; fält som du vill märka som innehåller information som är specifik för din organisation. Gränssnittet kan använda dessa för att visa ett mer användarvänligt namn eller för att endast visa fält som har ett eget namn.

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
| `@type` | Den typ av beskrivning som definieras. För en egen namnbeskrivning måste det här värdet anges till `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökvägen till den specifika egenskap vars information du vill ändra. Sökvägen ska börja med ett snedstreck (`/`) och inte sluta med en. Inkludera inte `properties` i sökvägen (använd till exempel `/personalEmail/address` i stället för `/properties/personalEmail/properties/address`). |
| `xdm:title` | Den nya rubriken som du vill visa för det här fältet, skriven i Inledande versal. |
| `xdm:description` | En valfri beskrivning kan läggas till tillsammans med titeln. |
| `meta:enum` | Om fältet anges av `xdm:sourceProperty` är ett strängfält, `meta:enum` kan användas för att lägga till föreslagna värden för fältet i segmenteringsgränssnittet. Det är viktigt att notera att `meta:enum` deklarerar inte en uppräkning eller tillhandahåller någon datavalidering för XDM-fältet.<br><br>Detta ska endast användas för XDM-fält som definieras av Adobe. Om egenskapen source är ett anpassat fält som definieras av din organisation bör du i stället redigera fältets `meta:enum` direkt via en PATCH-begäran till fältets överordnade resurs. |
| `meta:excludeMetaEnum` | Om fältet anges av `xdm:sourceProperty` är ett strängfält som har befintliga föreslagna värden under en `meta:enum` kan du inkludera det här objektet i en egen namnbeskrivning för att utesluta vissa eller alla värden från segmenteringen. Nyckeln och värdet för varje post måste matcha de som ingår i originalet `meta:enum` av fältet för att bidraget ska kunna uteslutas. |

{style=&quot;table-layout:auto&quot;}

#### Relationsbeskrivning

Relationsbeskrivare beskriver en relation mellan två olika scheman, aktiverade för egenskaperna som beskrivs i `sourceProperty` och `destinationProperty`. Se självstudiekursen om [definiera en relation mellan två scheman](../tutorials/relationship-api.md) för mer information.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För en relationsbeskrivning måste det här värdet anges till `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | The `$id` URI för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökväg till fältet i källschemat där relationen definieras. Ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med&quot;egenskaper&quot; i sökvägen (till exempel&quot;/personalEmail/address&quot; istället för&quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | The `$id` URI för referensschemat som den här beskrivningen definierar en relation med. |
| `xdm:destinationVersion` | Huvudversionen av referensschemat. |
| `xdm:destinationProperty` | Valfri sökväg till ett målfält i referensschemat. Om den här egenskapen utelämnas härleds målfältet av alla fält som innehåller en matchande identitetsbeskrivning för referens (se nedan). |

{style=&quot;table-layout:auto&quot;}

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
| `xdm:sourceSchema` | The `$id` URI för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökväg till fältet i källschemat som ska användas för att referera till referensschemat. Ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med &quot;egenskaper&quot; i sökvägen (till exempel `/personalEmail/address` i stället för `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Identitetsnamnområdeskoden för egenskapen source. |

{style=&quot;table-layout:auto&quot;}

#### Borttagen fältbeskrivning

Du kan [ta bort ett fält i en anpassad XDM-resurs](../tutorials/field-deprecation-api.md#custom) genom att lägga till en `meta:status` attribut inställt på `deprecated` till fältet i fråga. Om du vill ta bort fält från standard-XDM-resurser i dina scheman kan du tilldela schemat en inaktuell fältbeskrivning för att uppnå samma effekt. Använda [korrigera `Accept` header](../tutorials/field-deprecation-api.md#verify-deprecation)kan du sedan visa vilka standardfält som är inaktuella för ett schema när du söker efter det i API:t.

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
| `@type` | Beskrivningstypen. För en deskriptor för fältborttagning måste det här värdet anges till `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` för det schema som du använder beskrivningen på. |
| `xdm:sourceVersion` | Den version av schemat som du tillämpar beskrivningen på. Ska anges till `1`. |
| `xdm:sourceProperty` | Sökvägen till egenskapen i schemat som du tillämpar beskrivningen på. Om du vill tillämpa beskrivningen på flera egenskaper kan du ange en lista med sökvägar i form av en array (till exempel `["/firstName", "/lastName"]`). |

{style=&quot;table-layout:auto&quot;}
