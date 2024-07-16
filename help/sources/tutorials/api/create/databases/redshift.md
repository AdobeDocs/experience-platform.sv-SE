---
title: Skapa en Amazon Redshift Base-anslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till Amazon Redshift med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Skapa en [!DNL Amazon Redshift]-basanslutning med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>Källan [!DNL Amazon Redshift] är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL Amazon Redshift] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Amazon Redshift] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Amazon Redshift] måste du ange följande anslutningsegenskaper:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| `server` | Servern som är associerad med ditt [!DNL Amazon Redshift]-konto. |
| `port` | TCP-porten som en [!DNL Amazon Redshift]-server använder för att avlyssna klientanslutningar. |
| `username` | Användarnamnet som är associerat med ditt [!DNL Amazon Redshift]-konto. |
| `password` | Lösenordet som är kopplat till ditt [!DNL Amazon Redshift]-konto. |
| `database` | Databasen [!DNL Amazon Redshift] som du använder. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Amazon Redshift] är `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Mer information om hur du kommer igång finns i det här [[!DNL Amazon Redshift] dokumentet](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

>[!NOTE]
>
>Standardkodningsstandarden för [!DNL Redshift] är Unicode. Detta kan inte ändras.

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till slutpunkten `/connections` och anger dina autentiseringsuppgifter för [!DNL Amazon Redshift] som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Amazon Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| ------------- | --------------- |
| `auth.params.server` | Din [!DNL Amazon Redshift]-server. |
| `auth.params.port` | TCP-porten som servern [!DNL Amazon Redshift] använder för att avlyssna klientanslutningar. |
| `auth.params.database` | Databasen som är associerad med ditt [!DNL Amazon Redshift]-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Amazon Redshift]-konto. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Amazon Redshift]-konto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Amazon Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Amazon Redshift]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/database-nosql.md)
