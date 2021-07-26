---
keywords: Experience Platform;hem;populära ämnen;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Skapa en Salesforce Marketing Cloud Base-anslutning med API:t för flödestjänsten
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Salesforce Marketing Cloud med API:t för Flow Service.
source-git-commit: 56458ed6e74a76e2787ab3b9f1409b11556bdee2
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Skapa en [!DNL Salesforce Marketing Cloud]-basanslutning med hjälp av API:t [!DNL Flow Service]

>[!NOTE]
>
>Källan [!DNL Salesforce Marketing Cloud] är i betaversion. Mer information om hur du använder betatecknade källor finns i [källöversikten](../../../../home.md#terms-and-conditions).

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Salesforce Marketing Cloud] med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Salesforce Marketing Cloud] med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Salesforce Marketing Cloud] måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Programmets värdserver. Detta är ofta din underdomän. |
| `clientId` | Klient-ID som är associerat med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce Marketing Cloud] är: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

Mer information om hur du kommer igång finns i det här [[!DNL Salesforce Marketing Cloud] dokumentet](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Salesforce Marketing Cloud] som en del av begärandetexten.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "id": "cea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.clientId` | Klient-ID som är associerat med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `auth.params.clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Salesforce Marketing Cloud]: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

I den här självstudiekursen har du skapat en [!DNL Salesforce Marketing Cloud]-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda detta anslutnings-ID i nästa självstudiekurs när du lär dig att [utforska automatiseringssystem för marknadsföring med API:t för Flow Service](../../explore/marketing-automation.md).
