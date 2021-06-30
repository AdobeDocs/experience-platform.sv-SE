---
keywords: Experience Platform;hem;populära ämnen;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Skapa en Salesforce Service Cloud-källanslutning med API:t för flödestjänst
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Salesforce Service Cloud med API:t för flödestjänst.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: ff0f6bc6b8a57b678b329fe2b47c53919e0e2d64
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# Skapa en [!DNL Salesforce Service Cloud]-källanslutning med hjälp av API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Salesforce Service Cloud] med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Salesforce Service Cloud] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Salesforce Service Cloud] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `username` | Användarnamnet för ditt [!DNL Salesforce Service Cloud]-användarkonto. |
| `password` | Lösenordet för ditt [!DNL Salesforce Service Cloud]-konto. |
| `securityToken` | Säkerhetstoken för ditt [!DNL Salesforce Service Cloud]-konto. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce Service Cloud] är: `b66ab34-8619-49cb-96d1-39b37ede86ea`. |

Mer information om hur du kommer igång finns i [det här Salesforce Service Cloud-dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Salesforce Service Cloud] som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Salesforce Service Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Salesforce Service Cloud]-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Salesforce Service Cloud]-konto. |
| `auth.params.securityToken` | Säkerhetstoken som är associerad med ditt [!DNL Salesforce Service Cloud]-konto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Salesforce Service Cloud]: `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att undersöka ditt CRM-system i nästa steg.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Salesforce Service Cloud]-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda detta anslutnings-ID i nästa självstudiekurs när du lär dig hur du [utforskar lyckade kundsystem med API:t för Flow Service](../../explore/customer-success.md).
