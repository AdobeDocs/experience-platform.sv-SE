---
title: Skapa en Google PubSub Source-anslutning med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till ett Google PubSub-konto med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 0%

---

# Skapa en [!DNL Google PubSub] Source-anslutning med API:t för flödestjänsten

>[!IMPORTANT]
>
>Källan [!DNL Google PubSub] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

I den här självstudiekursen får du hjälp med att ansluta [!DNL Google PubSub] (kallas nedan [!DNL PubSub]) till Experience Platform med [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL PubSub] till Experience Platform med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Du måste ange värden för anslutningsegenskaperna som beskrivs nedan för att kunna ansluta ditt [!DNL PubSub]-konto till [!DNL Flow Service]. Mer information om autentisering och nödvändiga inställningar finns i [[!DNL PubSub source] översikten](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB Projektbaserad autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `projectId` | Det projekt-ID som krävs för att autentisera [!DNL PubSub]. |
| `credentials` | Autentiseringsuppgifterna som krävs för att autentisera [!DNL PubSub]. Du måste se till att du skickar den fullständiga JSON-filen när du har tagit bort blanktecknen från inloggningsuppgifterna. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer som är kopplade till att skapa bas- och källmålanslutningarna. Anslutningsspecifikations-ID [!DNL PubSub] är: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Ämnesbaserad och prenumerationsbaserad autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `credentials` | Autentiseringsuppgifterna som krävs för att autentisera [!DNL PubSub]. Du måste se till att du skickar den fullständiga JSON-filen när du har tagit bort blanktecknen från inloggningsuppgifterna. |
| `topicName` | Namnet på resursen som representerar en feed med meddelanden. Du måste ange ett ämnesnamn om du vill ge åtkomst till en viss dataström i [!DNL PubSub]-källan. Ämnesnamnets format är: `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | Namnet på din [!DNL PubSub]-prenumeration. I [!DNL PubSub] kan du med prenumerationer ta emot meddelanden genom att prenumerera på det ämne som meddelanden har publicerats i. **Obs!**: En enstaka [!DNL PubSub]-prenumeration kan bara användas för ett dataflöde. Om du vill kunna skapa flera dataflöden måste du ha flera prenumerationer. Prenumerationsnamnformatet är: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer som är kopplade till att skapa bas- och källmålanslutningarna. Anslutningsspecifikations-ID [!DNL PubSub] är: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

Mer information om dessa värden finns i det här [[!DNL PubSub] autentiseringsdokumentet](https://cloud.google.com/pubsub/docs/authentication). Om du vill använda tjänstkontobaserad autentisering läser du i den här [[!DNL PubSub] handboken om hur du skapar tjänstkonton](https://cloud.google.com/docs/authentication/production#create_service_account) för steg om hur du genererar dina autentiseringsuppgifter.

>[!TIP]
>
>Om du använder kontobaserad autentisering för tjänster måste du se till att du har beviljat tillräcklig användaråtkomst till ditt tjänstkonto och att det inte finns några extra tomrum i JSON när du kopierar och klistrar in dina autentiseringsuppgifter.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Google PubSub]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Det första steget i att skapa en källanslutning är att autentisera [!DNL PubSub]-källan och generera ett grundläggande anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL PubSub]-autentiseringsuppgifter som en del av parametrarna för begäran.

Med [!DNL PubSub]-källan kan du ange vilken typ av åtkomst du vill tillåta under autentiseringen. Du kan konfigurera ditt konto så att det har rotåtkomst eller begränsa åtkomsten till ett visst [!DNL PubSub]-ämne och en viss prenumeration.

>[!NOTE]
>
>Principal (roller) som tilldelats ett [!DNL PubSub]-projekt ärvs i alla ämnen och prenumerationer som skapas i ett [!DNL PubSub]-projekt. Om du vill att ett huvudämne (en roll) ska ha tillgång till ett visst ämne, måste det huvudämnet (rollen) också läggas till i ämnets motsvarande prenumeration. Mer information finns i [[!DNL PubSub] dokumentationen om åtkomstkontroll](<https://cloud.google.com/pubsub/docs/access-control>).

**API-format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Projektbaserad autentisering]

Om du vill skapa en basanslutning med projektbaserad autentisering gör du en POST-begäran till `/connections`-slutpunkten och anger `projectId` och `credentials` i begärandetexten.

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
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
| `connectionSpec.id` | Anslutningens spec-ID [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

++++

+++svar

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta grundläggande anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB Ämnesbaserad och prenumerationsbaserad autentisering]

Om du vill skapa en basanslutning med ämne- och prenumerationsbaserad autentisering gör du en POST-begäran till `/connections`-slutpunkten och anger `credentials`, `topicName` och `subscriptionName` i begärandetexten.

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
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
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
| `auth.params.credentials` | Autentiseringsuppgiften eller nyckeln som krävs för att autentisera [!DNL PubSub]. |
| `auth.params.topicName` | Projekt-ID och ämne-ID-par för källan [!DNL PubSub] som du vill ge åtkomst till. |
| `auth.params.subscriptionName` | Projekt-ID och prenumerations-ID-par för källan [!DNL PubSub] som du vill ge åtkomst till. |
| `connectionSpec.id` | Anslutningens spec-ID [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

+++

+++svar

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta grundläggande anslutnings-ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## Skapa en källanslutning {#source}

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
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ange för att inkludera mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för källan [!DNL PubSub] som skapades i föregående steg. |
| `connectionSpec.id` | Det fasta anslutningsspecifikations-ID:t för [!DNL PubSub]. Detta ID är: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Formatet på de [!DNL PubSub]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.topicName` | Namnet på ditt [!DNL PubSub]-ämne. I [!DNL PubSub] är ett ämne en namngiven resurs som representerar en feed med meddelanden. |
| `params.subscriptionName` | Prenumerationsnamnet som motsvarar ett visst ämne. I [!DNL PubSub] kan du använda prenumerationer för att läsa meddelanden från ett ämne. En eller flera prenumerationer kan tilldelas till ett enskilt ämne. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudie för att skapa ett dataflöde.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>När du har skapat eller uppdaterat ett dataflöde för direktuppspelning krävs en kort 5-minuters paus i datainmatningen för att förhindra eventuella fall av dataförlust eller dataförlust.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL PubSub]-källanslutning med API:t [!DNL Flow Service]. Du kan använda det här källanslutnings-ID:t i nästa självstudie för att [skapa ett direktuppspelat dataflöde med  [!DNL Flow Service] API](../../collect/streaming.md).
