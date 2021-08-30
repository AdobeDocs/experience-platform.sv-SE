---
keywords: Experience Platform;hem;populära ämnen;veeva crm;Veeva CRM;Veeva;
solution: Experience Platform
title: Skapa en Vector CRM-basanslutning med API:t för flödestjänsten
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Veeva CRM med API:t för Flow Service.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 1%

---

# (Beta) Skapa en [!DNL Veeva CRM]-basanslutning med hjälp av API:t [!DNL Flow Service]

>[!NOTE]
>
>Källan [!DNL Veeva CRM] är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Veeva CRM] med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Veeva CRM] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Veeva CRM] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `environmentUrl` | URL:en för din [!DNL Veeva CRM]-instans. |
| `username` | Användarnamnsvärdet för ditt [!DNL Veeva CRM]-konto. |
| `password` | Lösenordsvärdet för ditt [!DNL Veeva CRM]-konto. |
| `securityToken` | Säkerhetstoken för din [!DNL Veeva CRM]-instans. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Veeva CRM] är: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Mer information om dessa värden finns i det här [[!DNL Veeva CRM] dokumentet](https://developer.veevacrm.com/api/#order-management-rest-api).

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Veeva CRM] som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Namnet på din [!DNL Veeva CRM]-basanslutning. Du kan använda det här namnet för att söka efter din [!DNL Veeva CRM]-basanslutning. |
| `description` | En valfri beskrivning för din [!DNL Veeva CRM]-basanslutning. |
| `auth.specName` | Autentiseringstypen som används för anslutningen. |
| `auth.params.environmentUrl` | URL:en för din [!DNL Veeva CRM]-instans. |
| `auth.params.username` | Användarnamnsvärdet för ditt [!DNL Veeva CRM]-konto. |
| `auth.params.password` | Lösenordsvärdet för ditt [!DNL Veeva CRM]-konto. |
| `auth.params.securityToken` | Säkerhetstoken för din [!DNL Veeva CRM]-instans. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Svar**

Ett lyckat svar returnerar information om den nyskapade basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Veeva CRM]-basanslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda detta ID i nästa självstudiekurs när du lär dig hur du [utforskar CRM-system med API:t för Flow Service](../../explore/crm.md).
