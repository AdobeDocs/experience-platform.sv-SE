---
keywords: Experience Platform;home;popular topics;Azure Data Explorer;data explorer;Data Explorer
solution: Experience Platform
title: Skapa en Azure Data Explorer-koppling med API:t för Flow Service
topic: overview
type: Tutorial
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Azure Data Explorer (nedan kallad Data Explorer) till Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Skapa en [!DNL Azure Data Explorer] koppling med [!DNL Flow Service] API:t

>[!NOTE]
>
>Kopplingen [!DNL Azure Data Explorer] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används API:t för att vägleda dig genom de olika stegen för att ansluta [!DNL Flow Service] (nedan kallad Data Explorer) till [!DNL Azure Data Explorer] [!DNL Experience Platform].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Data Explorer] med [!DNL Flow Service] API:t.

### Samla in nödvändiga inloggningsuppgifter

För [!DNL Flow Service] att kunna ansluta till [!DNL Data Explorer]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `endpoint` | Serverns slutpunkt.. [!DNL Data Explorer] . |
| `database` | Namnet på [!DNL Data Explorer] databasen. |
| `tenant` | Det unika klient-ID som används för att ansluta till [!DNL Data Explorer] databasen. |
| `servicePrincipalId` | Det unika tjänstens huvudnamn-ID som används för att ansluta till [!DNL Data Explorer] databasen. |
| `servicePrincipalKey` | Den unika tjänstens huvudnyckel som används för att ansluta till [!DNL Data Explorer] databasen. |
| `connectionSpec.id` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikationens ID för [!DNL Data Explorer] är `0479cc14-7651-4354-b233-7480606c2ac3`. |

Mer information om hur du kommer igång finns i [det här Datan Explorer](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla E[!DNL xperience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en koppling krävs per [!DNL Data Explorer] konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL Data Explorer] anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POSTEN. Anslutningsspecifikationens ID för [!DNL Data Explorer] är `0479cc14-7651-4354-b233-7480606c2ac3`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.endpoint` | Serverns slutpunkt.. [!DNL Data Explorer] . |
| `auth.params.database` | Namnet på [!DNL Data Explorer] databasen. |
| `auth.params.tenant` | Det unika klient-ID som används för att ansluta till [!DNL Data Explorer] databasen. |
| `auth.params.servicePrincipalId` | Det unika tjänstens huvudnamn-ID som används för att ansluta till [!DNL Data Explorer] databasen. |
| `auth.params.servicePrincipalKey` | Den unika tjänstens huvudnyckel som används för att ansluta till [!DNL Data Explorer] databasen. |
| `connectionSpec.id` | Anslutningens spec-ID [!DNL Data Explorer] : `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Data Explorer] anslutning med hjälp av [!DNL Flow Service] API:t och fått anslutningens unika ID-värde. Du kan använda det här ID:t i nästa självstudiekurs när du lär dig hur du [utforskar databaser med API:t](../../explore/database-nosql.md)för Flow Service.
