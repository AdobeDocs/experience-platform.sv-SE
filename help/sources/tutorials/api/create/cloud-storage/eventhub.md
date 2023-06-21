---
title: Skapa en källanslutning för Azure Event Hubs med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till ett Azure Event Hubs-konto med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b76bc6ddb0d49bbd089627c8df8b31703d0e50b1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Skapa en [!DNL Azure Event Hubs] källanslutning med [!DNL Flow Service] API

>[!IMPORTANT]
>
>The [!DNL Azure Event Hubs] Källan är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

I den här självstudiekursen får du hjälp med att koppla samman [!DNL Azure Event Hubs] (nedan kallad[!DNL Event Hubs]&quot;) till Experience Platform med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
- [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL Event Hubs] till plattform med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att få kontakt med [!DNL Event Hubs] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `sasKey` | Primärnyckeln för [!DNL Event Hubs] namnutrymme. The `sasPolicy` som `sasKey` motsvarar måste ha `manage` rättigheter som konfigurerats för [!DNL Event Hubs] lista som ska fyllas i. |
| `namespace` | Namnutrymmet för [!DNL Event Hubs] du försöker komma åt. An [!DNL Event Hubs] namespace innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. The [!DNL Event Hubs] anslutningsspecifikation-ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Mer information om dessa värden finns i [det här händelsehubbsdokumentet](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

Det första steget i att skapa en källanslutning är att autentisera [!DNL Event Hubs] och generera ett anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Event Hubs] autentiseringsuppgifter som en del av parametrarna för begäran.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.namespace` | Namnutrymmet för [!DNL Event Hubs] du försöker komma åt. |
| `connectionSpec.id` | The [!DNL Event Hubs] anslutningsspecifikation-ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Skapa en källanslutning

>[!TIP]
>
>An [!DNL Event Hubs] konsumentgrupp kan bara användas för ett enda flöde vid en given tidpunkt.

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från. En källanslutning består av information som datakälla, dataformat och ett källanslutnings-ID som behövs för att skapa ett dataflöde. En källanslutningsinstans är specifik för en klientorganisation och organisation.

Om du vill skapa en källanslutning skickar du en POST till `/sourceConnections` slutpunkt för [!DNL Flow Service] API.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `baseConnectionId` | Anslutnings-ID för din [!DNL Event Hubs] källa som skapades i föregående steg. |
| `connectionSpec.id` | ID för fast anslutningsspecifikation för [!DNL Event Hubs]. Detta ID är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Formatet på [!DNL Event Hubs] data som du vill importera. För närvarande är det enda dataformatet som stöds `json`. |
| `params.eventHubName` | Namnet på [!DNL Event Hubs] källa. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |
| `params.reset` | Den här parametern definierar hur data läses. Använd `latest` för att börja läsa från de senaste data och använda `earliest` för att börja läsa från de första tillgängliga data i strömmen. Den här parametern är valfri och används som standard `earliest` om ej tillhandahållet. |
| `params.consumerGroup` | Publicerings- eller prenumerationsmekanismen som ska användas för [!DNL Event Hubs]. Den här parametern är valfri och används som standard `$Default` om ej tillhandahållet. Se detta [[!DNL Event Hubs] guide om händelsekonsumenter](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) för mer information. **Anteckning**: An [!DNL Event Hubs] konsumentgrupp kan bara användas för ett enda flöde vid en given tidpunkt. |

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Event Hubs] källanslutning med [!DNL Flow Service] API. Du kan använda det här källanslutnings-ID:t i nästa självstudiekurs för att [skapa ett direktuppspelat dataflöde med [!DNL Flow Service] API](../../collect/streaming.md).
