---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-slutpunkt för etiketter
description: Lär dig hur du hanterar dataanvändningsetiketter i Experience Platform med hjälp av API:t för principtjänsten.
role: Developer
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 77d68a42b16c78cdc2b55f7776ba1c8ec98d8acd
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Slutpunkt för etiketter

Med etiketter för dataanvändning kan du kategorisera data enligt de användarprofiler som kan gälla för dessa data. Med slutpunkten `/labels` i [!DNL Policy Service API] kan du programmässigt hantera dataanvändningsetiketter i ditt upplevelseprogram.

>[!NOTE]
>
>Slutpunkten `/labels` används bara för att hämta, skapa och uppdatera dataanvändningsetiketter. Du kan inte ta bort etiketter. Du kan dock lägga till eller ta bort etiketter i datauppsättningar och fält med API-anrop. Instruktioner finns i guiden [Hantera datauppsättningsrubriker](../labels/dataset-api.md) för dokumentet.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett [!DNL Experience Platform] -API.

## Hämta en lista med etiketter {#list}

Du kan visa alla `core` - eller `custom`-etiketter genom att göra en GET-förfrågan till `/labels/core` respektive `/labels/custom`.

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

Ett godkänt svar returnerar en lista med anpassade etiketter som hämtats från systemet. Eftersom exempelbegäran ovan gjordes till `/labels/custom` visas endast anpassade etiketter i svaret nedan.

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

## Söka efter en etikett {#look-up}

Du kan söka efter en specifik etikett genom att ta med etikettens `name`-egenskap i sökvägen för en GET-begäran till [!DNL Policy Service] API.

**API-format**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LABEL_NAME}` | Egenskapen `name` för den anpassade etikett som du vill söka efter. |

**Begäran**

Följande begäran hämtar den anpassade etiketten `L2`, som anges i sökvägen.

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

## Skapa eller uppdatera en anpassad etikett {#create-update}

Om du vill skapa eller uppdatera en anpassad etikett måste du göra en PUT-förfrågan till API:t [!DNL Policy Service].

>[!NOTE]
>
>Om du vill ta bort etiketter från en datauppsättning kan du utföra en [PUT-begäran på API:t för datauppsättningstjänsten](../labels/dataset-api.md#remove) eller använda [datauppsättningsgränssnittet](../labels/user-guide.md#remove-labels-from-a-dataset).

**API-format**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LABEL_NAME}` | Egenskapen `name` för en anpassad etikett. Om det inte finns någon egen etikett med det här namnet skapas en ny etikett. Om det finns en sådan kommer den etiketten att uppdateras. |

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
| `category` | Etikettens kategori. Du kan skapa egna kategorier för anpassade etiketter, men du bör använda `Custom` om du vill att etiketten ska visas i användargränssnittet. |
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

## Nästa steg

I den här guiden beskrivs användningen av slutpunkten `/labels` i API:t för principtjänsten. Anvisningar om hur du använder etiketter på datauppsättningar och fält finns i [API-guiden för datauppsättningsrubriker](../labels/dataset-api.md).
