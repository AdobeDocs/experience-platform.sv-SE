---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Slutpunkt för etiketter
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# Slutpunkt för etiketter

Med etiketter för dataanvändning kan du kategorisera data enligt de användarprofiler som kan gälla för dessa data. Med slutpunkten i `/labels` [!DNL Policy Service API] kan du programmässigt hantera dataanvändningsetiketter i ert upplevelseprogram.

>[!NOTE]
>
>Slutpunkten används bara för att hämta, skapa och uppdatera etiketter för dataanvändning. `/labels` Anvisningar om hur du lägger till etiketter i datauppsättningar och fält med API-anrop finns i handboken om [hantering av datauppsättningsrubriker](../labels/dataset-api.md).

## Komma igång

API-slutpunkten som används i den här handboken är en del av [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Innan du fortsätter bör du läsa [Komma igång-guiden](getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API i det här dokumentet samt viktig information om vilka huvuden som krävs för att kunna anropa valfritt [!DNL Experience Platform] -API.

## Hämta en lista med etiketter {#list}

Du kan visa alla `core` eller `custom` etiketter genom att göra en GET-förfrågan till `/labels/core` respektive `/labels/custom`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med anpassade etiketter som hämtats från systemet. Eftersom exempelbegäran gjordes till `/labels/custom`visar svaret nedan endast anpassade etiketter.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Du kan söka efter en specifik etikett genom att ta med etikettens `name` egenskap i sökvägen för en GET-begäran till [!DNL Policy Service] API:t.

**API-format**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LABEL_NAME}` | Egenskapen `name` för den anpassade etikett som du vill söka efter. |

**Begäran**

Följande begäran hämtar den anpassade etiketten `L2`enligt sökvägen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

Om du vill skapa eller uppdatera en anpassad etikett måste du göra en PUT-begäran till [!DNL Policy Service] API:t.

**API-format**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{LABEL_NAME}` | Egenskapen `name` för en anpassad etikett. Om det inte finns någon egen etikett med det här namnet skapas en ny etikett. Om det finns en sådan kommer den etiketten att uppdateras. |

**Begäran**

Följande begäran skapar en ny etikett `L3`som beskriver data som innehåller information om kundernas valda betalningsplaner.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `category` | Etikettens kategori. Du kan skapa egna kategorier för anpassade etiketter, men du bör använda `Custom` dem om du vill att etiketten ska visas i användargränssnittet. |
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
  "imsOrg": "{IMS_ORG}",
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

Den här guiden beskriver användningen av `/labels` slutpunkten i API:t för principtjänsten. Anvisningar om hur du använder etiketter på datauppsättningar och fält finns i API-handboken för [datauppsättningsrubriker](../labels/dataset-api.md).