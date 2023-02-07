---
title: Skapa en Oracle Eloqua-basanslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Eloqua med API:t för Flow Service.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Skapa en [!DNL Oracle Eloqua] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Oracle Eloqua] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md): Plattformen gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Plattformen innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Oracle Eloqua] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Oracle Eloqua]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `endpoint` | Slutpunkten för [!DNL Oracle Eloqua]. |
| `username` | Användarnamnet för [!DNL Oracle Eloqua] konto. Användarnamnet måste vara formaterat som `siteName + \\ + username`, där `siteName` är företagsnamnet som du använde för att logga in på [!DNL Oracle Eloqua] och `username` är ditt användarnamn. Användarnamnet för inloggning kan till exempel vara: `adobe\\emily`. |
| `password` | Lösenordet som motsvarar [!DNL Oracle Eloqua] användarnamn. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Värdet för anslutningsspecifikationens ID [!DNL Oracle Eloqua] källan är fast som: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Mer information om autentiseringsuppgifter för [!DNL Oracle Eloqua], se [[!DNL Oracle Eloqua] guide om autentisering](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Oracle Eloqua] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Oracle Eloqua]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Namnet på [!DNL Oracle Eloqua] basanslutning. Du bör ange ett beskrivande namn eftersom du kan använda det här värdet för att leta upp din basanslutning. |
| `description` | (Valfritt) En egenskap som du kan ta med för att ge ytterligare information om din basanslutning. |
| `auth.specName` | Autentiseringstypen som används för anslutningen. |
| `auth.params.endpoint` | Slutpunkten för [!DNL Oracle Eloqua] server. |
| `auth.params.username` | Den sammanfogade autentiseringsuppgiften som innehåller platsnamnet och användarnamnet som motsvarar din [!DNL Oracle Eloqua] konto. |
| `auth.params.password` | Lösenordet som motsvarar [!DNL Oracle Eloqua] konto. |
| `connectionSpec.id` | Värdet för anslutningsspecifikationens ID [!DNL Oracle Eloqua] källan är fast som: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Oracle Eloqua] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att ta fram data för automatiserad marknadsföring till plattformen med [!DNL Flow Service] API](../../collect/marketing-automation.md)
