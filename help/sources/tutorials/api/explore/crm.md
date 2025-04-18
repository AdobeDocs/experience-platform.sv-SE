---
keywords: Experience Platform;hem;populära ämnen;CRM;crm;crm flow service
solution: Experience Platform
title: Utforska ett CRM-system med API:t för flödestjänsten
description: I den här självstudien används API:t för Flow Service för att utforska CRM-system.
exl-id: 9a8c553a-a93d-4539-a9d2-5f76a3927d92
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 1%

---

# Utforska ett CRM-system med API:t [!DNL Flow Service]

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används [!DNL Flow Service]-API:t för att utforska CRM-system.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till ett CRM-system med API:t [!DNL Flow Service].

### Skapa ett anslutnings-ID

För att kunna utforska ditt CRM-system med hjälp av [!DNL Experience Platform] API:er måste du ha ett giltigt anslutnings-ID. Om du inte redan har en anslutning till det CRM-system som du vill arbeta med kan du skapa en genom följande självstudier:

* [Microsoft Dynamics](../create/crm/ms-dynamics.md)
* [Salesforce](../create/crm/salesforce.md)

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver en extra medietypsrubrik:

* `Content-Type: application/json`

## Utforska era datatabeller

Med hjälp av anslutnings-ID:t för ditt CRM-system kan du utforska datatabellerna genom att utföra GET-förfrågningar. Använd följande anrop för att hitta sökvägen till tabellen som du vill inspektera eller importera till [!DNL Experience Platform].

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för basanslutningen för CRM-systemet. |

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar är en matris med tabeller från CRM-systemet. Hitta tabellen som du vill hämta till [!DNL Experience Platform] och notera dess `path`-egenskap, eftersom du måste ange den i nästa steg för att inspektera dess struktur.

```json
[
    {
        "type": "table",
        "name": "Solution Component Summary",
        "path": "msdyn_solutioncomponentsummary",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Quote Invoicing Product",
        "path": "msdyn_quoteinvoicingproduct",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Opportunity Relationship",
        "path": "customeropportunityrole",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspektera strukturen i en tabell

Om du vill inspektera tabellstrukturen från CRM-systemet utför du en GET-begäran samtidigt som du anger sökvägen till en tabell som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för basanslutningen för CRM-systemet. |
| `{TABLE_PATH}` | Sökvägen till en tabell. |

**Begäran**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen för en tabell. Information om var och en av tabellens kolumner finns inom elementen i arrayen `columns`.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

## Nästa steg

Genom att följa den här självstudien har du undersökt CRM-systemet, hittat sökvägen till tabellen som du vill hämta till [!DNL Experience Platform] och fått information om dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från ditt CRM-system och hämta dem till Experience Platform](../collect/crm.md).
