---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;descriptor;Descriptor;descriptors;Descriptors;identity;Identity;friendly name;Friendly name;alternatedisplayinfo;reference;Reference;relationship;Relationship
solution: Experience Platform
title: Beskrivningar
description: 'Scheman definierar en statisk vy av datatabeller, men ger inga specifika detaljer om hur data som baseras på dessa scheman (till exempel datauppsättningar) kan relateras till varandra. Med Adobe Experience Platform kan du beskriva dessa relationer och andra tolka metadata om ett schema med hjälp av beskrivningar. '
topic: developer guide
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 0%

---


# Beskrivningar

Scheman definierar en statisk vy av datatabeller, men ger inga specifika detaljer om hur data som baseras på dessa scheman (till exempel datauppsättningar) kan relateras till varandra. Med Adobe Experience Platform kan du beskriva dessa relationer och andra tolka metadata om ett schema med hjälp av beskrivningar.

Schemabeskrivare är metadata på tenant-nivå, vilket innebär att de är unika för IMS-organisationen och alla beskrivningsåtgärder utförs i klientbehållaren.

Varje schema kan ha en eller flera schemabeskrivningsentiteter tillämpade. Varje schemabeskrivningsentitet innehåller en beskrivning `@type` och den `sourceSchema` som den gäller. När dessa beskrivningar har tillämpats gäller de alla datauppsättningar som har skapats med schemat.

Det här dokumentet innehåller exempel-API-anrop för beskrivningar, samt en fullständig lista över tillgängliga beskrivningar och de fält som krävs för att definiera varje typ.

>[!NOTE]
>
>Beskrivningar kräver unika Accept-huvuden som ersätter `xed` med `xdm`, men som i övrigt ser mycket lika ut som Accept-huvuden som används i andra delar av [!DNL Schema Registry]. Rätt Accept-huvuden har tagits med i samplingsanropen nedan, men var extra försiktig för att se till att rätt huvuden används.

## Listbeskrivare

En enda GET-förfrågan kan användas för att returnera en lista över alla beskrivningar som har definierats av din organisation.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

Svarsformatet beror på vilket Acceptera-huvud som skickas i begäran. Observera att `/descriptors` slutpunkten använder Acceptera rubriker som skiljer sig från alla andra slutpunkter i [!DNL Schema Registry] API:t.

Rubrikerna för godkännande av beskrivning ersätter `xed` med `xdm`och erbjuder ett `link` alternativ som är unikt för beskrivningar.

| Acceptera | Beskrivning |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Returnerar en array med beskrivande ID:n |
| `application/vnd.adobe.xdm-link+json` | Returnerar en array med API-sökvägar för beskrivningar |
| `application/vnd.adobe.xdm+json` | Returnerar en array med expanderade beskrivningsobjekt |

**Svar**

Svaret innehåller en array för varje beskrivningstyp som har definierade beskrivningar. Om det inte finns några beskrivningar av en viss `@type` definierad typ returnerar registret alltså ingen tom array för den beskrivningstypen.

När du använder `link` Accept-huvudet visas varje beskrivning som ett arrayobjekt i formatet `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

## Söka efter en beskrivning

Om du vill visa information om en viss beskrivning kan du söka efter (GET) en enskild beskrivning med hjälp av dess `@id`.

**API-format**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | The `@id` of the descriptor you want to lookup. |

**Begäran**

Beskrivningar har ingen version, därför krävs ingen Accept-rubrik i sökningsbegäran.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om beskrivningen, inklusive dess `@type` och `sourceSchema`, samt ytterligare information som varierar beroende på typen av beskrivning. Det returnerade `@id` måste matcha den beskrivning `@id` som anges i begäran.

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
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Skapa beskrivning

Med [!DNL Schema Registry] den kan du definiera flera olika beskrivningstyper. Varje beskrivningstyp kräver att dess egna specifika fält skickas i POSTEN. En fullständig lista med beskrivningar, och de fält som behövs för att definiera dem, finns i avsnittet om tillägg om [att definiera beskrivningar](#defining-descriptors).

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran definierar en identitetsbeskrivning i ett e-postadressfält i ett exempelschema. Detta anger [!DNL Experience Platform] att e-postadressen ska användas som identifierare för att sammanfoga information om den enskilda personen.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och information om den nyskapade beskrivningen, inklusive dess `@id`. Det `@id` är ett skrivskyddat fält som tilldelats av [!DNL Schema Registry] och används för att referera till beskrivningen i API:t.

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

## Uppdateringsbeskrivning

Du kan uppdatera en beskrivning genom att göra en PUT-begäran som refererar till den beskrivning `@id` som du vill uppdatera i sökvägen till begäran.

**API-format**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | The `@id` of the descriptor you want to update. |

**Begäran**

Denna begäran skriver i princip om beskrivningen, så begärandetexten måste innehålla alla fält som krävs för att definiera en beskrivning av den typen. Med andra ord är nyttolasten som ska uppdatera (PUT) en beskrivning densamma som nyttolasten för att skapa (POST) en beskrivning av samma typ.

I det här exemplet uppdateras identitetsbeskrivningen så att den refererar till en annan `xdm:sourceProperty` (&quot;mobiltelefon&quot;) och ändrar `xdm:namespace` den till &quot;Telefon&quot;.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Information om egenskaperna `xdm:namespace` och `xdm:property`hur du får tillgång till dem finns i avsnittet om tillägg om [att definiera beskrivningar](#defining-descriptors).

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och `@id` den uppdaterade beskrivningen (som ska matcha den som `@id` skickades i begäran).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Om du utför en sökning (GET) för att visa beskrivningen visas att fälten nu har uppdaterats för att återspegla de ändringar som skickats i PUT-begäran.

## Ta bort beskrivning

Ibland kan du behöva ta bort en beskrivning som du har definierat från [!DNL Schema Registry]. Detta gör du genom att göra en DELETE-begäran som refererar till `@id` den beskrivning som du vill ta bort.

**API-format**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DESCRIPTOR_ID}` | The `@id` of the descriptor you want to delete. |

