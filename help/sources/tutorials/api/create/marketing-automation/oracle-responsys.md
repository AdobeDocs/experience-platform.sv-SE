---
keywords: Experience Platform;hem;populära ämnen;oracle;
title: (Beta) Skapa en Oraclena svarsbasanslutning med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Responssys med API:t för Flow Service.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# (Beta) Skapa en [!DNL Oracle Responsys] basanslutning med [!DNL Flow Service] API

>[!NOTE]
>
>The [!DNL Oracle Responsys] källan är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Oracle Responsys] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md): Plattformen tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Plattformen innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Oracle Responsys] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Oracle Responsys]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `endpoint` | Slutpunkts-URL för REST-autentisering för din [!DNL Oracle Responsys] -instans. |
| `clientId` | Klient-ID för din [!DNL Oracle Responsys] -instans. |
| `clientSecret` | Klienthemligheten för din [!DNL Oracle Responsys] -instans. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Värdet för anslutningsspecifikationens ID [!DNL Oracle Responsys] källan är fast som: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Mer information om autentiseringsuppgifter för [!DNL Oracle Responsys], se [[!DNL Oracle Responsys] guide om autentisering](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Oracle Responsys] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Oracle Responsys]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Namnet på [!DNL Oracle Responsys] basanslutning. Du bör ange ett beskrivande namn eftersom du kan använda det här värdet för att leta upp din basanslutning. |
| `description` | (Valfritt) En egenskap som du kan ta med för att ge ytterligare information om din basanslutning. |
| `auth.specName` | Autentiseringstypen som används för anslutningen. |
| `auth.params.endpoint` | Slutpunkts-URL för REST-autentisering för din [!DNL Oracle Responsys] server. |
| `auth.params.clientId` | Klient-ID för din [!DNL Oracle Responsys] -instans. |
| `auth.params.clientSecret` | Klienthemligheten för din [!DNL Oracle Responsys] -instans. |
| `connectionSpec.id` | Värdet för anslutningsspecifikationens ID [!DNL Oracle Responsys] källan är fast som: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Oracle Responsys] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att ta fram data för automatiserad marknadsföring till plattformen med [!DNL Flow Service] API](../../collect/marketing-automation.md)
