---
keywords: Experience Platform;hem;populära ämnen;tredje parts databas;databasflödestjänst
solution: Experience Platform
title: Utforska en databas med API:t för Flow Service
description: I den här självstudien används API:t för Flow Service för att utforska innehållet och filstrukturen i en tredjepartsdatabas.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# Utforska en databas med [!DNL Flow Service] API

I den här självstudiekursen används [!DNL Flow Service] API för att utforska innehållet och filstrukturen i en tredjepartsdatabas.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till en tredjepartsdatabas med hjälp av [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

Den här självstudien kräver att du har en giltig anslutning till den tredjepartsdatabas som du vill importera data från. En giltig anslutning innefattar databasens anslutningsspecifikations-ID och anslutnings-ID. Mer information om hur du skapar en databasanslutning och hämtar dessa värden finns i [översikt över källanslutningar](./../../../home.md#database).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla E[!DNL xperience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive sådana som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Utforska era datatabeller

Med hjälp av anslutnings-ID:t för din databas kan du utforska dina datatabeller genom att utföra GET-förfrågningar. Använd följande anrop för att hitta sökvägen till tabellen som du vill inspektera eller importera till [!DNL Platform].

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Anslutnings-ID för datakällan. |

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med tabeller från databasen. Hitta den tabell du vill ta med [!DNL Platform] och notera `path` -egenskapen, eftersom du måste ange den i nästa steg för att inspektera dess struktur.

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect tabellstrukturen

Om du vill inspektera strukturen för en tabell från din databas utför du en GET-förfrågan samtidigt som du anger sökvägen till en tabell som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID:t för en databasanslutning. |
| `{TABLE_PATH}` | Sökvägen till en tabell. |

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den angivna tabellen. Information om tabellens kolumner finns i element i `columns` array.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "TestID",
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
            }
        ]
    }
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du utforskat databasen och hittat sökvägen till tabellen som du vill importera till [!DNL Platform]och fick information om sin struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från databasen och ta in dem på plattformen](../collect/database-nosql.md).
