---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en PostgreSQL-koppling med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Skapa en PostgreSQL-koppling med API:t för Flow Service

>[!NOTE]
>PostgreSQL-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Experience Platform till PostgreSQL (nedan kallat PSQL).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till PSQL med API:t för Flow Service.

### Samla in nödvändiga inloggningsuppgifter

För att Flow Service ska kunna ansluta till PSQL måste du ange följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som är associerad med ditt PSQL-konto. |

Mer information om hur du kommer igång finns i det här [PSQL-dokumentet](https://www.postgresql.org/docs/9.2/app-psql.html).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör Flow Service, isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Söka efter anslutningsspecifikationer

För att kunna skapa en PSQL-anslutning måste det finnas en uppsättning PSQL-anslutningsspecifikationer i Flow Service. Det första steget i att ansluta Platform till PSQL är att hämta dessa specifikationer.

**API-format**

Varje tillgänglig källa har en egen unik uppsättning anslutningsspecifikationer för att beskriva kopplingsegenskaper som autentiseringskrav. Om du skickar en GET-begäran till `/connectionSpecs` slutpunkten returneras anslutningsspecifikationerna för alla tillgängliga källor. Du kan även ta med frågan `property=name=="postgre-sql"` för att få information om PSQL.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="postgre-sql"
```

**Begäran**

Följande begäran hämtar anslutningsspecifikationerna för PSQL.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="postgre-sql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar anslutningsspecifikationerna för PSQL, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en basanslutning.

```json
{
    "items": [
        {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "name": "postgre-sql",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for PostgreSQL",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to PostgreSQL",
                        "properties": {
                            "connectionString": {
                                "type": "string",
                                "description": "An ODBC connection string to connect to Azure Database for PostgreSQL.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Skapa en basanslutning

En basanslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Det krävs bara en basanslutning per PSQL-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for PostgreSQL",
        "description": "Base connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
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
| `auth.params.connectionString` | Anslutningssträngen som är associerad med ditt PSQL-konto. |
| `connectionSpec.id` | Anslutningsspecifikationen `id` för ditt PSQL-konto som hämtades i föregående steg. |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nya basanslutningen. Detta ID krävs för att utforska din PSQL-databas i nästa självstudiekurs.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en PSQL-basanslutning med API:t för Flow Service och fått anslutningens unika ID-värde. Du kan använda detta grundläggande anslutnings-ID i nästa självstudiekurs när du lär dig hur du [utforskar databaser eller NoSQL-system med API:t](../../explore/database-nosql.md)för Flow Service.
