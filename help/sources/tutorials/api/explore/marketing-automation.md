---
keywords: Experience Platform;hemmabruk;populära ämnen;automatiserad marknadsföring
solution: Experience Platform
title: Utforska ett marknadsföringsautomatiseringssystem med API:t för Flow Service
description: I den här självstudien används API:t för Flow Service för att utforska automatiserade marknadsföringssystem.
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Utforska ett automatiserat marknadsföringssystem med [!DNL Flow Service] API

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används [!DNL Flow Service] API för att utforska automatiserade marknadsföringssystem.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till ett automatiserat marknadsföringssystem med hjälp av [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

Den här självstudiekursen kräver att du har en giltig anslutning till det program för automatiserad marknadsföring från tredje part som du vill importera data från. En giltig anslutning innefattar programmets anslutningsspecifikations-ID och anslutnings-ID. Mer information om hur du skapar en anslutning för automatiserad marknadsföring och hämtar dessa värden finns i [koppla en källa för automatiserad marknadsföring till plattformen](../../api/create/marketing-automation/hubspot.md) självstudiekurs.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive sådana som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Utforska era datatabeller

Med hjälp av basanslutningen för ert automatiseringssystem för marknadsföring kan ni utforska era datatabeller genom att utföra GETTER. Använd följande anrop för att hitta sökvägen till tabellen som du vill inspektera eller importera till [!DNL Platform].

**API-format**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID:t för basanslutningen för ert automatiseringssystem för marknadsföring. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett framgångsrikt svar är en mängd tabeller från ert marknadsföringssystem. Hitta den tabell du vill ta med [!DNL Platform] och notera `path` -egenskapen, eftersom du måste ange den i nästa steg för att inspektera dess struktur.

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## Inspect tabellstrukturen

Om du vill inspektera tabellstrukturen från ditt automatiseringssystem för marknadsföring, ska du utföra en GET-förfrågan och ange sökvägen till en tabell som en frågeparameter.

**API-format**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Anslutnings-ID för ert automatiseringssystem för marknadsföring. |
| `{TABLE_PATH}` | Sökvägen till en tabell inom ert automatiserade marknadsföringssystem. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för en tabell. Information om tabellens kolumner finns i element i `columns` array.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du utforskat ditt automatiseringssystem för marknadsföring och hittat sökvägen till tabellen du vill ta med i [!DNL Platform]och fick information om sin struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från ert automatiseringssystem för marknadsföring och införliva dem i plattformen](../collect/marketing-automation.md).
