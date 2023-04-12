---
keywords: Experience Platform;hem;populära ämnen;Kinesis;kines;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Skapa en Amazon Kinesis-källanslutning med API:t för flödestjänsten
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till en Amazon Kinesis-källa med API:t för Flow Service.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Skapa en [!DNL Amazon Kinesis] källanslutning med API:t för Flow Service

I den här självstudiekursen får du hjälp med att koppla samman [!DNL Amazon Kinesis] (nedan kallad[!DNL Kinesis]&quot;) till Experience Platform med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL Kinesis] till plattform med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att få kontakt med [!DNL Amazon Kinesis] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | Åtkomstnyckel-ID:t är hälften av det åtkomstnyckelpar som används för att autentisera din [!DNL Kinesis] konto till plattform. |
| `secretKey` | Den hemliga åtkomstnyckeln är den andra halvan av det åtkomstnyckelpar som används för att autentisera din [!DNL Kinesis] konto till plattform. |
| `region` | Regionen för din [!DNL Kinesis] konto. Se guiden [lägga till IP-adresser i tillåtelselista](../../../../ip-address-allow-list.md) för mer information om regioner. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. The [!DNL Kinesis] anslutningsspecifikation-ID: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Mer information om [!DNL Kinesis] åtkomstnycklar och hur du genererar dem finns i [[!DNL AWS] guide för hantering av åtkomstnycklar för IAM-användare](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

Det första steget i att skapa en källanslutning är att autentisera [!DNL Kinesis] och generera ett anslutnings-ID. Med ett grundläggande anslutnings-ID kan du utforska och navigera bland filer inifrån källan och identifiera specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Kinesis] autentiseringsuppgifter som en del av parametrarna för begäran.

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
| `auth.params.accessKeyId` | Åtkomstnyckel-ID för din [!DNL Kinesis] konto. |
| `auth.params.secretKey` | Den hemliga åtkomstnyckeln för [!DNL Kinesis] konto. |
| `auth.params.region` | Regionen för din [!DNL Kinesis] konto. |
| `connectionSpec.id` | The [!DNL Kinesis] anslutningsspecifikation-ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

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

Om du vill skapa en källanslutning skickar du en POST till `/sourceConnections` slutpunkt för [!DNL Flow Service] API.

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
| `baseConnectionId` | Basanslutnings-ID för din [!DNL Kinesis] källa som skapades i föregående steg. |
| `connectionSpec.id` | ID för fast anslutningsspecifikation för [!DNL Kinesis]. Detta ID är: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Formatet på [!DNL Kinesis] data som du vill importera. För närvarande är det enda dataformatet som stöds `json`. |
| `params.stream` | Namnet på dataströmmen som posterna ska hämtas från. |
| `params.dataType` | Den här parametern definierar vilken typ av data som importeras. Datatyper som stöds är: `raw` och `xdm`. |
| `params.reset` | Den här parametern definierar hur data läses. Använd `latest` för att börja läsa från de senaste data och använda `earliest` för att börja läsa från de första tillgängliga data i strömmen. |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen. Detta ID krävs i nästa självstudiekurs för att skapa ett dataflöde.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Kinesis] källanslutning med [!DNL Flow Service] API. Du kan använda det här källanslutnings-ID:t i nästa självstudiekurs för att [skapa ett direktuppspelat dataflöde med [!DNL Flow Service] API](../../collect/streaming.md).
