---
keywords: Experience Platform;hem;populära ämnen;[!DNL Azure Table Storage];[!DNL Azure Table Storage];Azure table storage
solution: Experience Platform
title: Skapa en Azure Table Storage Base-anslutning med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Azure Table Storage till Adobe Experience Platform med API:t för Flow Service.
exl-id: 8ebd5d77-ed1f-47e1-8212-efb6c5e84ec1
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# Skapa en [!DNL Azure Table Storage]-basanslutning med hjälp av API:t [!DNL Flow Service]

>[!NOTE]
>
>[!DNL Azure Table Storage]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Azure Table Storage] med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Azure Table Storage] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Azure Table Storage] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som används för att ansluta till en [!DNL Azure Table Storage]-instans. Anslutningssträngsmönstret för [!DNL Azure Table Storage] är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikationens ID för [!DNL Azure Table Storage] är `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

Mer information om hur du hämtar en anslutningssträng finns i [det här [!DNL Azure Table Storage] dokumentet](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Azure Table Storage] som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Azure Table Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Table Storage connection",
        "description": "Azure Table Storage connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som används för att ansluta till en [!DNL Azure Table Storage]-instans. Anslutningssträngsmönstret för [!DNL Azure Table Storage] är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Azure Table Storage]: `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "82abddb3-d59a-436c-abdd-b3d59a436c21",
    "etag": "\"7d00fde3-0000-0200-0000-5e84d9430000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Azure Table Storage]-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig att [utforska databaser med API:t för Flow Service](../../explore/database-nosql.md).
