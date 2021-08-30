---
keywords: Experience Platform;hem;populära ämnen;Google PubSub;google pubsub
solution: Experience Platform
title: Skapa en Google PubSub Source-anslutning med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till ett Google PubSub-konto med API:t för Flow Service.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# Skapa en [!DNL Google PubSub]-källanslutning med API:t för Flow Service

>[!NOTE]
>
>[!DNL Google PubSub]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

I den här självstudiekursen får du hjälp med att ansluta [!DNL Google PubSub] (nedan kallat &quot;[!DNL PubSub]&quot;) till Experience Platform med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta [!DNL PubSub] till plattformen med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL PubSub] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `projectId` | Det projekt-ID som krävs för att autentisera [!DNL PubSub]. |
| `credentials` | Autentiseringsuppgiften eller nyckeln som krävs för att autentisera [!DNL PubSub]. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer som är kopplade till att skapa bas- och källmålanslutningarna. Anslutningsspecifikations-ID för [!DNL PubSub] är: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Mer information om dessa värden finns i det här [[!DNL PubSub] autentiseringsdokumentet](https://cloud.google.com/pubsub/docs/authentication). Om du vill använda tjänstkontobaserad autentisering läser du den här [[!DNL PubSub] guiden om hur du skapar tjänstkonton](https://cloud.google.com/docs/authentication/production#create_service_account) för steg om hur du genererar dina autentiseringsuppgifter.

>[!TIP]
>
>Om du använder kontobaserad autentisering för tjänster måste du se till att du har beviljat tillräcklig användaråtkomst till ditt tjänstkonto och att det inte finns några extra tomrum i JSON när du kopierar och klistrar in dina autentiseringsuppgifter.

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

Det första steget i att skapa en källanslutning är att autentisera källan för [!DNL PubSub] och generera ett grundläggande anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL PubSub] som en del av parametrarna för begäran.

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
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
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
| `auth.params.projectId` | Det projekt-ID som krävs för att autentisera [!DNL PubSub]. |
| `auth.params.credentials` | Autentiseringsuppgiften eller nyckeln som krävs för att autentisera [!DNL PubSub]. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta grundläggande anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Skapa en källanslutning {#source}

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
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ange för att inkludera mer information om din källanslutning. |
| `baseConnectionId` | Det grundläggande anslutnings-ID för din [!DNL PubSub]-källa som genererades i föregående steg. |
| `connectionSpec.id` | Det fasta anslutningsspecifikations-ID:t för [!DNL PubSub]. Detta ID är: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Formatet på de [!DNL PubSub]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.topicId` | Ämne-ID definierar den specifika namngivna resursen som meddelanden skickas av utgivare |
| `params.subscriptionId` | Prenumerations-ID:t definierar den specifika namngivna resursen som representerar flödet av meddelanden från ett specifikt ämne som ska levereras till prenumerationsprogrammet. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudiekurs för att skapa ett dataflöde.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL PubSub]-källanslutning med hjälp av API:t [!DNL Flow Service]. Du kan använda det här källanslutnings-ID:t i nästa självstudie för att [skapa ett direktuppspelat dataflöde med hjälp av [!DNL Flow Service] API](../../collect/streaming.md).
