---
title: Skapa en Amazon Kinesis Source-anslutning med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till en Amazon Kinesis-källa med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Skapa en [!DNL Amazon Kinesis]-källanslutning med API:t för Flow Service

>[!IMPORTANT]
>
>Källan [!DNL Amazon Kinesis] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

I den här självstudiekursen får du hjälp med att ansluta [!DNL Amazon Kinesis] (kallas nedan [!DNL Kinesis]) till Experience Platform med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL Kinesis] till Experience Platform med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till ditt [!DNL Amazon Kinesis]-konto måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | Åtkomstnyckel-ID:t är hälften av åtkomstnyckelparet som används för att autentisera ditt [!DNL Kinesis]-konto för Experience Platform. |
| `secretKey` | Den hemliga åtkomstnyckeln är den andra halvan av det åtkomstnyckelpar som används för att autentisera ditt [!DNL Kinesis]-konto för Experience Platform. |
| `region` | Regionen för ditt [!DNL Kinesis]-konto. Mer information om regioner finns i guiden om att [lägga till IP-adresser i tillåtelselista](../../../../ip-address-allow-list.md). |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID [!DNL Kinesis] är: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Mer information om [!DNL Kinesis]-åtkomstnycklar och hur du genererar dem finns i den här [[!DNL AWS] handboken om hur du hanterar åtkomstnycklar för IAM-användare](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

Det första steget i att skapa en källanslutning är att autentisera [!DNL Kinesis]-källan och generera ett grundläggande anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Kinesis]-autentiseringsuppgifter som en del av parametrarna för begäran.

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
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.accessKeyId` | Åtkomstnyckel-ID för ditt [!DNL Kinesis]-konto. |
| `auth.params.secretKey` | Den hemliga åtkomstnyckeln för ditt [!DNL Kinesis]-konto. |
| `auth.params.region` | Regionen för ditt [!DNL Kinesis]-konto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Skapa en källanslutning {#source}

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från. En källanslutning består av information som datakälla, dataformat och det källanslutnings-ID som behövs för att skapa ett dataflöde. En källanslutningsinstans är specifik för en klientorganisation och organisation.

Om du vill skapa en källanslutning skickar du en POST-begäran till `/sourceConnections`-slutpunkten för [!DNL Flow Service] API:t.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på källanslutningen. Kontrollera att namnet på källanslutningen är beskrivande, eftersom du kan använda det här för att söka efter information om källanslutningen. |
| `description` | Ett valfritt värde som du kan ange för att inkludera mer information om din källanslutning. |
| `baseConnectionId` | Basanslutnings-ID för källan [!DNL Kinesis] som skapades i föregående steg. |
| `connectionSpec.id` | Det fasta anslutningsspecifikations-ID:t för [!DNL Kinesis]. Detta ID är: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Formatet på de [!DNL Kinesis]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.stream` | Namnet på dataströmmen som posterna ska hämtas från. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |
| `params.reset` | Den här parametern definierar hur data läses. Använd `latest` för att börja läsa från de senaste data och använd `earliest` för att börja läsa från de första tillgängliga data i strömmen. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudie för att skapa ett dataflöde.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Kinesis]-källanslutning med API:t [!DNL Flow Service]. Du kan använda det här källanslutnings-ID:t i nästa självstudie för att [skapa ett direktuppspelat dataflöde med  [!DNL Flow Service] API](../../collect/streaming.md).
