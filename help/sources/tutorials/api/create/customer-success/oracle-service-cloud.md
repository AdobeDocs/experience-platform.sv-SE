---
keywords: Experience Platform;hem;populära ämnen;Oracle Service Cloud;oracle service cloud
title: Skapa en Oracle Service Cloud Source Connection med API:t för flödestjänst
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Service Cloud med API:t för flödestjänst.
exl-id: 00c0bc9c-a740-4bab-a882-2cfed8abe758
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Skapa en Oracle Service Cloud-källanslutning med hjälp av API:t [!DNL Flow Service]

>[!WARNING]
>
>[!DNL Oracle Service Cloud]-källan kommer att bli inaktuell i slutet av maj 2025.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för Oracle Service Cloud med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till Oracle Service Cloud med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till Oracle Service Cloud måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Värd-URL:en för din Oracle Service Cloud-instans. |
| `username` | Användarnamnet för ditt användarkonto för Oracle Service Cloud. |
| `password` | Lösenordet för ditt Oracle Service Cloud-konto. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för Oracle Service Cloud är: `ba5126ec-c9ac-11eb-b8bc-0242ac130003`. |

Mer information om hur du autentiserar ditt Oracle Service Cloud-konto finns i [[!DNL Oracle] handboken om autentisering](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till slutpunkten `/connections` samtidigt som du anger autentiseringsuppgifterna för Oracle Service Cloud som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för Oracle Service Cloud:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | Värd-URL:en för din Oracle Service Cloud-instans. |
| `auth.params.username` | Det användarnamn som är kopplat till ditt Oracle Service Cloud-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt Oracle Service Cloud-konto. |
| `connectionSpec.id` | Oraclets anslutningsspecifikation för Service Cloud: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att undersöka ditt CRM-system i nästa steg.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en Oracle Service Cloud-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att skicka kunddata till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/customer-success.md)
