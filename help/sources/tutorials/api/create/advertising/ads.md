---
title: Koppla Google-annonser till Experience Platform med API:er
description: Lär dig hur du ansluter Adobe Experience Platform till Google Ads med API:t för Flow Service.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Anslut [!DNL Google Ads] till Experience Platform med API:t [!DNL Flow Service]

>[!NOTE]
>
>Källan [!DNL Google Ads] är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du lära dig hur du ansluter ditt [!DNL Google Ads]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Google Ads] med API:t [!DNL Flow Service].

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

### Samla in nödvändiga inloggningsuppgifter

Mer information om autentisering finns i [[!DNL Google Ads] källöversikten](../../../../connectors/advertising/ads.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till slutpunkten `/connections` och anger dina autentiseringsuppgifter för Google Ads som en del av parametrarna för begäran.

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
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v17"

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
| `auth.params.clientCustomerID` | Klientens kund-ID för ditt [!DNL Google Ads]-konto. |
| `auth.params.loginCustomerID` | Det användar-ID för inloggningskund som motsvarar ditt [!DNL Google Ads]-hanterarkonto. |
| `auth.params.developerToken` | Utvecklartoken för ditt [!DNL Google Ads]-konto. |
| `auth.params.refreshToken` | Uppdateringstoken för ditt [!DNL Google Ads]-konto. |
| `auth.params.clientID` | Klient-ID för ditt [!DNL Google Ads]-konto. |
| `auth.params.clientSecret` | Klienthemligheten för ditt [!DNL Google Ads]-konto. |
| `auth.params.googleAdsApiVersion` | API-versionen [!DNL Google Ads] som du använder. Den senaste versionen som stöds på Experience Platform är `v17`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Google Ads]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Skapa ett dataflöde för att importera annonsdata

Genom att följa den här självstudiekursen har du skapat en [!DNL Google Ads]-basanslutning med [!DNL Flow Service] API:t och anslutit ditt [!DNL Google Ads]-konto till Experience Platform. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta annonsdata till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/advertising.md)
