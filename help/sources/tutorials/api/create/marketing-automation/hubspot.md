---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en HubSpot-anslutning med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Skapa en HubSpot-anslutning med API:t för Flow Service

>[!NOTE]
>HubSpot-anslutningen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Experience Platform till HubSpot.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till HubSpot med API:t för Flow Service.

### Samla in nödvändiga inloggningsuppgifter

För att Flow Service ska kunna ansluta till HubSpot måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Klient-ID | Klient-ID som är associerat med ditt HubSpot-program. |
| Klienthemlighet | Klienthemligheten som är kopplad till ditt HubSpot-program. |
| Åtkomsttoken | Åtkomsttoken som fås när din OAuth-integration autentiseras initialt. |
| Uppdatera token | Den uppdateringstoken som erhölls när OAuth-integreringen autentiserades initialt. |
| ID för anslutningsspecifikation | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikation-ID för HubSpot är: `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Mer information om hur du kommer igång finns i det här [HubSpot-dokumentet](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör Flow Service, isoleras till specifika virtuella sandlådor. Alla förfrågningar till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per HubSpot-konto eftersom det kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```https
POST /connections
```

**Begäran**

För att kunna skapa en HubSpot-anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POST-begäran. Anslutningsspecifikationens ID för HubSpot är `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.clientId` | Klient-ID som är associerat med ditt HubSpot-program. |
| `auth.params.clientSecret` | Klienthemligheten som är kopplad till ditt HubSpot-program. |
| `auth.params.accessToken` | Åtkomsttoken som fås när din OAuth-integration autentiseras initialt. |
| `auth.params.refreshToken` | Den uppdateringstoken som erhölls när OAuth-integreringen autentiserades initialt. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen för API:t, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

I den här självstudiekursen har du skapat en HubSpot-anslutning med API:t för Flow Service och fått anslutningens unika ID-värde. Du kan använda detta anslutnings-ID i nästa självstudiekurs när du lär dig hur du [utforskar automatiserade marknadsföringssystem med API:t](../../explore/marketing-automation.md)för Flow Service.