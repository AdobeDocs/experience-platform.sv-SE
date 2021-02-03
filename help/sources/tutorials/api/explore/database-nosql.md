---
keywords: Experience Platform;hem;populära ämnen;tredje parts databas;databasflödestjänst
solution: Experience Platform
title: Utforska en databas med API:t för Flow Service
topic: overview
description: I den här självstudien används API:t för Flow Service för att utforska innehållet och filstrukturen i en tredjepartsdatabas.
translation-type: tm+mt
source-git-commit: ddf5be2f30bc347a881bdcbc6b880f087c03e263
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Utforska en databas med hjälp av API:t [!DNL Flow Service]

I den här självstudien används API:t [!DNL Flow Service] för att utforska innehållet och filstrukturen i en tredjepartsdatabas.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till en tredjepartsdatabas med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Den här självstudien kräver att du har en giltig anslutning till den tredjepartsdatabas som du vill importera data från. En giltig anslutning innefattar databasens anslutningsspecifikations-ID och anslutnings-ID. Mer information om hur du skapar en databasanslutning och hämtar dessa värden finns i [översikten över källanslutningar](./../../../home.md#database).

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla E[!DNL xperience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med tabeller från databasen. Leta reda på tabellen som du vill hämta till [!DNL Platform] och notera dess `path`-egenskap, eftersom du måste ange den i nästa steg för att kontrollera dess struktur.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för den angivna tabellen. Information om tabellens kolumner finns i elementen i `columns`-arrayen.

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

Genom att följa den här självstudien har du undersökt din databas, hittat sökvägen till tabellen som du vill importera till [!DNL Platform] och fått information om dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från din databas och hämta den till plattformen](../collect/database-nosql.md).