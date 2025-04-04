---
keywords: Experience Platform;home;populära topics;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Skapa en PostSQL-basanslutning med API:t för Flow-tjänsten
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till PostgreSQL med API:t för Flow Service.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Skapa en [!DNL PostgreSQL]-basanslutning med API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL PostgreSQL] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL PostgreSQL] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL PostgreSQL] måste du ange följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som är associerad med ditt [!DNL PostgreSQL]-konto. Anslutningssträngsmönstret [!DNL PostgreSQL] är: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL PostgreSQL] är `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Mer information om hur du hämtar en anslutningssträng finns i det här [[!DNL PostgreSQL] dokumentet](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Aktivera SSL-kryptering för anslutningssträngen

Du kan aktivera SSL-kryptering för anslutningssträngen [!DNL PostgreSQL] genom att lägga till anslutningssträngen med följande egenskaper:

| Egenskap | Beskrivning | Exempel |
| --- | --- | --- |
| `EncryptionMethod` | Gör att du kan aktivera SSL-kryptering på dina [!DNL PostgreSQL]-data. | <uL><li>`EncryptionMethod=0`(Inaktiverad)</li><li>`EncryptionMethod=1`(Aktiverad)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validerar certifikat som skickas av din [!DNL PostgreSQL]-databas när `EncryptionMethod` används. | <uL><li>`ValidationServerCertificate=0`(Inaktiverad)</li><li>`ValidationServerCertificate=1`(Aktiverad)</li></ul> |

Följande är ett exempel på en [!DNL PostgreSQL]-anslutningssträng med SSL-kryptering: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL PostgreSQL]-autentiseringsuppgifter som en del av parametrarna för begäran.

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
| `auth.params.connectionString` | Anslutningssträngen som är associerad med ditt [!DNL PostgreSQL]-konto. Anslutningssträngsmönstret [!DNL PostgreSQL] är: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID:n [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyskapade basanslutningen. Detta ID krävs för att utforska din [!DNL PostgreSQL]-databas i nästa självstudie.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL PostgreSQL]-anslutningsbasanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
