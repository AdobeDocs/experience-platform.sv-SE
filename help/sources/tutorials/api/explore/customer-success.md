---
keywords: Experience Platform;home;popular topics;cs;CS;customer success system
solution: Experience Platform
title: Utforska ett lyckat kundsystem med API:t för Flow Service
topic: overview
description: I den här självstudien används API:t för Flow Service för att utforska system för Customer Success (CS).
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---


# Utforska ett lyckat kundsystem med hjälp av [!DNL Flow Service] API

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används API:t för att utforska system för Customer Success (CS). [!DNL Flow Service]

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
* [Sandlådor](../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till ett CS-system med hjälp av [!DNL Flow Service] API:t.

### Hämta en basanslutning

För att kunna utforska CS-systemet med API: [!DNL Platform] er måste du ha ett giltigt basanslutnings-ID. Om du inte redan har en basanslutning för det CS-system du vill arbeta med kan du skapa en genom följande självstudier:

* [Salesforce Service Cloud](../create/customer-success/salesforce-service-cloud.md)
* [ServiceNow](../create/customer-success/servicenow.md)

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Utforska era datatabeller

Med basanslutningen för ditt CS-system kan du utforska datatabeller genom att utföra GET-förfrågningar. Använd följande anrop för att hitta sökvägen till tabellen som du vill inspektera eller importera till [!DNL Platform].

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID:t för en CS-basanslutning. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med tabeller från CS-systemet. Leta reda på tabellen som du vill hämta in [!DNL Platform] och notera dess `path` egenskap, eftersom du måste ange den i nästa steg för att kontrollera dess struktur.

```json
[
    {
        "type": "table",
        "name": "Accepted Event Relation",
        "path": "AcceptedEventRelation",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account",
        "path": "Account",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Change Event",
        "path": "AccountChangeEvent",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Clean Info",
        "path": "AccountCleanInfo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect tabellstrukturen

Om du vill inspektera tabellstrukturen i ditt CS-system utför du en GET-förfrågan och anger tabellens sökväg som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID:t för en CS-basanslutning. |
| `{TABLE_PATH}` | Sökvägen till en tabell. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den angivna tabellen. Information om tabellens kolumner finns i elementen i `columns` arrayen.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
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

I den här självstudiekursen har du undersökt CS-systemet, hittat sökvägen till tabellen som du vill importera [!DNL Platform]och fått information om dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från ditt CS-system och överföra dem till Platform](../collect/customer-success.md).