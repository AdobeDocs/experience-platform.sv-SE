---
keywords: Experience Platform;home;popular topics;redshift;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Skapa en Amazon Redshift-koppling med API:t för Flow Service
topic: overview
type: Tutorial
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Experience Platform till Amazon Redshift (nedan kallat Redshift).
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---


# Skapa en [!DNL Amazon Redshift] koppling med [!DNL Flow Service] API:t

>[!NOTE]
>
>Kopplingen [!DNL Amazon Redshift] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används API:t för att vägleda dig genom de olika stegen för att ansluta [!DNL Flow Service] till [!DNL Experience Platform] (kallas nedan&quot; [!DNL Amazon Redshift][!DNL Redshift]&quot;).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Redshift] med [!DNL Flow Service] API:t.

### Samla in nödvändiga inloggningsuppgifter

För [!DNL Flow Service] att kunna ansluta till [!DNL Redshift]måste du ange följande anslutningsegenskaper:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| `server` | Servern som är kopplad till ditt [!DNL Redshift] konto. |
| `username` | Användarnamnet som är associerat med ditt [!DNL Redshift] konto. |
| `password` | Lösenordet som är kopplat till ditt [!DNL Redshift] konto. |
| `database` | Den [!DNL Redshift] databas du använder. |

Mer information om hur du kommer igång finns i [detta Redshift-dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Söka efter anslutningsspecifikationer

För att kunna skapa en [!DNL Redshift] anslutning måste det finnas en uppsättning [!DNL Redshift] anslutningsspecifikationer inom [!DNL Flow Service]. Det första steget i att ansluta [!DNL Platform] till [!DNL Redshift] är att hämta dessa specifikationer.

**API-format**

Varje tillgänglig källa har en egen unik uppsättning anslutningsspecifikationer för att beskriva kopplingsegenskaper som autentiseringskrav. Du kan söka efter anslutningsspecifikationer för [!DNL Redshift] genom att utföra en GET-förfrågan och använda frågeparametrar.

Om du skickar en GET-begäran utan frågeparametrar returneras anslutningsspecifikationerna för alla tillgängliga källor. Du kan ta med frågan `property=name=="amazon-redshift"` för att få information om [!DNL Redshift].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="amazon-redshift"
```

**Begäran**

Följande begäran hämtar anslutningsspecifikationerna för [!DNL Redshift].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="amazon-redshift"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar anslutningsspecifikationerna för [!DNL Redshift], inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en basanslutning.

```json
{
    "items": [
        {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "name": "amazon-redshift",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "server": {
                                "type": "string",
                                "description": "IP address or host name of the Amazon Redshift server"
                            },
                            "username": {
                                "type": "string",
                                "description": "Name of user who has access to the database"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "database": {
                                "type": "string",
                                "description": "Name of the Amazon Redshift database"
                            }
                        },
                        "required": [
                            "server",
                            "username",
                            "password",
                            "database"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Skapa en basanslutning

En basanslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en basanslutning krävs per [!DNL Redshift] konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

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
| `auth.params.server` | Din [!DNL Redshift] server. |
| `auth.params.database` | Databasen som är kopplad till ditt [!DNL Redshift] konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Redshift] konto. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Redshift] konto. |
| `connectionSpec.id` | Anslutningsspecifikationen `id` för ditt [!DNL Redshift] konto som hämtades i föregående steg. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Redshift] basanslutning med hjälp av [!DNL Flow Service] -API:t och har fått anslutningens unika ID-värde. Du kan använda detta grundläggande anslutnings-ID i nästa självstudiekurs när du lär dig hur du [utforskar databaser eller NoSQL-system med API:t](../../explore/database-nosql.md)för Flow Service.
