---
keywords: Experience Platform;home;populära topics;event hub;Azure event hub;Event hub
solution: Experience Platform
title: Skapa en källanslutning för Azure Event Hubs med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till ett Azure Event Hubs-konto med API:t för Flow Service.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---


# Skapa en [!DNL Azure Event Hubs]-källanslutning med hjälp av API:t [!DNL Flow Service]

I den här självstudiekursen får du hjälp med att ansluta [!DNL Azure Event Hubs] (nedan kallat &quot;[!DNL Event Hubs]&quot;) till Experience Platform med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
- [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta [!DNL Event Hubs] till plattformen med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till ditt [!DNL Event Hubs]-konto måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `sasKey` | Den genererade signaturen för delad åtkomst. |
| `namespace` | Namnområdet för [!DNL Event Hubs] som du försöker komma åt. Ett [!DNL Event Hubs]-namnutrymme ger en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Event Hubs] är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Mer information om dessa värden finns i [det här händelsehubbsdokumentet](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

Det första steget i att skapa en källanslutning är att autentisera källan för [!DNL Event Hubs] och generera ett grundläggande anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Event Hubs] som en del av parametrarna för begäran.

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
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
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
| `auth.params.namespace` | Namnområdet för [!DNL Event Hubs] som du försöker komma åt. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Event Hubs] är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Svar**

Ett lyckat svar returnerar information om den nyskapade basanslutningen, inklusive dess unika identifierare (`id`). Detta anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Skapa en källanslutning

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från. En källanslutning består av information som datakälla, dataformat och ett källanslutnings-ID som behövs för att skapa ett dataflöde. En källanslutningsinstans är specifik för en klientorganisation och IMS-organisation.

Om du vill skapa en källanslutning skickar du en POST till `/sourceConnections`-slutpunkten för API:t [!DNL Flow Service].

**API-format**

```http
POST /sourceConnections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_Org}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Azure Event Hubs source connection",
        "description": "A source connection for Azure Event Hubs",
        "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ange för att inkludera mer information om din källanslutning. |
| `baseConnectionId` | Anslutnings-ID för din [!DNL Event Hubs]-källa som genererades i föregående steg. |
| `connectionSpec.id` | Det fasta anslutningsspecifikations-ID:t för [!DNL Event Hubs]. Detta ID är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Formatet på de [!DNL Event Hubs]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.eventHubName` | Namnet på din [!DNL Event Hubs]-källa. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |
| `params.reset` | Den här parametern definierar hur data läses. Använd `latest` för att börja läsa från de senaste data och använd `earliest` för att börja läsa från de första tillgängliga data i strömmen. Den här parametern är valfri och standardvärdet är `earliest` om den inte anges. |
| `params.consumerGroup` | Publicerings- eller prenumerationsmekanismen som ska användas för [!DNL Event Hubs]. Den här parametern är valfri och standardvärdet är `$Default` om den inte anges. Mer information finns i den här [[!DNL Event Hubs] handboken om händelsekonsumenter](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers). |

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Event Hubs]-källanslutning med hjälp av API:t [!DNL Flow Service]. Du kan använda det här källanslutnings-ID:t i nästa självstudie för att [skapa ett direktuppspelat dataflöde med hjälp av [!DNL Flow Service] API](../../collect/streaming.md).
