---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Azure File Storage-koppling med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 3a882656f93b86093b356be5dbc12b3e4321cfb8
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# Skapa en Azure File Storage-koppling med API:t för Flow Service

>[!NOTE]
>Azure File Storage Connector är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Azure File Storage till Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till Azure File Storage med API:t för Flow Service.

### Samla in nödvändiga inloggningsuppgifter

För att Flow Service ska kunna ansluta till Azure File Storage måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Slutpunkten för Azure File Storage-instansen som du försöker komma åt. |
| `userId` | Användaren med tillräcklig åtkomst till Azure File Storage-slutpunkten. |
| `password` | Lösenordet för din Azure File Storage-instans |
| ID för anslutningsspecifikation | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspec-ID för Azure File Storage är: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Mer information om hur du kommer igång finns i [det här Azure File Storage-dokumentet](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

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

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per Azure File Storage-konto eftersom det kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att skapa en Azure File Storage-anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POST-begäran. Anslutningsspecifikations-ID för Azure File Storage är `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | Slutpunkten för Azure File Storage-instansen som du försöker komma åt. |
| `auth.params.userId` | Användaren med tillräcklig åtkomst till Azure File Storage-slutpunkten. |
| `auth.params.password` | Åtkomstnyckeln för Azure File Storage. |
| `connectionSpec.id` | Anslutningsspecifikation-ID för Azure File Storage: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en Azure File Storage-anslutning med API:t för Flow Service och fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig hur du [utforskar ett molnlagringsutrymme från tredje part med API:t](../../explore/cloud-storage.md)för Flow Service.
