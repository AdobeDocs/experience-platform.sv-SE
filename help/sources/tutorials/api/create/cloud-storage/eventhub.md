---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Azure Event Hubs-koppling med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: fdffdd34d1ccb61d6c82fecc249ddeb501d79d0e
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---


# Skapa en Azure Event Hubs-koppling med API:t för Flow Service

>[!NOTE]
> Azure Event Hubs-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Experience Platform till ett Azure Event Hubs-konto.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
- [Sandlådor](../../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till ett Azure Event Hubs-konto med API:t för Flow Service.

### Samla in nödvändiga inloggningsuppgifter

För att Flow Service ska kunna ansluta till ditt Azure Event Hubs-konto måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `sasKey` | Den genererade signaturen för delad åtkomst. |
| `namespace` | Namnområdet för de händelsehubbar som du försöker komma åt. |
| `connectionSpec.id` | Anslutningsspecifikation-ID för Azure Event Hubs: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

Mer information om dessa värden finns i [det här händelsehubbsdokumentet](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör Flow Service, isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

- Innehållstyp: `application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per Azure Event Hubs-konto eftersom det kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Basic Authentication for Event Hubs",
            "params": {
                "sasKeyName": "sasKeyName",
                "sasKey": "sasKey",
                "namespace": "namespace"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `auth.params.sasKey` | Den genererade signaturen för delad åtkomst. |
| `namespace` | Namnområdet för de händelsehubbar som du försöker komma åt. |
| `connectionSpec.id` | Anslutningsspecifikation-ID för Azure Event Hubs: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att du ska kunna utforska dina molnlagringsdata i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en Azure Event Hubs-anslutning med API:er och ett unikt ID har hämtats som en del av svarstexten. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t](../../explore/cloud-storage.md)för Flow Service.