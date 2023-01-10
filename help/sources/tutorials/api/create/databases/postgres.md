---
keywords: Experience Platform;hem;populära ämnen;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Skapa en PostSQL-basanslutning med API:t för Flow Service
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till PostgreSQL med API:t för Flow Service.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---

# Skapa en [!DNL PostgreSQL] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL PostgreSQL] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL PostgreSQL] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] att ansluta till [!DNL PostgreSQL]måste du ange följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som är associerad med din [!DNL PostgreSQL] konto. The [!DNL PostgreSQL] anslutningssträngsmönstret är: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL PostgreSQL] är `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Mer information om hur du hämtar en anslutningssträng finns i [[!DNL PostgreSQL] dokument](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Aktivera SSL-kryptering för anslutningssträngen

Du kan aktivera SSL-kryptering för din [!DNL PostgreSQL] anslutningssträng genom att lägga till anslutningssträngen med följande egenskaper:

| Egenskap | Beskrivning | Exempel |
| --- | --- | --- |
| `EncryptionMethod` | Gör att du kan aktivera SSL-kryptering på din [!DNL PostgreSQL] data. | <uL><li>`EncryptionMethod=0`(Inaktiverat)</li><li>`EncryptionMethod=1`(Aktiverad)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validerar certifikat som skickats av din [!DNL PostgreSQL] databas när `EncryptionMethod` används. | <uL><li>`ValidationServerCertificate=0`(Inaktiverat)</li><li>`ValidationServerCertificate=1`(Aktiverad)</li></ul> |

Följande är ett exempel på en [!DNL PostgreSQL] anslutningssträng tillagd med SSL-kryptering: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL PostgreSQL] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL PostgreSQL]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| ------------- | --------------- |
| `auth.params.connectionString` | Anslutningssträngen som är associerad med din [!DNL PostgreSQL] konto. The [!DNL PostgreSQL] anslutningssträngsmönstret är: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | The [!DNL PostgreSQL] ID för anslutningsspecifikation: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nya basanslutningen. Detta ID krävs för att du ska kunna utforska [!DNL PostgreSQL] i nästa självstudiekurs.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL PostgreSQL] anslutningsbasanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med [!DNL Flow Service] API](../../collect/database-nosql.md)
