---
title: Skapa en Azure Event Hubs Source Connection med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till ett Azure Event Hubs-konto med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 0%

---

# Skapa en [!DNL Azure Event Hubs]-källanslutning med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>Källan [!DNL Azure Event Hubs] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

I den här självstudiekursen får du lära dig hur du ansluter [!DNL Azure Event Hubs] (kallas nedan [!DNL Event Hubs]) till Experience Platform med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
- [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL Event Hubs] till Experience Platform med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till ditt [!DNL Event Hubs]-konto måste du ange värden för följande anslutningsegenskaper:

>[!BEGINTABS]

>[!TAB Standardautentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `sasKey` | Primärnyckeln för namnområdet [!DNL Event Hubs]. `sasPolicy` som `sasKey` motsvarar måste ha `manage` rättigheter konfigurerade för att [!DNL Event Hubs]-listan ska kunna fyllas i. |
| `namespace` | Namnområdet för [!DNL Event Hub] som du använder. Ett [!DNL Event Hub]-namnområde innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID [!DNL Event Hubs] är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB SAS-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `sasKey` | Primärnyckeln för namnområdet [!DNL Event Hubs]. `sasPolicy` som `sasKey` motsvarar måste ha `manage` rättigheter konfigurerade för att [!DNL Event Hubs]-listan ska kunna fyllas i. |
| `namespace` | Namnområdet för [!DNL Event Hub] som du använder. Ett [!DNL Event Hub]-namnområde innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| `eventHubName` | Fyll i ditt [!DNL Azure Event Hub]-namn. Läs [Microsoft-dokumentationen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) om du vill ha mer information om [!DNL Event Hub]-namn. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID [!DNL Event Hubs] är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Mer information om SAS-autentisering (Shared Access Signatures) för [!DNL Event Hubs] finns i [[!DNL Azure] handboken om användning av SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Händelsehubben Azure Active Directory-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `tenantId` | Klient-ID som du vill begära behörighet från. Ditt klient-ID kan formateras som ett GUID eller som ett eget namn. **Obs!** Klient-ID kallas för &quot;katalog-ID&quot; i gränssnittet [!DNL Microsoft Azure]. |
| `clientId` | Program-ID som tilldelats din app. Du kan hämta detta ID från portalen [!DNL Microsoft Entra ID] där du registrerade din [!DNL Azure Active Directory]. |
| `clientSecretValue` | Klienthemligheten som används tillsammans med klient-ID för att autentisera din app. Du kan hämta din klienthemlighet från portalen [!DNL Microsoft Entra ID] där du registrerade din [!DNL Azure Active Directory]. |
| `namespace` | Namnområdet för [!DNL Event Hub] som du använder. Ett [!DNL Event Hub]-namnområde innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |

Mer information om [!DNL Azure Active Directory] finns i [Azure-guiden om hur du använder Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Händelsehubben har omfattat Azure Active Directory Auth]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `tenantId` | Klient-ID som du vill begära behörighet från. Ditt klient-ID kan formateras som ett GUID eller som ett eget namn. **Obs!** Klient-ID kallas för &quot;katalog-ID&quot; i gränssnittet [!DNL Microsoft Azure]. |
| `clientId` | Program-ID som tilldelats din app. Du kan hämta detta ID från portalen [!DNL Microsoft Entra ID] där du registrerade din [!DNL Azure Active Directory]. |
| `clientSecretValue` | Klienthemligheten som används tillsammans med klient-ID för att autentisera din app. Du kan hämta din klienthemlighet från portalen [!DNL Microsoft Entra ID] där du registrerade din [!DNL Azure Active Directory]. |
| `namespace` | Namnområdet för [!DNL Event Hub] som du använder. Ett [!DNL Event Hub]-namnområde innehåller en unik omfångsbehållare där du kan skapa en eller flera [!DNL Event Hubs]. |
| `eventHubName` | Fyll i ditt [!DNL Azure Event Hub]-namn. Läs [Microsoft-dokumentationen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) om du vill ha mer information om [!DNL Event Hub]-namn. |

>[!ENDTABS]

Mer information om dessa värden finns i [det här händelsehubbsdokumentet](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Event Hubs]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Det första steget i att skapa en källanslutning är att autentisera [!DNL Event Hubs]-källan och generera ett grundläggande anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Event Hubs]-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Standardautentisering]

