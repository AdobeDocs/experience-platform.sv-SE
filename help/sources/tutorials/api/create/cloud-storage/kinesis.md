---
keywords: Experience Platform;hem;populära ämnen;Kinesis;kines;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Skapa en Amazon Kinesis-källanslutning med API:t för flödestjänsten
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till en Amazon Kinesis-källa med API:t för Flow Service.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: fe7c498542cc0dd5f53bc3a434ab34d62e449048
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# Skapa en [!DNL Amazon Kinesis]-källanslutning med API:t för Flow Service

I den här självstudiekursen får du hjälp med att ansluta [!DNL Amazon Kinesis] (nedan kallat &quot;[!DNL Kinesis]&quot;) till Experience Platform med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta [!DNL Kinesis] till plattformen med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till ditt [!DNL Amazon Kinesis]-konto måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | Åtkomstnyckel-ID:t är hälften av det åtkomstnyckelpar som används för att autentisera ditt [!DNL Kinesis]-konto för plattformen. |
| `secretKey` | Den hemliga åtkomstnyckeln är den andra halvan av det åtkomstnyckelpar som används för att autentisera ditt [!DNL Kinesis]-konto för plattformen. |
| `region` | Regionen för ditt [!DNL Kinesis]-konto. Mer information om regioner finns i guiden [om hur du lägger till IP-adresser i tillåtelselista](../../../../ip-address-allow-list.md). |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Kinesis] är: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Mer information om [!DNL Kinesis]-åtkomstnycklar och hur du genererar dem finns i den här [[!DNL AWS] handboken om hur du hanterar åtkomstnycklar för IAM-användare](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

Det första steget i att skapa en källanslutning är att autentisera källan för [!DNL Kinesis] och generera ett grundläggande anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Kinesis] som en del av parametrarna för begäran.

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
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Svar**

Ett lyckat svar returnerar information om den nyskapade basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Skapa en källanslutning {#source}

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från. En källanslutning består av information som datakälla, dataformat och det källanslutnings-ID som behövs för att skapa ett dataflöde. En källanslutningsinstans är specifik för en klientorganisation och IMS-organisation.

Om du vill skapa en källanslutning skickar du en POST till `/sourceConnections`-slutpunkten för API:t [!DNL Flow Service].

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `baseConnectionId` | Det grundläggande anslutnings-ID för din [!DNL Kinesis]-källa som genererades i föregående steg. |
| `connectionSpec.id` | Det fasta anslutningsspecifikations-ID:t för [!DNL Kinesis]. Detta ID är: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Formatet på de [!DNL Kinesis]-data som du vill importera. För närvarande är det enda dataformat som stöds `json`. |
| `params.stream` | Namnet på dataströmmen som posterna ska hämtas från. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |
| `params.reset` | Den här parametern definierar hur data läses. Använd `latest` för att börja läsa från de senaste data och använd `earliest` för att börja läsa från de första tillgängliga data i strömmen. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudiekurs för att skapa ett dataflöde.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Kinesis]-källanslutning med hjälp av API:t [!DNL Flow Service]. Du kan använda det här källanslutnings-ID:t i nästa självstudie för att [skapa ett direktuppspelat dataflöde med hjälp av [!DNL Flow Service] API](../../collect/streaming.md).
