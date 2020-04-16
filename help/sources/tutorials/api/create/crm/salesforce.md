---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Salesforce-koppling med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: cc999ce1ab426f412c0cc2b69173a336a14024f3

---


# Skapa en Salesforce-koppling med API:t för Flow Service

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta plattformen till ett Salesforce-konto för att samla in CRM-data.

Om du föredrar att använda användargränssnittet i Experience Platform innehåller [Dynamics- eller Salesforce-gränssnittet för källkopplingen](../../../ui/create/crm/dynamics-salesforce.md) stegvisa instruktioner för att utföra liknande åtgärder.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta plattformen till ett Salesforce-konto med API:t för Flow Service.

### Samla in nödvändiga inloggningsuppgifter

För att Flow Service ska kunna ansluta till Salesforce måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `environmentUrl` | URL:en för Salesforce-källinstansen. |
| `username` | Användarnamnet för Salesforce-användarkontot. |
| `password` | Lösenordet för Salesforce-användarkontot. |
| `securityToken` | Säkerhetstoken för Salesforce-användarkontot. |

Mer information om hur du kommer igång finns i [det här Salesforce-dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

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

Innan du ansluter plattformen till ett Salesforce-konto måste du verifiera att det finns anslutningsspecifikationer för Salesforce. Om det inte finns några anslutningsspecifikationer går det inte att ansluta.

Varje tillgänglig källa har en egen unik uppsättning anslutningsspecifikationer för att beskriva kopplingsegenskaper som autentiseringskrav. Du kan söka efter anslutningsspecifikationer för Salesforce genom att utföra en GET-begäran och använda frågeparametrar.

**API-format**

Om du skickar en GET-begäran utan frågeparametrar returneras anslutningsspecifikationerna för alla tillgängliga källor. Du kan ta med frågan `property=name=="salesforce"` för att få information särskilt om Salesforce.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce"
```

**Begäran**

Följande begäran hämtar anslutningsspecifikationerna för Salesforce.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name==%22salesforce%22' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar anslutningsspecifikationerna för Salesforce, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en basanslutning.

```json
{
    "items": [
        {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "name": "salesforce",
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
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Skapa en basanslutning

En basanslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en basanslutning krävs per Salesforce-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

Utför följande POST-begäran för att skapa en basanslutning.

**API-format**

```http
POST /connections
```

**Begäran**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Base Connection",
        "description": "Base connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.username` | Användarnamnet som är associerat med ditt Salesforce-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt Salesforce-konto. |
| `auth.params.securityToken` | Säkerhetstoken som är associerad med ditt Salesforce-konto. |
| `connectionSpec.id` | Anslutningsspecifikationen `id` för Salesforce-kontot som hämtades i föregående steg. |

**Svar**

Ett lyckat svar innehåller basanslutningsens unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en basanslutning för ditt Salesforce-konto med hjälp av API:er och ett unikt ID hämtades som en del av svarstexten. Du kan använda detta grundläggande anslutnings-ID i nästa självstudiekurs när du lär dig hur du [utforskar CRM-system med API:t](../../explore/crm.md)för Flow Service.