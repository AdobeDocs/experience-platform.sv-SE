---
keywords: Experience Platform;hem;populära ämnen;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Skapa en Salesforce Marketing Cloud Base-anslutning med API:t för flödestjänsten
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Salesforce Marketing Cloud med API:t för Flow Service.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 1%

---

# Skapa en [!DNL Salesforce Marketing Cloud] basanslutning med [!DNL Flow Service] API

>[!NOTE]
>
>The [!DNL Salesforce Marketing Cloud] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Salesforce Marketing Cloud] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Salesforce Marketing Cloud] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Salesforce Marketing Cloud]måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Programmets värdserver. Detta är ofta din underdomän. **Obs!** När du anger `host` behöver du bara ange underdomänen och inte hela URL:en. Om din värd-URL till exempel är `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`behöver du bara ange `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` som värdvärde. |
| `clientId` | Klient-ID som är kopplat till din [!DNL Salesforce Marketing Cloud] program. |
| `clientSecret` | Klienthemligheten som är kopplad till din [!DNL Salesforce Marketing Cloud] program. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce Marketing Cloud] är: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Mer information om hur du kommer igång finns i [[!DNL Salesforce Marketing Cloud] dokument](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Salesforce Marketing Cloud] autentiseringsuppgifter som en del av begärandetexten.

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
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
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
| `auth.params.clientId` | Klient-ID som är kopplat till din [!DNL Salesforce Marketing Cloud] program. |
| `auth.params.clientSecret` | Klienthemligheten som är kopplad till din [!DNL Salesforce Marketing Cloud] program. |
| `connectionSpec.id` | The [!DNL Salesforce Marketing Cloud] anslutningsspecifikation-ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Salesforce Marketing Cloud] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att ta fram data för automatiserad marknadsföring till plattformen med [!DNL Flow Service] API](../../collect/marketing-automation.md)
