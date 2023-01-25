---
title: Skapa en Google Cloud-lagringsbasanslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till ett Google Cloud-lagringskonto med API:t för flödestjänst.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Skapa en [!DNL Google Cloud Storage] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Google Cloud Storage] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till ett Google Cloud Storage-konto med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att få kontakt med [!DNL Google Cloud Storage] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | En 61-siffrig alfanumerisk sträng som används för att autentisera [!DNL Google Cloud Storage] konto till plattform. |
| `secretAccessKey` | En 40-siffrig, base-64-kodad sträng som används för att autentisera [!DNL Google Cloud Storage] konto till plattform. |
| `bucketName` | Namnet på [!DNL Google Cloud Storage] bucket. Du måste ange ett bucketnamn om du vill ge åtkomst till en viss undermapp i molnlagringen. |
| `folderPath` | Sökvägen till mappen som du vill ge åtkomst till. |

Mer information om dessa värden finns i [Google Cloud Storage HMAC-nycklar](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guide. Anvisningar om hur du skapar ditt eget ID för åtkomstnyckel och hemlig åtkomstnyckel finns i [[!DNL Google Cloud Storage] översikt](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Google Cloud Storage] autentiseringsuppgifter som en del av parametrarna för begäran.

>[!TIP]
>
>Under det här steget kan du även ange vilka undermappar ditt konto ska ha åtkomst till genom att definiera namnet på bucket och sökvägen till undermappen.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Google Cloud Storage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
          }
      },
      "connectionSpec": {
          "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.accessKeyId` | Det ID för åtkomstnyckel som är kopplat till din [!DNL Google Cloud Storage] konto. |
| `auth.params.secretAccessKey` | Den hemliga åtkomstnyckel som är kopplad till din [!DNL Google Cloud Storage] konto. |
| `auth.params.bucketName` | Namnet på [!DNL Google Cloud Storage] bucket. Du måste ange ett bucketnamn om du vill ge åtkomst till en viss undermapp i molnlagringen. |
| `auth.params.folderPath` | Sökvägen till mappen som du vill ge åtkomst till. |
| `connectionSpec.id` | The [!DNL Google Cloud Storage] anslutningsspecifikation-ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att du ska kunna utforska dina molnlagringsdata i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Google Cloud Storage] anslutning med API:er och ett unikt ID erhölls som en del av svarstexten. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för Flow Service](../../explore/cloud-storage.md).
