---
keywords: Experience Platform;hem;populära ämnen;Fyrkant;Fyrkant
title: Skapa en kvadratisk basanslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Square till Adobe Experience Platform med API:t för Flow Service.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Skapa en [!DNL Square]-basanslutning med API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL Square] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Square] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Square] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `host` | URL:en för instansen [!DNL Square]. |
| `clientId` | Klient-ID som är associerat med ditt [!DNL Square]-konto. |
| `clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Square]-konto. |
| `accessToken` | Åtkomsttoken används för att autentisera ditt [!DNL Square]-konto med OAuth 2.0-autentisering. Åtkomsttoken kan hämtas från [!DNL Square]. |
| `refreshToken` | Uppdateringstoken används för att generera nya åtkomsttoken när din nuvarande åtkomsttoken upphör att gälla. Uppdateringstoken kan hämtas från [!DNL Square]. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Square] är: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Mer information om dessa autentiseringsuppgifter och hur du hämtar dem finns i [[!DNL Square] dokumentationen om OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till slutpunkten `/connections` och anger dina autentiseringsuppgifter för [!DNL Square] som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | URL:en för instansen [!DNL Square]. |
| `auth.params.clientId` | Klient-ID som är associerat med ditt [!DNL Square]-konto. |
| `auth.params.clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Square]-konto. |
| `auth.params.accessToken` | Åtkomsttoken används för att autentisera ditt [!DNL Square]-konto med OAuth 2.0-autentisering. Åtkomsttoken kan hämtas från [!DNL Square]. |
| `auth.params.refreshToken` | Uppdateringstoken används för att generera nya åtkomsttoken när din nuvarande åtkomsttoken upphör att gälla. Uppdateringstoken kan hämtas från [!DNL Square]. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Square]: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Square]-anslutning med API:t [!DNL Flow Service] och fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig hur du [utforskar betalningsprogram med API:t för Flow Service ](../../explore/payments.md).
