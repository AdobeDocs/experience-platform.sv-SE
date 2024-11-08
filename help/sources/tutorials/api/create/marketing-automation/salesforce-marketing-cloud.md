---
title: Skapa en Salesforce Marketing Cloud Base-anslutning med API:t för Flow Service
description: Lär dig hur du autentiserar ditt Salesforce Marketing Cloud-konto mot Experience Platform med hjälp av API:t för Flow Service.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Skapa en [!DNL Salesforce Marketing Cloud]-basanslutning med API:t [!DNL Flow Service]

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]-källan kommer att bli inaktuell i slutet av maj 2025.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL Salesforce Marketing Cloud] med [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Salesforce Marketing Cloud] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Salesforce Marketing Cloud] måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Programmets värdserver. Detta är ofta din underdomän. **Obs!** När du anger ditt `host`-värde måste du ange `{subdomain}.rest.marketingcloudapis.com`. Om din värd-URL till exempel är `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/` måste du ange `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` som värdvärde. |
| `clientId` | Klient-ID som är associerat med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce Marketing Cloud] är: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Mer information om hur du kommer igång finns i det här [[!DNL Salesforce Marketing Cloud] dokumentet](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Skapa en basanslutning

>[!IMPORTANT]
>
>Inläsning av anpassade objekt stöds för närvarande inte av källintegreringen [!DNL Salesforce Marketing Cloud].

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina [!DNL Salesforce Marketing Cloud] autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.clientId` | Klient-ID som är associerat med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `auth.params.clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Salesforce Marketing Cloud]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att överföra data för automatiserad marknadsföring till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/marketing-automation.md)
