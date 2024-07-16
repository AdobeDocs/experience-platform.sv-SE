---
keywords: Experience Platform;home;populära topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: API-slutpunkt för anslutningsparametrar
description: Du kan hämta anslutningsparametrar för användning av den interaktiva tjänsten genom att göra en GET-förfrågan till slutpunkten /connection_parameters.
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Slutpunkt för anslutningsparametrar

## Exempel på API-anrop

I följande avsnitt får du hjälp med API-anropet som du kan göra med API:t [!DNL Query Service]. Anropet innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

### Begär anslutningsparametrar

Du kan hämta anslutningsparametrar genom att göra en GET-förfrågan till slutpunkten `/connection_parameters`. Mer information om klienter som använder anslutningsparametrar för att ansluta via den interaktiva tjänsten finns i dokumentationen om [frågetjänstklienter](../clients/overview.md).

**API-format**

```http
GET /connection_parameters
```

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med dina anslutningsparametrar.

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
