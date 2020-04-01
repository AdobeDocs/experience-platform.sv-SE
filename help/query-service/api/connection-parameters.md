---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbok för frågetjänstutvecklare
topic: connection parameters
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Anslutningsparametrar

## Exempel på API-anrop

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till API:t för frågetjänsten. Följande avsnitt går igenom de olika API-anrop du kan göra med hjälp av API:t för frågetjänsten. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

### Begär anslutningsparametrar för den interaktiva tjänsten

Du kan hämta anslutningsparametrar för användning av den [interaktiva tjänsten](../creating-queries/writing-queries.md) genom att göra en GET-begäran till `/connection_parameters` slutpunkten. Mer information om klienter som använder anslutningsparametrar för att ansluta via den interaktiva tjänsten finns i dokumentationen om [Query Service-klienter](../clients/overview.md).

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
