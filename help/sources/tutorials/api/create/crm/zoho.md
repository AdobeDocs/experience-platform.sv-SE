---
keywords: Experience Platform;hem;populära ämnen;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Skapa en Zoho CRM-basanslutning med API:t för flödestjänsten
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Zoho CRM med API:t för Flow Service.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Skapa en [!DNL Zoho CRM] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Zoho CRM] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Zoho CRM] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Zoho CRM]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `endpoint` | Slutpunkten för [!DNL Zoho CRM] servern som du begär. |
| `accountsUrl` | Konton-URL:en används för att generera din åtkomst och uppdatera tokens. URL:en måste vara domänspecifik. |
| `clientId` | Klient-ID som motsvarar ditt [!DNL Zoho CRM] användarkonto. |
| `clientSecret` | Klienthemligheten som motsvarar din [!DNL Zoho CRM] användarkonto. |
| `accessToken` | Åtkomsttoken ger dig säker och tillfällig åtkomst till din [!DNL Zoho CRM] konto. |
| `refreshToken` | En uppdateringstoken är en token som används för att generera en ny åtkomsttoken när din åtkomsttoken har upphört att gälla. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Zoho CRM] är: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Mer information om dessa autentiseringsuppgifter finns i dokumentationen om [[!DNL Zoho CRM] autentisering](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Zoho CRM] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

>[!TIP]
>
>Din konto-URL-domän måste motsvara rätt domänplats. Följande är de olika domänerna och deras motsvarande konto-URL:er:<ul><li>USA: https://accounts.zoho.com</li><li>Australien: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Indien: https://accounts.zoho.in</li><li>Kina: https://accounts.zoho.com.cn</li></ul>

Följande begäran skapar en basanslutning för [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Namnet på [!DNL Zoho CRM] basanslutning. Du kan använda det här namnet för att söka efter [!DNL Zoho CRM] basanslutning. |
| `description` | En valfri beskrivning av [!DNL Zoho CRM] basanslutning. |
| `auth.specName` | Autentiseringstypen som används för anslutningen. |
| `auth.params.endpoint` | Slutpunkten för [!DNL Zoho CRM] servern som du begär. |
| `auth.params.accountsUrl` | Konton-URL:en används för att skapa din åtkomst och uppdatera tokens. URL:en måste vara domänspecifik. |
| `auth.params.clientId` | Klient-ID som motsvarar ditt [!DNL Zoho CRM] användarkonto. |
| `auth.params.clientSecret` | Klienthemligheten som motsvarar din [!DNL Zoho CRM] användarkonto. |
| `auth.params.accessToken` | Åtkomsttoken ger dig säker och tillfällig åtkomst till din [!DNL Zoho CRM] konto. |
| `auth.params.refreshToken` | En uppdateringstoken är en token som används för att generera en ny åtkomsttoken när din åtkomsttoken har upphört att gälla. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Zoho] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta CRM-data till plattformen med [!DNL Flow Service] API](../../collect/crm.md)
