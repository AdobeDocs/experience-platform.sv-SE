---
keywords: Experience Platform;hem;populära ämnen;datastyrning;dataanvändningsetikett api;principtjänst api
solution: Experience Platform
title: Hantera dataanvändningsetiketter med API:er
description: Med API:t för datauppsättningstjänsten kan du tillämpa och redigera användningsetiketter för datauppsättningar. Den ingår i Adobe Experience Platform datakatalogfunktioner, men är skild från katalogtjänstens API, som hanterar datauppsättningsmetadata.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 1%

---


# Hantera dataanvändningsetiketter med API:er

Det här dokumentet innehåller anvisningar om hur du hanterar etiketter för dataanvändning med [!DNL Policy Service] API och [!DNL Dataset Service] API.

The [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) innehåller flera slutpunkter som gör att du kan skapa och hantera dataanvändningsetiketter för din organisation.

The [!DNL Dataset Service] Med API kan du använda och redigera användningsetiketter för datauppsättningar. Den är en del av Adobe Experience Platform funktioner för datakatalog, men skiljer sig från [!DNL Catalog Service] API som hanterar datauppsättningsmetadata.

## Komma igång

Innan du läser den här handboken följer du de steg som beskrivs i [komma igång, avsnitt](../../catalog/api/getting-started.md) i guiden för katalogutvecklare om du vill samla in de inloggningsuppgifter som krävs för att ringa till [!DNL Platform] API:er.

För att ringa [!DNL Dataset Service] slutpunkter som kontureras i det här dokumentet måste ha den unika `id` värde för en specifik datamängd. Om du inte har det här värdet läser du i guiden [lista katalogobjekt](../../catalog/api/list-objects.md) för att hitta ID:n för dina befintliga datauppsättningar.

## Visa alla etiketter {#list-labels}

Använda [!DNL Policy Service] API, du kan visa alla `core` eller `custom` etiketter genom att göra en GET-förfrågan till `/labels/core` eller `/labels/custom`, respektive.

**API-format**

```http
GET /labels/core
GET /labels/custom
```

**Begäran**

I följande begäran visas alla anpassade etiketter som skapats under din organisation.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med anpassade etiketter som hämtats från systemet. Eftersom exempelbegäran ovan gjordes till `/labels/custom`visas endast anpassade etiketter i svaret nedan.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Söka efter en etikett {#look-up-label}

Du kan söka efter en specifik etikett genom att ta med den etikettens `name` i sökvägen för en GET-begäran till [!DNL Policy Service] API.

**API-format**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LABEL_NAME}` | The `name` egenskapen för den anpassade etikett som du vill söka efter. |

**Begäran**

Följande begäran hämtar den anpassade etiketten `L2`, vilket anges i sökvägen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar informationen om den anpassade etiketten.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Skapa eller uppdatera en anpassad etikett {#create-update-label}

Om du vill skapa eller uppdatera en anpassad etikett måste du göra en PUT-förfrågan till [!DNL Policy Service] API.

**API-format**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LABEL_NAME}` | The `name` egenskap för en anpassad etikett. Om det inte finns någon egen etikett med det här namnet skapas en ny etikett. Om det finns en sådan kommer den etiketten att uppdateras. |

**Begäran**

Följande begäran skapar en ny etikett, `L3`, som syftar till att beskriva data som innehåller information om kundens valda betalningsplaner.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | En unik strängidentifierare för etiketten. Det här värdet används för uppslagssyften och för att använda etiketten på datauppsättningar och fält, och vi rekommenderar därför att det är kort och koncist. |
| `category` | Etikettens kategori. Du kan skapa egna kategorier för anpassade etiketter, men vi rekommenderar att du använder `Custom` om du vill att etiketten ska visas i användargränssnittet. |
| `friendlyName` | Ett eget namn för etiketten som används för visning. |
| `description` | (Valfritt) En beskrivning av etiketten som ger ytterligare kontext. |

**Svar**

