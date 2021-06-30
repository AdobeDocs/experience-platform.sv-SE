---
keywords: Experience Platform;hem;populära ämnen;annonssystem;Reklamsystem
solution: Experience Platform
title: Utforska ett annonssystem med API:t för Flow Service
topic-legacy: overview
description: Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från. I den här självstudien används API:t för Flow Service för att utforska annonssystem.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 8aa8dfcc4f8a36d0898a9cc079bd98b89e3589a1
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# Utforska ett annonssystem med API:t [!DNL Flow Service]

När du har skapat en basanslutning kan du nu använda det unika basanslutnings-ID:t för att navigera och utforska källans datastruktur och innehåll. På så sätt kan du identifiera specifika objekt och deras respektive datatyper och format innan du skapar ett dataflöde och överför dem till Adobe Experience Platform.

I den här självstudien används [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). att utforska annonssystem.

## Komma igång

>[!IMPORTANT]

Den här självstudiekursen kräver att du har det unika ID:t för din annonskälla. Om du inte har det här ID:t kan du titta i självstudiekursen [Koppla en annonskälla till Platform](../../api/create/advertising/ads.md).

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till ett annonssystem med API:t [!DNL Flow Service].

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../landing/api-guide.md).

## Utforska era datatabeller

Med hjälp av basanslutningen för ert annonssystem kan ni utforska era datatabeller genom att utföra GET-förfrågningar. Använd följande anrop för att hitta sökvägen till tabellen som du vill inspektera eller importera till [!DNL Platform].

**API-format**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID:t för basanslutningen för ditt annonssystem. |

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett framgångsrikt svar är en rad tabeller från ert annonssystem. Leta reda på tabellen som du vill hämta till [!DNL Platform] och notera dess `path`-egenskap, eftersom du måste ange den i nästa steg för att kontrollera dess struktur.

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect tabellstrukturen

Om du vill inspektera tabellstrukturen från ditt annonssystem utför du en GET-förfrågan och anger tabellens sökväg som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Anslutnings-ID för ditt annonssystem. |
| `{TABLE_PATH}` | Sökvägen till en tabell i ert annonssystem. |

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för en tabell. Information om tabellens kolumner finns i elementen i `columns`-arrayen.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
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

Genom att följa den här självstudiekursen har du utforskat ditt annonssystem, hittat sökvägen till tabellen som du vill hämta till [!DNL Platform] och fått information om dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från ditt annonssystem och överföra den till Platform](../collect/advertising.md).
