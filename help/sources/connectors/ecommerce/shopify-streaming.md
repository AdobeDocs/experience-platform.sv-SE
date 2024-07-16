---
title: Shopify Streaming Source
description: Lär dig hur du skapar en källanslutning och ett dataflöde för att importera strömmande data från Shopify-instansen till Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>Källan [!DNL Shopify Streaming] är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Adobe Experience Platform har stöd för inmatning av data från direktuppspelningsprogram. Stöd för direktuppspelningsproviders är [!DNL Shopify].

## Förhandskrav {#prerequisites}

I följande avsnitt beskrivs de nödvändiga stegen som måste utföras innan källan [!DNL Shopify Streaming] används.

Du måste ha ett giltigt [!DNL Shopify]-partnerkonto för att kunna ansluta till [!DNL Shopify] API:er. Om du inte redan har ett partnerkonto kan du registrera dig på [[!DNL Shopify] partnerinstrumentpanelen](https://www.shopify.com/partners).

### Skapa ditt program

Med ett giltigt [!DNL Shopify]-partnerkonto kan du nu fortsätta och skapa din app med partnerinstrumentpanelen. Mer information om hur du skapar din app i [!DNL Shopify] finns i [[!DNL Shopify] guiden om hur du kommer igång](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

När appen har skapats hämtar du ditt **klient-ID** och **klienthemlighet** från fliken **klientautentiseringsuppgifter** på [!DNL Shopify] partners-kontrollpanelen. Klient-ID och klienthemlighet används i nästa steg för att hämta din auktoriseringskod och åtkomsttoken.

### Hämta din auktoriseringskod

Hämta sedan din auktoriseringskod genom att ange domänens `myshopify.com`-URL i webbläsaren, tillsammans med frågesträngar som definierar API-nyckeln, scope och omdirigerings-URI.

Formatet för den här URL:en är följande:

**API-format**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parameter | Beskrivning |
| --- | --- |
| `shop` | Din URL för underdomänen `myshopify.com`. |
| `api_key` | Ditt [!DNL Shopify]-klient-ID. Du kan hämta ditt klient-ID från fliken **klientautentiseringsuppgifter** på kontrollpanelen för [!DNL Shopify] partners. |
| `scopes` | Den typ av åtkomst som du vill definiera. Du kan till exempel ange omfattningar som `scope=write_orders,read_customers` för att tillåta behörigheter att ändra order och läsa kunder. |
| `redirect_uri` | URL:en för skriptet som ska generera åtkomsttoken. |

**Begäran**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Svar**

Ett lyckat svar returnerar din omdirigerings-URL, inklusive den auktoriseringskod som krävs för att generera din åtkomsttoken.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Hämta din åtkomsttoken

Nu när du har ditt klient-ID, din klienthemlighet och din behörighetskod kan du hämta din åtkomsttoken. Om du vill hämta din åtkomsttoken gör du en POST-förfrågan till domänens `myshopify.com`-URL när du lägger till den här URL:en med [!DNL Shopify's] API-slutpunkt: `/admin/oauth/access_token`.

**API-format**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Begäran**

Följande begäran genererar en åtkomsttoken för din [!DNL Shopify]-instans.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**Svar**

Ett lyckat svar returnerar din åtkomsttoken och dina behörighetsområden.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Skapa en webkrok för att strömma [!DNL Shopify]-data {#webhook}

Med hjälp av webhooks kan program förbli synkroniserade med dina [!DNL Shopify]-data eller utföra en åtgärd efter att en viss händelse inträffar i en butik. För direktuppspelning av [!DNL Shopify]-data till Experience Platform kan webhooks användas för att definiera http-slutpunkten och avsnitten för prenumeration.

**Begäran**

Följande begäran skapar en webkrok för dina [!DNL Shopify Streaming]-data.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| Parameter | Beskrivning |
| --- | --- | 
| `webhook.address` | Den http-slutpunkt dit direktuppspelningsmeddelanden skickas. |
| `webhook.topic` | Avsnittet om din webkroprenumeration. Mer information finns i [[!DNL Shopify] händelseguiden](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics) för webkrok. |
| `webhook.format` | Dataformatet. |

**Svar**

Ett lyckat svar returnerar information på din webkrok, inklusive motsvarande `id`, adress och annan metadatainformation.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### Begränsningar {#limitations}

Nedan följer en lista över kända begränsningar som du kan stöta på när du använder webbhooks med källan [!DNL Shopify Streaming].

* Det är inte säkert att du kan ordna leveransordningen för olika ämnen för samma resurs. Det är till exempel möjligt att en `products/update`-webkrok levereras före en `products/create`-webkrok.
* Du kan ställa in webkroken så att den levererar webkrockhändelser till en slutpunkt minst en gång. Det innebär att en slutpunkt kan ta emot samma händelse flera gånger. Du kan söka efter duplicerade webkrockhändelser genom att jämföra huvudet `X-Shopify-Webhook-Id` med tidigare händelser.
* [!DNL Shopify] behandlar HTTP 2xx-statussvar som lyckade meddelanden. Andra statuskodssvar betraktas som misslyckanden. [!DNL Shopify] innehåller en återförsöksmekanism för misslyckade webkrockmeddelanden. Om det inte finns **något svar efter att ha väntat i fem sekunder**, försöker [!DNL Shopify] ansluta igen **19 gånger** under de kommande **48 timmarna**. Om det fortfarande inte finns några svar i slutet av återförsöksperioden tar [!DNL Shopify] bort webkroken.

## Nästa steg

I följande självstudier beskrivs hur du ansluter [!DNL Shopify Streaming]-källan till Experience Platform med API:t och användargränssnittet:

* [Skapa en källanslutning och ett dataflöde för punktuppspelning med API:t för Flow Service](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Skapa en källanslutning och ett dataflöde för Shopify Streaming i användargränssnittet](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
