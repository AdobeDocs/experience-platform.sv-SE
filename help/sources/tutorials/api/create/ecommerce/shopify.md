---
keywords: Experience Platform;hemmabruk;populära ämnen;Gör en kopia;förminska;e-handel
solution: Experience Platform
title: Skapa en anslutning till basen för Shopify-koppling med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Shopify till Adobe Experience Platform med API:t för Flow Service.
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: e8c6620a6d2447a577bd56192030ff4353c62c62
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---

# Skapa en [!DNL Shopify]-basanslutning med hjälp av API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Shopify] (kallas nedan &quot;[!DNL Shopify]&quot;) med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Sources]](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Shopify] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Shopify] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Slutpunkten för [!DNL Shopify]-servern. |
| `accessToken` | Åtkomsttoken för ditt [!DNL Shopify]-användarkonto. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Shopify] är: `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

Mer information om hur du kommer igång finns i det här [dokumentet för autentisering av Shopify](https://shopify.dev/concepts/about-apis/authentication).

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Shopify] som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Shopify]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | Slutpunkten för [!DNL Shopify]-servern. |
| `auth.params.accessToken` | Åtkomsttoken för ditt [!DNL Shopify]-användarkonto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Shopify]: `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Shopify]-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig att [utforska eCommerce-anslutningar med API:t för Flow Service](../../explore/ecommerce.md).