**Begäran**

Du behöver inte acceptera rubriker när du tar bort beskrivningar.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Om du vill bekräfta att beskrivningen har tagits bort kan du utföra en uppslagsbegäran mot beskrivningen `@id`. Svaret returnerar HTTP-status 404 (Hittades inte) eftersom beskrivningen har tagits bort från [!DNL Schema Registry].

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du arbetar med beskrivningar i [!DNL Schema Registry] API.

### Definiera beskrivningar

I följande avsnitt ges en översikt över tillgängliga beskrivningstyper, inklusive de fält som krävs för att definiera en beskrivning av varje typ.

#### Identitetsbeskrivare

En identitetsbeskrivning signalerar att&quot;[!UICONTROL sourceProperty]&quot; för&quot;[!UICONTROL sourceSchema]&quot; är ett [!DNL Identity] fält som beskrivs av [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | Den typ av beskrivning som definieras. |
| `xdm:sourceSchema` | URI:n `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökvägen till den specifika egenskap som ska vara identiteten. Sökvägen ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med &quot;egenskaper&quot; i sökvägen (använd t.ex. &quot;/personalEmail/address&quot; istället för &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | Identitetsnamnutrymmets `id` - eller `code` -värde. En lista med namnutrymmen finns med API:t för [[!DNL Identity Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | Antingen `xdm:id` eller `xdm:code`, beroende på vilken `xdm:namespace` som används. |
| `xdm:isPrimary` | Ett booleskt värde (tillval). När värdet är true anges fältet som primär identitet. Scheman får endast innehålla en primär identitet. |

#### Egen namnbeskrivning

Med egna namnbeskrivningar kan användaren ändra värdena `title`, `description`och `meta:enum` värdena i huvudbibliotekets schemafält. Detta är särskilt användbart när du arbetar med&quot;eVars&quot; och andra&quot;generiska&quot; fält som du vill märka som innehåller information som är specifik för din organisation. Gränssnittet kan använda dessa för att visa ett mer användarvänligt namn eller för att endast visa fält som har ett eget namn.

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
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. |
| `xdm:sourceSchema` | URI:n `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökvägen till den specifika egenskap som ska vara identiteten. Sökvägen ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med &quot;egenskaper&quot; i sökvägen (använd t.ex. &quot;/personalEmail/address&quot; istället för &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:title` | Den nya rubriken som du vill visa för det här fältet, skriven i Inledande versal. |
| `xdm:description` | En valfri beskrivning kan läggas till tillsammans med titeln. |
| `meta:enum` | Om fältet som anges av `xdm:sourceProperty` är ett strängfält, `meta:enum` bestämmer listan med föreslagna värden för fältet i [!DNL Experience Platform] användargränssnittet. Det är viktigt att komma ihåg att `meta:enum` inte deklarerar en uppräkning eller tillhandahåller någon datavalidering för XDM-fältet.<br><br>Detta ska endast användas för XDM-fält som definieras av Adobe. Om egenskapen source är ett anpassat fält som definieras av din organisation bör du i stället redigera fältets `meta:enum` egenskap direkt via en [PATCH-begäran](./update-resource.md). |

#### Relationsbeskrivning

Relationsbeskrivare beskriver en relation mellan två olika scheman, som är aktiverade för egenskaperna som beskrivs i `sourceProperty` och `destinationProperty`. Mer information finns i självstudiekursen om hur du [definierar en relation mellan två scheman](../tutorials/relationship-api.md) .

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
| `@type` | Den typ av beskrivning som definieras. |
| `xdm:sourceSchema` | URI:n `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökväg till fältet i källschemat där relationen definieras. Ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med&quot;egenskaper&quot; i sökvägen (till exempel&quot;/personalEmail/address&quot; istället för&quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | URI:n för målschemat som den här beskrivningen definierar en relation med. `$id` |
| `xdm:destinationVersion` | Huvudversionen av målschemat. |
| `xdm:destinationProperty` | Valfri sökväg till ett målfält i målschemat. Om den här egenskapen utelämnas härleds målfältet av alla fält som innehåller en matchande identitetsbeskrivning för referens (se nedan). |


#### Referens för identitetsbeskrivning

Referensidentitetsbeskrivningar ger en referenskontext till den primära identiteten för ett schemafält, vilket gör att det kan refereras till av fält i andra scheman. Fält måste redan ha en identitetsbeskrivning innan en referensbeskrivning kan användas på dem.

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
| `@type` | Den typ av beskrivning som definieras. |
| `xdm:sourceSchema` | URI:n `$id` för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökväg till fältet i källschemat där beskrivningen definieras. Ska börja med ett &quot;/&quot; och inte sluta med ett. Ta inte med&quot;egenskaper&quot; i sökvägen (till exempel&quot;/personalEmail/address&quot; istället för&quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | Identitetsnamnområdeskoden för egenskapen source. |