---
keywords: Experience Platform;hem;populära ämnen;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Skapa en källanslutning till Apache Cassandra med API:t för flödestjänst
type: Tutorial
description: Lär dig hur du ansluter Apache Cassandra till Adobe Experience Platform med API:t för Flow Service.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Skapa en [!DNL Apache Cassandra] källanslutning med [!DNL Flow Service] API

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används [!DNL Flow Service] API för att vägleda dig genom stegen för att ansluta [!DNL Apache Cassandra] (nedan kallat &quot;Cassandra&quot;) till [!DNL Experience Platform].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till Cassandra med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Cassandra]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för [!DNL Cassandra] server. |
| `port` | TCP-porten som [!DNL Cassandra] servern använder för att avlyssna klientanslutningar. Standardporten är `9042`. |
| `username` | Användarnamnet som används för att ansluta till [!DNL Cassandra] server för autentisering. |
| `password` | Lösenordet för att ansluta till [!DNL Cassandra] server för autentisering. |
| `connectionSpec.id` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikations-ID för [!DNL Cassandra] är `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Mer information om hur du kommer igång finns i [det här Cassandra-dokumentet](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en kontakt krävs per [!DNL Cassandra] som det kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att skapa en [!DNL Cassandra] måste dess unika anslutningsspecifikation-ID anges som en del av POSTEN. Anslutningsspecifikations-ID för [!DNL Cassandra] är `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | IP-adressen eller värdnamnet för [!DNL Cassandra] server. |
| `auth.params.port` | TCP-porten som [!DNL Cassandra] servern använder för att avlyssna klientanslutningar. Standardporten är `9042`. |
| `auth.params.username` | Användarnamnet som används för att ansluta till [!DNL Cassandra] server för autentisering. |
| `auth.params.password` | Lösenordet för att ansluta till [!DNL Cassandra] server för autentisering. |
| `connectionSpec.id` | The [!DNL Cassandra] anslutningsspec-ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Cassandra] anslutning med [!DNL Flow Service] API och har fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig hur du [utforska databaser med API:t för Flow Service](../../explore/database-nosql.md).
