---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utforska ett protokollsystem med API:t för Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 95779ae70c723c20370f9636032de366ccd928ca

---


# Utforska ett protokollsystem med API:t för Flow Service

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t för Flow Service för att utforska protokollprogram.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till ett protokollprogram med API:t för Flow Service.

### Hämta en basanslutning

För att kunna utforska ditt protokollsystem med hjälp av plattforms-API:er måste du ha ett giltigt basanslutnings-ID. Om du inte redan har en basanslutning för det protokollsystem du vill arbeta med kan du skapa en genom följande självstudie:

* [Allmän OData](../create/protocols/odata.md)

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör Flow Service, isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Utforska era datatabeller

Med anslutnings-ID:t för protokollprogrammet kan du utforska datatabellerna genom att utföra GET-begäranden. Använd följande anrop för att hitta sökvägen till tabellen som du vill inspektera eller importera till Platform.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för en protokollbasanslutning. |

**Begäran**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/a5c6b647-e784-4b58-86b6-47e784ab580b/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med tabeller från ditt protokollprogram. Leta reda på tabellen som du vill hämta till Platform och notera dess `path` egenskap, eftersom du måste ange den i nästa steg för att inspektera dess struktur.

```json
[
    {
        "type": "table",
        "name": "Categories",
        "path": "Categories",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "CustomerDemographics",
        "path": "CustomerDemographics",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Customers",
        "path": "Customers",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Orders",
        "path": "Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspektera tabellstrukturen

Om du vill inspektera strukturen för en tabell från ditt protokollprogram, ska du utföra en GET-begäran samtidigt som du anger sökvägen till en tabell som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Anslutnings-ID för protokollprogrammet. |
| `{TABLE_PATH}` | Sökvägen till en tabell i protokollprogrammet. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/a5c6b647-e784-4b58-86b6-47e784ab580b/explore?objectType=table&object=Orders' \
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
                "name": "OrderID",
                "type": "integer",
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "CustomerID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "EmployeeID",
                "type": "integer",
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "OrderDate",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du undersökt ditt protokollprogram, hittat sökvägen till tabellen som du vill importera till Platform och fått information om dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från ditt protokollprogram och överföra dem till Platform](../collect/protocols.md).
