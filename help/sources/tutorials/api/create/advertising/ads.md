---
keywords: Experience Platform;hem;populära ämnen;Google ads;Google Ads;Google ads;ads
title: Skapa en Google Ads Base Connection med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Google Ads med API:t för Flow Service.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# Skapa en Google Ads-basanslutning med [!DNL Flow Service] API

>[!NOTE]
>
>Google Ads-källan är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för Google Ads med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av Experience Platform-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till Google Ads med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] Om du vill ansluta till Google Ads måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `clientCustomerId` | Klientens kund-ID är det kontonummer som motsvarar det Google Ads-klientkonto som du vill hantera med API:t för Google Ads. Detta ID följer mallen för `123-456-7890`. |
| `developerToken` | Med utvecklartoken får du tillgång till Google Ads API. Du kan använda samma utvecklartoken för att göra förfrågningar mot alla dina Google Ads-konton. Hämta din utvecklartoken från [logga in på ditt chefskonto](https://ads.google.com/home/tools/manager-accounts/) och sedan navigera till [!DNL API Center] sida. |
| `refreshToken` | Uppdateringstoken är en del av [!DNL OAuth2] autentisering. Med denna token kan du återskapa dina åtkomsttoken när de har upphört att gälla. |
| `clientId` | Klient-ID används tillsammans med klienthemligheten som en del av [!DNL OAuth2] autentisering. Tillsammans gör klient-ID och klienthemlighet det möjligt för programmet att agera för ditt kontos räkning genom att identifiera ditt program för Google. |
| `clientSecret` | Klienthemligheten används tillsammans med klient-ID som en del av [!DNL OAuth2] autentisering. Tillsammans gör klient-ID och klienthemlighet det möjligt för programmet att agera för ditt kontos räkning genom att identifiera ditt program för Google. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för Google Ads är: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Läs API-översiktsdokumentet för [mer information om hur du kommer igång med Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkten när du anger inloggningsuppgifter för Google Ads som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för Google Ads:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.clientCustomerID` | Kund-ID för ditt Google Ads-konto. |
| `auth.params.developerToken` | Utvecklartoken för ditt Google Ads-konto. |
| `auth.params.refreshToken` | Uppdateringstoken för ditt Google Ads-konto. |
| `auth.params.clientID` | Klient-ID för ditt Google Ads-konto. |
| `auth.params.clientSecret` | Klienthemligheten för ditt Google Ads-konto. |
| `connectionSpec.id` | Anslutningsspecifikation-ID för Google Ads: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en Google Ads-basanslutning med hjälp av [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta annonsdata till plattformen med [!DNL Flow Service] API](../../collect/advertising.md)
