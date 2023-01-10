---
keywords: Experience Platform;hemanvändare;populära ämnen;rödskift;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Skapa en Amazon Redshift Base-anslutning med API:t för flödestjänsten
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Amazon Redshift med API:t för Flow Service.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Skapa en [!DNL Amazon Redshift] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Amazon Redshift] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Amazon Redshift] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL Amazon Redshift]måste du ange följande anslutningsegenskaper:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| `server` | Servern som är kopplad till din [!DNL Amazon Redshift] konto. |
| `username` | Användarnamnet som är associerat med din [!DNL Amazon Redshift] konto. |
| `password` | Lösenordet som är kopplat till [!DNL Amazon Redshift] konto. |
| `database` | The [!DNL Amazon Redshift] databas som du använder. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Amazon Redshift] är `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Mer information om hur du kommer igång finns i [[!DNL Amazon Redshift] dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

>[!NOTE]
>
>Standardkodningsstandard för [!DNL Redshift] är Unicode. Detta kan inte ändras.

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Amazon Redshift] autentiseringsuppgifter som en del av parametrarna för begäran.

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
| `auth.params.server` | Dina [!DNL Amazon Redshift] server. |
| `auth.params.database` | Databasen som är associerad med din [!DNL Amazon Redshift] konto. |
| `auth.params.password` | Lösenordet som är kopplat till [!DNL Amazon Redshift] konto. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Amazon Redshift] konto. |
| `connectionSpec.id` | The [!DNL Amazon Redshift] anslutningsspecifikation-ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Amazon Redshift] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med [!DNL Flow Service] API](../../collect/database-nosql.md)
