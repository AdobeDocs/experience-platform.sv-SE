---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: Handbok för frågetjänstutvecklare
topic: connection parameters
description: Du kan hämta anslutningsparametrar för användning av den interaktiva tjänsten genom att göra en GET-förfrågan till slutpunkten /connection_parameters.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Anslutningsparametrar

## Exempel på API-anrop

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till [!DNL Query Service] API:t. I följande avsnitt går du igenom de olika API-anropen som du kan göra med hjälp av [!DNL Query Service] API:t. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

### Begär anslutningsparametrar för den interaktiva tjänsten

Du kan hämta anslutningsparametrar för användning av den [interaktiva tjänsten](../creating-queries/writing-queries.md) genom att göra en GET-förfrågan till `/connection_parameters` slutpunkten. Mer information om klienter som använder anslutningsparametrar för att ansluta via den interaktiva tjänsten finns i dokumentationen om [Query Service-klienter](../clients/overview.md).

**API-format**

```http
GET /connection_parameters
```

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
