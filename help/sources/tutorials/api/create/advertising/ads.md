---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Google AdWords-koppling med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 1%

---


# Skapa en [!DNL Google AdWords] koppling med [!DNL Flow Service] API:t

>[!NOTE]
>
>Kopplingen [!DNL Google AdWords] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används API:t för att vägleda dig genom de olika stegen för att ansluta [!DNL Flow Service] till [!DNL Experience Platform] [!DNL Google AdWords].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till Ad med API:t [!DNL Flow Service] .

### Samla in nödvändiga inloggningsuppgifter

För [!DNL Flow Service] att kunna ansluta till AdWords måste du ange värden för följande anslutningsegenskaper:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| Kund-ID | Kund-ID för AdWords-kontot. |
| Utvecklartoken | Utvecklartoken som är associerad med hanterarkontot. |
| Uppdatera token | Uppdateringstoken som hämtats från [!DNL Google] för att auktorisera åtkomst till AdWords. |
| Klient-ID | Klient-ID:t för det [!DNL Google] program som används för att hämta uppdateringstoken. |
| Klienthemlighet | Klienthemligheten för det program [!DNL Google] som används för att hämta uppdateringstoken. |
| ID för anslutningsspecifikation | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikations-ID för [!DNL Google AdWords] är: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Mer information om dessa värden finns i det här [Google AdWords-dokumentet](https://developers.google.com/adwords/api/docs/guides/authentication).

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

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per [!DNL Google AdWords] konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

**API-format**

```https
POST /connections
```

**Begäran**

I följande begäran skapas en ny AdWords-anslutning, som konfigureras med egenskaperna i nyttolasten:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.clientCustomerID` | Kundens ID för ditt [!DNL AdWords] konto. |
| `auth.params.developerToken` | Utvecklartoken för ditt [!DNL AdWords] konto. |
| `auth.params.refreshToken` | Uppdateringstoken för ditt [!DNL AdWords] konto. |
| `auth.params.clientID` | Klient-ID för ditt [!DNL AdWords] konto. |
| `auth.params.clientSecret` | Klienthemligheten för ditt [!DNL AdWords] konto. |
| `connectionSpec.id` | ID för [!DNL Google AdWords] anslutningsspecifikation: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Google AdWords] anslutning med hjälp av [!DNL Flow Service] API:t och fått anslutningens unika ID-värde. Du kan använda detta ID i nästa självstudiekurs när du lär dig hur du [utforskar annonssystem med API:t](../../explore/advertising.md)för Flow Service.
