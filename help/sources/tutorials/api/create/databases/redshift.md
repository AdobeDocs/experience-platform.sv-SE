---
keywords: Experience Platform;hemanvändare;populära ämnen;rödskift;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Skapa en Amazon Redshift Base-anslutning med API:t för flödestjänsten
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Amazon Redshift med API:t för Flow Service.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# Skapa en [!DNL Amazon Redshift]-basanslutning med hjälp av API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Amazon Redshift] med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Amazon Redshift] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Amazon Redshift] måste du ange följande anslutningsegenskaper:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| `server` | Den server som är associerad med ditt [!DNL Amazon Redshift]-konto. |
| `username` | Användarnamnet som är associerat med ditt [!DNL Amazon Redshift]-konto. |
| `password` | Lösenordet som är kopplat till ditt [!DNL Amazon Redshift]-konto. |
| `database` | Den [!DNL Amazon Redshift]-databas du använder. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikationens ID för [!DNL Amazon Redshift] är `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Mer information om hur du kommer igång finns i det här [[!DNL Amazon Redshift] dokumentet](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Amazon Redshift] som en del av parametrarna för begäran.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
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
| `auth.params.database` | Databasen som är associerad med ditt [!DNL Amazon Redshift]-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Amazon Redshift]-konto. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Amazon Redshift]-konto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID för [!DNL Amazon Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Amazon Redshift]-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda detta anslutnings-ID i nästa självstudiekurs när du lär dig att [utforska databaser eller NoSQL-system med API:t för Flow Service](../../explore/database-nosql.md).
