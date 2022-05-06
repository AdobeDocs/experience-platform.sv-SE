---
keywords: Experience Platform;hem;populära ämnen;Azure Azure-Data Explorer;Azure-Data Explorer;Azure-Data Explorer
solution: Experience Platform
title: Skapa en Azure Azure Data Explorer Base-anslutning med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Azure Azure Data Explorer till Adobe Experience Platform med API:t för Flow Service.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# Skapa en [!DNL Azure Azure Data Explorer] basanslutning med [!DNL Flow Service] API

>[!NOTE]
>
>The [!DNL Azure Azure Data Explorer] anslutningen är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Azure Data Explorer] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Azure Data Explorer] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Azure Data Explorer]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `endpoint` | Slutpunkten för [!DNL Azure Data Explorer] server. |
| `database` | Namnet på [!DNL Azure Data Explorer] databas. |
| `tenant` | Det unika klient-ID som används för att ansluta till [!DNL Azure Data Explorer] databas. |
| `servicePrincipalId` | Det unika tjänstens huvudnamn-ID som används för att ansluta till [!DNL Azure Data Explorer] databas. |
| `servicePrincipalKey` | Den unika huvudnyckeln för tjänsten som används för att ansluta till [!DNL Azure Data Explorer] databas. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Azure Data Explorer] är `0479cc14-7651-4354-b233-7480606c2ac3`. |

Mer information om hur du kommer igång finns i [[!DNL Azure Data Explorer] dokument](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Azure Data Explorer] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Azure Data Explorer]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.endpoint` | Slutpunkten för [!DNL Azure Data Explorer] server. |
| `auth.params.database` | Namnet på [!DNL Azure Data Explorer] databas. |
| `auth.params.tenant` | Det unika klient-ID som används för att ansluta till [!DNL Azure Data Explorer] databas. |
| `auth.params.servicePrincipalId` | Det unika tjänstens huvudnamn-ID som används för att ansluta till [!DNL Azure Data Explorer] databas. |
| `auth.params.servicePrincipalKey` | Den unika huvudnyckeln för tjänsten som används för att ansluta till [!DNL Azure Data Explorer] databas. |
| `connectionSpec.id` | The [!DNL Azure Data Explorer] anslutningsspecifikation-ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Azure Data Explorer] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med [!DNL Flow Service] API](../../collect/database-nosql.md)
