---
keywords: Experience Platform;hemmabruk;populära ämnen;Gör en kopia;förminska;e-handel
solution: Experience Platform
title: Skapa en anslutning för Shopify-kopplingskälla med API:t för Flow Service
topic: översikt
type: Självstudiekurs
description: Lär dig hur du ansluter Shopify till Adobe Experience Platform med API:t för Flow Service.
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---


# Skapa en [!DNL Shopify]-källanslutning med hjälp av API:t [!DNL Flow Service]

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) för att vägleda dig genom stegen för att ansluta [!DNL Shopify] till [!DNL Experience Platform].

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
| `connectionSpec` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikations-ID för [!DNL Shopify] är: `4f63aa36-bd48-4e33-bb83-49fbcd11c708` |

Mer information om hur du kommer igång finns i det här [dokumentet för autentisering av Shopify](https://shopify.dev/concepts/about-apis/authentication).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per [!DNL Shopify]-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL Shopify]-anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POSTEN. Anslutningsspecifikationens ID för [!DNL Shopify] är `4f63aa36-bd48-4e33-bb83-49fbcd11c708`.

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
                "accessToken": "{ACCCESS_TOKEN}"
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