Ett lyckat svar returnerar informationen för en anpassad etikett, med HTTP-kod 200 (OK) om en befintlig etikett uppdaterades, eller 201 (Skapad) om en ny etikett skapades.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Söka efter etiketter för en datauppsättning {#look-up-dataset-labels}

Du kan söka efter dataanvändningsetiketter som har tillämpats på en befintlig datauppsättning genom att göra en GET-förfrågan till [!DNL Dataset Service] API.

**API-format**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Unika `id` värdet för den datauppsättning vars etiketter du vill söka efter. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar dataanvändningsetiketterna som har tillämpats på datauppsättningen.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `labels` | En lista över dataanvändningsetiketter som har tillämpats på datauppsättningen. |
| `optionalLabels` | En lista över enskilda fält i datauppsättningen som har dataanvändningsetiketter tillämpade på sig. Följande underegenskaper krävs:<br/><br/>`option`: Ett objekt som innehåller [!DNL Experience Data Model] (XDM)-attribut för fältet. Följande tre egenskaper krävs:<ul><li>`id`: URI `$id` värdet för schemat som är associerat med fältet.</li><li>`contentType`: Anger schemats format och version. Se avsnittet om [schemaversion](../../xdm/api/getting-started.md#versioning) i XDM API-guiden för mer information.</li><li>`schemaPath`: Sökvägen till den aktuella schemaegenskapen, skriven i [JSON-pekare](../../landing/api-fundamentals.md#json-pointer) syntax.</li></ul>`labels`: En lista över dataanvändningsetiketter som du vill lägga till i fältet. |

- id: URI $id-värdet för XDM-schemat som datauppsättningen baseras på.
- contentType: Anger schemats format och version. Se avsnittet om [schemaversion](../../xdm/api/getting-started.md#versioning) i XDM API-guiden för mer information.
- schemaPath: Sökvägen till den aktuella schemaegenskapen, skriven i [JSON-pekare](../../landing/api-fundamentals.md#json-pointer) syntax.

## Tillämpa etiketter på en datauppsättning {#apply-dataset-labels}

Du kan skapa en uppsättning etiketter för en datauppsättning genom att ange dem i nyttolasten för en POST- eller PUT-begäran till [!DNL Dataset Service] API. Om du använder någon av dessa metoder skrivs befintliga etiketter över och ersätts med de som finns i nyttolasten.

**API-format**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Unika `id` värdet för den datauppsättning som du skapar etiketter för. |

**Begäran**

Följande begäran om POST lägger till en serie etiketter i datauppsättningen samt ett specifikt fält i datauppsättningen. Fälten i nyttolasten är desamma som skulle behövas för en PUT-begäran.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `labels` | En lista med dataanvändningsetiketter som du vill lägga till i datauppsättningen. |
| `optionalLabels` | En lista över enskilda fält i datauppsättningen som du vill lägga till etiketter i. Varje objekt i den här arrayen måste ha följande egenskaper:<br/><br/>`option`: Ett objekt som innehåller [!DNL Experience Data Model] (XDM)-attribut för fältet. Följande tre egenskaper krävs:<ul><li>`id`: URI `$id` värdet för schemat som är associerat med fältet.</li><li>`contentType`: Anger schemats format och version. Se avsnittet om [schemaversion](../../xdm/api/getting-started.md#versioning) i XDM API-guiden för mer information.</li><li>`schemaPath`: Sökvägen till den aktuella schemaegenskapen, skriven i [JSON-pekare](../../landing/api-fundamentals.md#json-pointer) syntax.</li></ul>`labels`: En lista över dataanvändningsetiketter som du vill lägga till i fältet. |

**Svar**

Ett lyckat svar returnerar etiketterna som har lagts till i datauppsättningen.

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## Ta bort etiketter från en datauppsättning {#remove-dataset-labels}

Du kan ta bort etiketterna som används i en datauppsättning genom att göra en DELETE-förfrågan till [!DNL Dataset Service] API.

**API-format**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | Unika `id` värdet för den datauppsättning vars etiketter du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar på HTTP-status 200 (OK), som anger att etiketterna har tagits bort. Du kan [söka efter befintliga etiketter](#look-up-dataset-labels) för datauppsättningen i ett separat anrop för att bekräfta detta.

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig hur du hanterar dataanvändningsetiketter med API:er.

När du har lagt till etiketter för dataanvändning på data- och fältnivå kan du börja importera data till [!DNL Experience Platform]. Om du vill veta mer kan du börja med att läsa [dokumentation om dataöverföring](../../ingestion/home.md).

Nu kan du även definiera dataanvändningsprinciper baserat på de etiketter du har använt. Mer information finns i [dataanvändningsprinciper - översikt](../policies/overview.md).

Mer information om hur du hanterar datauppsättningar i [!DNL Experience Platform], se [datauppsättningar, översikt](../../catalog/datasets/overview.md).