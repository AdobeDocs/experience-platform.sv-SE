---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Microsoft Dynamics-anslutning med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 6c86cec91774f3444dc90042cd7ad5c71429aabd

---


# Skapa en Microsoft Dynamics-anslutning med API:t för Flow Service

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta plattformen till ett Microsoft Dynamics-konto (nedan kallat Dynamics) för att samla in CRM-data.

Om du föredrar att använda användargränssnittet i Experience Platform innehåller [Dynamics- eller Salesforce-gränssnittet för källkopplingen](../../../ui/create/crm/dynamics-salesforce.md) stegvisa instruktioner för att utföra liknande åtgärder.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta plattformen till ett Dynamics-konto med API:t för Flow Service.

### Samla in nödvändiga inloggningsuppgifter

För att Flow Service ska kunna ansluta till Dynamics måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUri` | Tjänst-URL:en för Dynamics-instansen. |
| `username` | Användarnamnet för ditt Dynamics-användarkonto. |
| `password` | Lösenordet för ditt Dynamics-konto. |

Mer information om hur du kommer igång finns i [det här Dynamics-dokumentet](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

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

Innan du ansluter plattformen till ett Dynamics-konto måste du verifiera att det finns anslutningsspecifikationer för Dynamics. Om det inte finns några anslutningsspecifikationer går det inte att ansluta.

Varje tillgänglig källa har en egen unik uppsättning anslutningsspecifikationer för att beskriva kopplingsegenskaper som autentiseringskrav. Du kan söka efter anslutningsspecifikationer för Dynamics genom att utföra en GET-begäran och använda frågeparametrar.

**API-format**

Om du skickar en GET-begäran utan frågeparametrar returneras anslutningsspecifikationerna för alla tillgängliga källor. Du kan inkludera frågan `property=name=="dynamics-online"` för att få information specifikt för Dynamics.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Begäran**

Följande begäran hämtar anslutningsspecifikationerna för Dynamics.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar anslutningsspecifikationerna för Dynamics, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en basanslutning.

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Skapa en basanslutning

En basanslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en basanslutning krävs per Dynamics-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

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
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.serviceUri` | Den tjänst-URI som är associerad med Dynamics-instansen. |
| `auth.params.username` | Användarnamnet som är associerat med ditt Dynamics-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt Dynamics-konto. |
| `connectionSpec.id` | Anslutningsspecifikationen `id` för ditt Dynamics-konto som hämtades i föregående steg. |

**Svar**

Ett lyckat svar innehåller basanslutningsens unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en basanslutning för ditt Dynamics-konto med API:er och ett unikt ID hämtades som en del av svarstexten. Du kan använda detta grundläggande anslutnings-ID i nästa självstudiekurs när du lär dig hur du [utforskar CRM-system med API:t](../../explore/crm.md)för Flow Service.