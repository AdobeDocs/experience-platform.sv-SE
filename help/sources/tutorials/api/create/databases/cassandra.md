---
keywords: Experience Platform;home;popular topics;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Skapa en Apache Cassandra-anslutning med API:t för Flow Service
topic: overview
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Apache Cassandra (nedan kallat "Cassandra") till Experience Platform.
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---


# Skapa en [!DNL Apache Cassandra] koppling med [!DNL Flow Service] API:t

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används API:t för att vägleda dig genom de olika stegen för att ansluta [!DNL Flow Service] (nedan kallat &quot;Cassandra&quot;) till [!DNL Apache Cassandra] [!DNL Experience Platform].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till Cassandra med [!DNL Flow Service] -API:t.

### Samla in nödvändiga inloggningsuppgifter

För [!DNL Flow Service] att kunna ansluta till [!DNL Cassandra]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för [!DNL Cassandra] servern. |
| `port` | Den TCP-port som servern använder för att avlyssna klientanslutningar. [!DNL Cassandra] avlyssning. Standardporten är `9042`. |
| `username` | Användarnamnet som används för att ansluta till [!DNL Cassandra] servern för autentisering. |
| `password` | Lösenordet för att ansluta till [!DNL Cassandra] servern för autentisering. |
| `connectionSpec.id` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikationens ID för [!DNL Cassandra] är `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Mer information om hur du kommer igång finns i [det här Cassandra-dokumentet](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en koppling krävs per [!DNL Cassandra] konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL Cassandra] anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POSTEN. Anslutningsspecifikationens ID för [!DNL Cassandra] är `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | IP-adressen eller värdnamnet för [!DNL Cassandra] servern. |
| `auth.params.port` | Den TCP-port som servern använder för att avlyssna klientanslutningar. [!DNL Cassandra] avlyssning. Standardporten är `9042`. |
| `auth.params.username` | Användarnamnet som används för att ansluta till [!DNL Cassandra] servern för autentisering. |
| `auth.params.password` | Lösenordet för att ansluta till [!DNL Cassandra] servern för autentisering. |
| `connectionSpec.id` | Anslutningens spec-ID [!DNL Cassandra] : `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Cassandra] anslutning med hjälp av [!DNL Flow Service] API:t och fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig hur du [utforskar databaser med API:t](../../explore/database-nosql.md)för Flow Service.
