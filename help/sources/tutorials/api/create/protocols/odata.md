---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en allmän OData-koppling med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 34334a6ff5a3f0c16ad32b4d0438d4ee8513372f

---


# Skapa en allmän OData-koppling med API:t för Flow Service

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta generiska OData till Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till OData med API:t för Flow Service.

### Samla in nödvändiga inloggningsuppgifter

För att Flow Service ska kunna ansluta till OData måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| url | rot-URL:en för OData-tjänsten. |
| connectionSpec.id | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikations-ID för OData är: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3` |

Mer information om hur du kommer igång finns i [detta OData-dokument](https://www.odata.org/getting-started/basic-tutorial/).

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

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per OData-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att skapa en OData-anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POST-begäran. Anslutningsspecifikationens ID för OData är `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Protocols",
        "description": "A test connection for a Protocols source",
        "auth": {
            "specName": "Anonymous Authentication",
        "params": {
            "url" :  "{URL}"
            }
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.url` | Värden för OData-servern. |
| `connectionSpec.id` | OData-anslutningsspecifikations-ID: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en OData-anslutning med API:t för Flow Service och fått anslutningens unika ID-värde. Du kan använda detta ID i nästa självstudiekurs när du lär dig hur du [utforskar protokollprogram med API:t](../../explore/protocols.md)för Flow Service.