---
keywords: Experience Platform;hem;populära ämnen;dataförberedelse;api guide;exempeldata;
solution: Experience Platform
title: Exempel på API-slutpunkt för data
description: Du kan använda ändpunkten "/samples" i Adobe Experience Platform API för att hämta, skapa, uppdatera och validera mappningsexempeldata.
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Exempeldataslutpunkt

Exempeldata kan användas när du skapar ett schema för mappningsuppsättningen. Du kan använda `/samples`-slutpunkten i API:t för dataförberedelser för att hämta, skapa och uppdatera exempeldata programmatiskt.

## Visa exempeldata

Du kan hämta en lista över alla mappningsexempeldata för din organisation genom att göra en GET-förfrågan till slutpunkten `/samples`.

**API-format**

Slutpunkten `/samples` har stöd för flera frågeparametrar som kan hjälpa dig att filtrera dina resultat. För närvarande måste du ta med både parametern `start` och parametern `limit` som en del av din begäran.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{LIMIT}` | **Krävs**. Anger antalet mappningssamplingsdata som returneras. |
| `{START}` | **Krävs**. Anger förskjutningen för resultatsidorna. Om du vill hämta den första resultatsidan anger du värdet till `start=0`. |

**Begäran**

Följande begäran hämtar de två sista mappningsexempeldata inom din organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om de två sista objekten för att mappa exempeldata.

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `sampleData` | |
| `sampleType` | |

## Skapa exempeldata

Du kan skapa exempeldata genom att göra en POST-förfrågan till slutpunkten `/samples`.

```http
POST /samples
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om dina nya exempeldata.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Skapa exempeldata genom att överföra en fil

Du kan skapa exempeldata med hjälp av en fil genom att göra en POST-förfrågan till slutpunkten `/samples/upload`.

**API-format**

```http
POST /samples/upload
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om dina nya exempeldata.

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Söka efter ett specifikt exempeldataobjekt

Du kan söka efter ett specifikt objekt med exempeldata genom att ange dess ID i sökvägen för en GET-begäran till slutpunkten `/samples`.

**API-format**

```http
GET /samples/{SAMPLE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SAMPLE_ID}` | ID för det exempeldataobjekt som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om det exempeldataobjekt som du vill hämta.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Uppdatera exempeldata

Du kan uppdatera ett specifikt exempeldataobjekt genom att ange dess ID i sökvägen för en PUT-begäran till slutpunkten `/samples`.

**API-format**

```http
PUT /samples/{SAMPLE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SAMPLE_ID}` | ID:t för det exempeldataobjekt som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar angivna exempeldata. Det uppdaterar efternamnet från &quot;Smith&quot; till &quot;Lee&quot;.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om uppdaterade exempeldata.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
