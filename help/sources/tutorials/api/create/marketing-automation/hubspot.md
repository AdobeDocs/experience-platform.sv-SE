---
keywords: Experience Platform;hem;populära ämnen;hubspot;Hubspot
solution: Experience Platform
title: Skapa en HubSpot Base-anslutning med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till HubSpot med API:t för Flow Service.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Skapa en [!DNL HubSpot] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL HubSpot] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL HubSpot] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL HubSpot]måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `clientId` | Klient-ID som är kopplat till din [!DNL HubSpot] program. |
| `clientSecret` | Klienthemligheten som är kopplad till din [!DNL HubSpot] program. |
| `accessToken` | Åtkomsttoken som fås när din OAuth-integration autentiseras initialt. |
| `refreshToken` | Den uppdateringstoken som erhölls när OAuth-integreringen autentiserades initialt. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL HubSpot] är: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Mer information om hur du kommer igång finns i [HubSpot-dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL HubSpot] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL HubSpot]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.clientId` | Klient-ID som är kopplat till din [!DNL HubSpot] program. |
| `auth.params.clientSecret` | Klienthemligheten som är kopplad till din [!DNL HubSpot] program. |
| `auth.params.accessToken` | Åtkomsttoken som fås när din OAuth-integration autentiseras initialt. |
| `auth.params.refreshToken` | Den uppdateringstoken som erhölls när OAuth-integreringen autentiserades initialt. |
| `connectionSpec.id` | The [!DNL HubSpot] anslutningsspecifikation-ID: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL HubSpot] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att ta fram data för automatiserad marknadsföring till plattformen med [!DNL Flow Service] API](../../collect/marketing-automation.md)
