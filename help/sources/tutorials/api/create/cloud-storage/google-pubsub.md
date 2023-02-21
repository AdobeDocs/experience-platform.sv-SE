---
title: Skapa en Google PubSub Source-anslutning med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till ett Google PubSub-konto med API:t för Flow Service.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Skapa en [!DNL Google PubSub] Källanslutning med API:t för Flow Service

I den här självstudiekursen får du hjälp med att koppla samman [!DNL Google PubSub] (nedan kallad[!DNL PubSub]&quot;) till Experience Platform med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL PubSub] till plattform med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att ansluta till [!DNL PubSub]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `projectId` | Det projekt-ID som krävs för autentisering [!DNL PubSub]. |
| `credentials` | Autentiseringsuppgifter eller nyckel som krävs för autentisering [!DNL PubSub]. |
| `topicId` | ID för [!DNL PubSub] en resurs som representerar en feed med meddelanden. Du måste ange ett ämne-ID om du vill ge åtkomst till en viss dataström i ditt [!DNL Google PubSub] källa. |
| `subscriptionId` | Ditt ID [!DNL PubSub] prenumeration. I [!DNL PubSub]kan du få meddelanden genom att prenumerera på det ämne som meddelanden har publicerats i. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer som är kopplade till att skapa bas- och källmålanslutningarna. The [!DNL PubSub] anslutningsspecifikation-ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Mer information om dessa värden finns i [[!DNL PubSub] autentisering](https://cloud.google.com/pubsub/docs/authentication) -dokument. Om du vill använda tjänstkontobaserad autentisering läser du följande [[!DNL PubSub] guide om hur du skapar tjänstkonton](https://cloud.google.com/docs/authentication/production#create_service_account) för steg om hur du genererar dina autentiseringsuppgifter.

>[!TIP]
>
>Om du använder kontobaserad autentisering för tjänster måste du se till att du har beviljat tillräcklig användaråtkomst till ditt tjänstkonto och att det inte finns några extra tomrum i JSON när du kopierar och klistrar in dina autentiseringsuppgifter.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

Det första steget i att skapa en källanslutning är att autentisera [!DNL PubSub] och generera ett anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL PubSub] autentiseringsuppgifter som en del av parametrarna för begäran.

Under det här steget kan du definiera de data som ditt konto har åtkomst till genom att ange ett ämne-ID. Det är bara prenumerationer som är kopplade till detta ämne-ID som är tillgängliga.

>[!NOTE]
>
>Principal (roller) som tilldelats ett underordnat projekt ärvs i alla ämnen och prenumerationer som skapas i ett [!DNL PubSub] projekt. Om du vill lägga till ett huvudämne (roll) för att få tillgång till ett visst ämne, måste det huvudämnet (rollen) också läggas till i ämnets motsvarande prenumeration. Mer information finns i [[!DNL PubSub] dokumentation om åtkomstkontroll](https://cloud.google.com/pubsub/docs/access-control).

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Google PubSub authentication credentials",
          "params": {
              "projectId": "acme-project",
              "credentials": "{CREDENTIALS}",
              "topicId": "acmeProjectAPI",
              "subscriptionId": "acme-project-api-new"
          }
      },
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.projectId` | Det projekt-ID som krävs för autentisering [!DNL PubSub]. |
| `auth.params.credentials` | Autentiseringsuppgifter eller nyckel som krävs för autentisering [!DNL PubSub]. |
| `auth.params.topicId` | Ämnes-ID för din [!DNL PubSub] källa som du vill ge åtkomst till. |
| `auth.params.subscriptionId` | ID:t för prenumerationen mot din [!DNL PubSub] ämne. |
| `connectionSpec.id` | The [!DNL PubSub] anslutningsspec-ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta grundläggande anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Skapa en källanslutning {#source}

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
      "name": "Google PubSub source connection",
      "description": "A source connection for Google PubSub",
      "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "topicId": "acme-project",
          "subscriptionId": "{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ange för att inkludera mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för din [!DNL PubSub] källa som skapades i föregående steg. |
| `connectionSpec.id` | ID för fast anslutningsspecifikation för [!DNL PubSub]. Detta ID är: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Formatet på [!DNL PubSub] data som du vill importera. För närvarande är det enda dataformatet som stöds `json`. |
| `params.topicId` | Ditt namn eller ID [!DNL PubSub] ämne. I [!DNL PubSub]är ett ämne en namngiven resurs som representerar en feed med meddelanden. |
| `params.subscriptionId` | Det prenumerations-ID som motsvarar ett visst ämne. I [!DNL PubSub]kan du läsa meddelanden från ett ämne. En eller flera prenumerationer kan tilldelas till ett enskilt ämne. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudiekurs för att skapa ett dataflöde.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL PubSub] källanslutning med [!DNL Flow Service] API. Du kan använda det här källanslutnings-ID:t i nästa självstudiekurs för att [skapa ett direktuppspelat dataflöde med [!DNL Flow Service] API](../../collect/streaming.md).
