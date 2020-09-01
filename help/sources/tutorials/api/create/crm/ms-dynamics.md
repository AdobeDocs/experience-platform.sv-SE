---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Skapa en Microsoft Dynamics-anslutning med API:t för Flow Service
topic: overview
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta plattformen till ett Microsoft Dynamics-konto (nedan kallat Dynamics) för att samla in CRM-data.
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Skapa en [!DNL Microsoft Dynamics] koppling med [!DNL Flow Service] API:t

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används API:t för att vägleda dig genom stegen för att ansluta [!DNL Flow Service] till ett [!DNL Platform] [!DNL Microsoft Dynamics] Dynamics-konto för att samla in CRM-data.

Om du föredrar att använda användargränssnittet i [!DNL Experience Platform]innehåller [Dynamics-gränssnittsjälvstudiekursen](../../../ui/create/crm/dynamics.md) för källanslutning stegsinstruktioner för att utföra liknande åtgärder.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): E[!DNL xperience Platform] tillhandahåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL Platform] till ett Dynamics-konto med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För [!DNL Flow Service] att kunna ansluta till [!DNL Dynamics]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUri` | Tjänst-URL:en för din [!DNL Dynamics] instans. |
| `username` | Användarnamnet för ditt [!DNL Dynamics] användarkonto. |
| `password` | Lösenordet för ditt [!DNL Dynamics] konto. |

Mer information om hur du kommer igång finns i [det här Dynamics-dokumentet](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

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

Innan du ansluter [!DNL Platform] till ett [!DNL Dynamics] konto måste du verifiera att det finns anslutningsspecifikationer för [!DNL Dynamics]. Om det inte finns några anslutningsspecifikationer går det inte att ansluta.

Varje tillgänglig källa har en egen unik uppsättning anslutningsspecifikationer för att beskriva kopplingsegenskaper som autentiseringskrav. Du kan söka efter anslutningsspecifikationer för [!DNL Dynamics] genom att utföra en GET-förfrågan och använda frågeparametrar.

**API-format**

Om du skickar en GET-begäran utan frågeparametrar returneras anslutningsspecifikationerna för alla tillgängliga källor. Du kan ta med frågan `property=name=="dynamics-online"` för att få information om [!DNL Dynamics].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Begäran**

Följande begäran hämtar anslutningsspecifikationerna för [!DNL Dynamics].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar anslutningsspecifikationerna för [!DNL Dynamics], inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en basanslutning.

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

En basanslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en basanslutning krävs per [!DNL Dynamics] konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

Utför följande POST-förfrågan för att skapa en basanslutning.

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
| `auth.params.serviceUri` | Den tjänst-URI som är associerad med din [!DNL Dynamics] instans. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Dynamics] konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Dynamics] konto. |
| `connectionSpec.id` | Anslutningsspecifikationen `id` för ditt [!DNL Dynamics] konto som hämtades i föregående steg. |

**Svar**

Ett lyckat svar innehåller basanslutningsens unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en basanslutning för ditt [!DNL Dynamics] konto med hjälp av API:er och ett unikt ID har hämtats som en del av svarstexten. Du kan använda detta grundläggande anslutnings-ID i nästa självstudiekurs när du lär dig hur du [utforskar CRM-system med API:t](../../explore/crm.md)för Flow Service.