---
title: Skapa en Google Cloud-lagringsbasanslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till ett Google Cloud-lagringskonto med API:t för flödestjänst.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Skapa en [!DNL Google Cloud Storage]-basanslutning med API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL Google Cloud Storage] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till ett Google Cloud Storage-konto med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till ditt [!DNL Google Cloud Storage]-konto måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | En alfanumerisk sträng på 61 tecken som används för att autentisera ditt [!DNL Google Cloud Storage]-konto för Experience Platform. |
| `secretAccessKey` | En 40-siffrig, base-64-kodad sträng som används för att autentisera ditt [!DNL Google Cloud Storage]-konto för Experience Platform. |
| `bucketName` | Namnet på din [!DNL Google Cloud Storage]-bucket. Du måste ange ett bucketnamn om du vill ge åtkomst till en viss undermapp i molnlagringen. |
| `folderPath` | Sökvägen till mappen som du vill ge åtkomst till. |

Mer information om dessa värden finns i handboken [Google Cloud Storage HMAC keys](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anvisningar om hur du skapar ditt eget ID för åtkomstnyckel och hemlig åtkomstnyckel finns i [[!DNL Google Cloud Storage] översikten](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Google Cloud Storage]-autentiseringsuppgifter som en del av parametrarna för begäran.

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
| `auth.params.accessKeyId` | Åtkomstnyckel-ID som är associerat med ditt [!DNL Google Cloud Storage]-konto. |
| `auth.params.secretAccessKey` | Den hemliga åtkomstnyckel som är associerad med ditt [!DNL Google Cloud Storage]-konto. |
| `auth.params.bucketName` | Namnet på din [!DNL Google Cloud Storage]-bucket. Du måste ange ett bucketnamn om du vill ge åtkomst till en viss undermapp i molnlagringen. |
| `auth.params.folderPath` | Sökvägen till mappen som du vill ge åtkomst till. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Google Cloud Storage]: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att du ska kunna utforska dina molnlagringsdata i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Google Cloud Storage]-anslutning med API:er och ett unikt ID har hämtats som en del av svarstexten. Du kan använda det här anslutnings-ID:t för att [utforska molnlagring med API:t för Flow Service ](../../explore/cloud-storage.md).
