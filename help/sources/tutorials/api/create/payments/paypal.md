---
keywords: Experience Platform;hem;populära ämnen;PayPal-kontakt;Paypal;Paypal
solution: Experience Platform
title: Skapa en PayPal-basanslutning med API:t för Flow Service
type: Tutorial
description: Lär dig hur du ansluter PayPal till Adobe Experience Platform med API:t för Flow Service.
exl-id: 5e6ca7b4-5e2f-4706-a339-ac159e2e0938
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Skapa en [!DNL PayPal]-basanslutning med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>[!DNL PayPal]-källan kommer att bli inaktuell i slutet av maj 2025. Du kan använda [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) i stället för [!DNL PayPal]-källan.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL PayPal] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL PayPal] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL PayPal] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | URL:en för instansen [!DNL PayPal]. (standard: api.sandbox.paypal.com). |
| `clientId` | Klient-ID som är associerat med ditt [!DNL PayPal]-program. |
| `clientSecret` | Klienthemligheten som är associerad med ditt [!DNL PayPal]-program. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL PayPal] är: `221c7626-58f6-4eec-8ee2-042b0226f03b` |

Mer information om hur du kommer igång finns i [det här PayPal-dokumentet](https://developer.paypal.com/docs/api/overview/#get-credentials).

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till slutpunkten `/connections` och anger dina autentiseringsuppgifter för [!DNL PayPal] som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL PayPal]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal connection",
        "description": "Paypal connection",
        "auth": {
        "specName": "Client-Id-Secret Based Authentication",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | URL:en för instansen [!DNL PayPal]. |
| `auth.params.clientId` | Klient-ID som är associerat med din [!DNL PayPal]-instans. |
| `auth.params.clientSecret` | Klienthemligheten som är associerad med din [!DNL PayPal]-instans. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL PayPal]: `221c7626-58f6-4eec-8ee2-042b0226f03b`. |

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL PayPal]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att skicka betalningsdata till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/payments.md)