Om du vill skapa ett konto med standardautentisering skickar du en POST-begäran till `/connections`-slutpunkten och anger värden för `sasKeyName`, `sasKey` och `namespace`.

+++Begäran

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
| `auth.params.namespace` | Namnområdet för [!DNL Event Hubs] som du använder. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Event Hubs] är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++svar

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB SAS-autentisering]

Om du vill skapa ett konto med SAS-autentisering gör du en POST-begäran till `/connections`-slutpunkten och anger värden för `sasKeyName`, `sasKey`, `namespace` och `eventHubName`.

+++Begäran

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
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
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
| `auth.params.namespace` | Namnområdet för [!DNL Event Hubs] som du använder. |
| `params.eventHubName` | Namnet på [!DNL Event Hubs]-källan. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Event Hubs] är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++svar

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Händelsehubben Azure Active Directory-autentisering]

Om du vill skapa ett konto med Azure Active Directory Auth gör du en POST-begäran till `/connections`-slutpunkten samtidigt som du anger värden för `tenantId`, `clientId`, `clientSecretValue` och `namespace`.

+++Begäran

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
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
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
| `auth.params.tenantId` | Klient-ID för ditt program. **Obs!** Klient-ID kallas för &quot;katalog-ID&quot; i gränssnittet [!DNL Microsoft Azure]. |
| `auth.params.clientId` | Klient-ID för din organisation. |
| `auth.params.clientSecretValue` | Klientens hemliga värde för din organisation. |
| `auth.params.namespace` | Namnområdet för [!DNL Event Hubs] som du använder. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Event Hubs] är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++svar

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Händelsehubben har omfattat Azure Active Directory Auth]

Om du vill skapa ett konto med Azure Active Directory Auth gör du en POST-begäran till `/connections`-slutpunkten samtidigt som du anger värden för `tenantId`, `clientId`, `clientSecretValue`, `namespace` och `eventHubName`.

+++Begäran

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
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
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
| `auth.params.tenantId` | Klient-ID för ditt program. **Obs!** Klient-ID kallas för &quot;katalog-ID&quot; i gränssnittet [!DNL Microsoft Azure]. |
| `auth.params.clientId` | Klient-ID för din organisation. |
| `auth.params.clientSecretValue` | Klientens hemliga värde för din organisation. |
| `auth.params.namespace` | Namnområdet för [!DNL Event Hubs] som du använder. |
| `auth.params.eventHubName` | Namnet på [!DNL Event Hubs]-källan. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Event Hubs] är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++svar

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## Skapa en källanslutning

>[!TIP]
>
>En [!DNL Event Hubs]-konsumentgrupp kan bara användas för ett enda flöde vid en given tidpunkt.

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från. En källanslutning består av information som datakälla, dataformat och ett källanslutnings-ID som behövs för att skapa ett dataflöde. En källanslutningsinstans är specifik för en klientorganisation och organisation.

Om du vill skapa en källanslutning skickar du en POST-begäran till `/sourceConnections`-slutpunkten för [!DNL Flow Service] API:t.

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
          "eventHubName": "{EVENT_HUB_NAME}",
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
| `baseConnectionId` | Anslutnings-ID för källan [!DNL Event Hubs] som skapades i föregående steg. |
| `connectionSpec.id` | Det fasta anslutningsspecifikations-ID:t för [!DNL Event Hubs]. Detta ID är: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Formatet på de [!DNL Event Hubs]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.eventHubName` | Namnet på [!DNL Event Hubs]-källan. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |
| `params.reset` | Den här parametern definierar hur data läses. Använd `latest` för att börja läsa från de senaste data och använd `earliest` för att börja läsa från de första tillgängliga data i strömmen. Den här parametern är valfri och standardvärdet är `earliest` om den inte anges. |
| `params.consumerGroup` | Publicerings- eller prenumerationsmekanismen som ska användas för [!DNL Event Hubs]. Den här parametern är valfri och standardvärdet är `$Default` om den inte anges. Mer information finns i [[!DNL Event Hubs] handboken om händelsekonsumenter](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers). **Obs!**: En [!DNL Event Hubs]-konsumentgrupp kan bara användas för ett enda flöde vid en given tidpunkt. |

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Event Hubs]-källanslutning med API:t [!DNL Flow Service]. Du kan använda det här källanslutnings-ID:t i nästa självstudie för att [skapa ett direktuppspelat dataflöde med  [!DNL Flow Service] API](../../collect/streaming.md).
