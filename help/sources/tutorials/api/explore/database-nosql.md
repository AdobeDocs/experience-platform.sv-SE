---
title: Utforska en databas med API:t för Flow Service
description: I den här självstudien används API:t för Flow Service för att utforska innehållet och filstrukturen i en tredjepartsdatabas.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 46e1a62e558a209ffed4a693cfd71ad5e76d7d98
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---

# Utforska en databas med API:t [!DNL Flow Service]

I den här självstudien används API:t [!DNL Flow Service] för att utforska innehållet och filstrukturen i en tredjepartsdatabas.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till en tredjepartsdatabas med API:t [!DNL Flow Service].

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../landing/api-guide.md).

## Utforska era datatabeller

Med hjälp av anslutnings-ID:t för din databas kan du utforska dina datatabeller genom att utföra GET-förfrågningar. Använd följande anrop för att hitta sökvägen till tabellen som du vill inspektera eller importera till Experience Platform.

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

Ett lyckat svar returnerar en array med tabeller från databasen. Leta reda på tabellen som du vill hämta till Experience Platform och notera dess `path`-egenskap, eftersom du måste ange den i nästa steg för att inspektera dess struktur.

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

## Inspektera strukturen i en tabell

Om du vill inspektera strukturen för en tabell från din databas utför du en GET-begäran samtidigt som du anger sökvägen till en tabell som en frågeparameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID för en databasanslutning. |
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

Ett lyckat svar returnerar strukturen för den angivna tabellen. Information om var och en av tabellens kolumner finns inom elementen i arrayen `columns`.

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
    },
    "data": [],
    "cdcMetadata": {
      "columnDetected": true
    }
}
```

## Nästa steg

I den här självstudiekursen har du undersökt din databas, hittat sökvägen till tabellen som du vill importera till Experience Platform och fått information om dess struktur. Du kan använda den här informationen i nästa självstudiekurs för att [samla in data från din databas och hämta dem till Experience Platform](../collect/database-nosql.md).
