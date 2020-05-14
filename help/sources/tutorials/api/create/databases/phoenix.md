---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Phoenix-anslutning med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# Skapa en Phoenix-anslutning med API:t för Flow Service

>[!NOTE]
>Phoenix-kontakten är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta en Phoenix-databas till Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till Phoenix med API:t för Flow Service.

### Samla in nödvändiga inloggningsuppgifter

För att Flow Service ska kunna ansluta till Phoenix måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Phoenix-serverns IP-adress eller värdnamn. |
| `username` | Användarnamnet som du använder för att komma åt Phoenix Server. |
| `password` | Lösenordet som motsvarar användaren. |
| `port` | Den TCP-port som Phoenix-servern använder för att lyssna efter klientanslutningar. Om du ansluter till Azure HDInsights anger du port som 443. |
| `httpPath` | Den del av URL:en som motsvarar Phoenix-servern. Ange /hbasephoenix0 om du använder Azure HDInsights-kluster. |
| `enableSsl` | Ett booleskt värde. Anger om anslutningar till servern krypteras med SSL. |
| `connectionSpec.id` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikation-ID för Phoenix är: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Mer information om hur du kommer igång finns i [det här Phoenix-dokumentet](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör Flow Service, isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per Phoenix-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att skapa en Phoenix-anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POST-begäran. Anslutningsspecifikation-ID för Phoenix är `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
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
| `auth.params.host` | Värden för Phoenix-servern. |
| `auth.params.username` | Användarnamnet som är kopplat till din Phoenix-anslutning. |
| `auth.params.password` | Lösenordet som är kopplat till din Phoenix-anslutning. |
| `auth.params.port` | TCP-porten för din Phoenix-anslutning. |
| `auth.params.httpPath` | Den partiella http-sökvägen för din Phoenix-anslutning. |
| `auth.params.enableSsl` | Det booleska värdet som anger om anslutningarna till servern är krypterade med SSL. |
| `connectionSpec.id` | Phoenix-anslutningsspecifikation-ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en Phoenix-anslutning med API:t för Flow Service och fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig hur du [utforskar databaser med API:t](../../explore/database-nosql.md)för Flow Service.