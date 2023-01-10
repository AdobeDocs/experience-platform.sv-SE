---
keywords: Experience Platform;hem;populära ämnen;Phoenix;phoenix
solution: Experience Platform
title: Skapa en Phoenix-basanslutning med API:t för Flow Service
type: Tutorial
description: Lär dig hur du ansluter en Phoenix-databas till Adobe Experience Platform med API:t för Flow Service.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# Skapa en [!DNL Phoenix] basanslutning med [!DNL Flow Service] API

>[!NOTE]
>
>The [!DNL Phoenix] anslutningen är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används [!DNL Flow Service] API för att vägleda dig genom stegen för att ansluta en [!DNL Phoenix] databas till [!DNL Experience Platform].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Phoenix] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Phoenix]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för [!DNL Phoenix] server. |
| `username` | Användarnamnet som du använder för att komma åt [!DNL Phoenix] Server. |
| `password` | Lösenordet som motsvarar användaren. |
| `port` | TCP-porten som [!DNL Phoenix] servern använder för att avlyssna klientanslutningar. Om du ansluter till [!DNL Azure] HDInsights, ange port som 443. |
| `httpPath` | Den del av URL:en som motsvarar [!DNL Phoenix] server. Ange /hbasephoenix0 om du använder [!DNL Azure] HDInsights-kluster. |
| `enableSsl` | Ett booleskt värde. Anger om anslutningar till servern krypteras med SSL. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Phoenix] är: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Mer information om hur du kommer igång finns i [det här Phoenix-dokumentet](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Phoenix] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Phoenix]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}",
            "port": {PORT},
            "httpPath": "{PATH}",
            "enableSsl": {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | Värden för [!DNL Phoenix] server. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Phoenix] anslutning. |
| `auth.params.password` | Lösenordet som är kopplat till [!DNL Phoenix] anslutning. |
| `auth.params.port` | TCP-porten för din [!DNL Phoenix] anslutning. |
| `auth.params.httpPath` | Den partiella http-sökvägen för [!DNL Phoenix] anslutning. |
| `auth.params.enableSsl` | Det booleska värdet som anger om anslutningarna till servern är krypterade med SSL. |
| `connectionSpec.id` | The [!DNL Phoenix] anslutningsspecifikation-ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Phoenix] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med [!DNL Flow Service] API](../../collect/database-nosql.md)
