---
title: Slutpunkt för accelererade frågor
description: Lär dig hur du får åtkomst till frågeflödat arkiv på ett tillståndslöst sätt för att snabbt returnera resultat baserat på aggregerade data. Det här dokumentet innehåller ett exempel på HTTP-begäran och svar för frågetjänstens accelererade frågeslutpunkt.
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: 037ea8d11bb94e3b4f71ea301a535677b3cccdbd
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Slutpunkt för accelererade frågor

Som en del av Data Distiller SKU [API för frågetjänst](https://developer.adobe.com/experience-platform-apis/references/query-service/) gör att du kan ställa tillståndslösa frågor till det accelererade arkivet. De returnerade resultaten baseras på aggregerade data. Den försämrade tidsfördröjningen för resultaten möjliggör ett mer interaktivt informationsutbyte. API:erna för accelererade frågor används också för att driva [användardefinierade kontrollpaneler](../../dashboards/user-defined-dashboards.md).

Innan du fortsätter med den här handboken bör du kontrollera att du har läst och förstått [API-guide för frågetjänst](./getting-started.md) för att kunna använda API:t för frågetjänsten.

## Komma igång

Data Distiller SKU krävs för att använda det frågeaccelererade arkivet. Se [packning](../packaging.md) och [skyddsräcken](../guardrails.md#query-accelerated-store)och [licensiering](../data-distiller/license-usage.md) dokumentation som relaterar till Data Distiller SKU. Om du inte har Data Distiller SKU kontaktar du Adobe kundtjänstrepresentanten för mer information.

I följande avsnitt beskrivs de API-anrop som krävs för att komma åt det frågeaccelererade arkivet på ett tillståndslöst sätt via API:t för frågetjänsten. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

## Kör en accelererad fråga {#run-accelerated-query}

Gör en förfrågan om POST till `/accelerated-queries` slutpunkt för att köra en accelererad fråga. Frågan finns antingen direkt i nyttolasten eller refereras till med ett mall-ID.

**API-format**

```shell
POST /accelerated-queries
```

### Begäran

>[!IMPORTANT]
>
>Begäranden till `/accelerated-queries` slutpunkten kräver antingen en SQL-sats ELLER ett mall-ID, men inte båda. Om du skickar båda i en begäran uppstår ett fel.

Följande begäran skickar en SQL-fråga i begärandetexten till det accelererade arkivet.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

Den här alternativa begäran skickar ett mall-ID i begärandetexten till det accelererade arkivet. SQL från motsvarande mall används för att fråga efter det accelererade arkivet.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| Egenskap | Beskrivning |
|---|---|
| `dbName` | Namnet på databasen som du gör en accelererad fråga till. Värdet för `dbName` bör ha formatet `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. Den angivna databasen måste finnas i det accelererade arkivet, annars genereras ett fel. Du måste också se till att `x-sandbox-name` rubrik och sandlådenamn i `dbName` referera till samma sandlåda. |
| `sql` | En SQL-satsträng. Den största tillåtna storleken är 100000 tecken. |
| `templateId` | Den unika identifieraren för en fråga som skapats och sparats som en mall när en begäran om POST görs till `/templates` slutpunkt. |
| `name` | Ett valfritt användarvänligt beskrivande namn för den accelererade frågan. |
| `description` | En valfri kommentar om syftet med frågan för att hjälpa andra användare förstå syftet. Den största tillåtna storleken är 1 000 byte. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med ad hoc-schemat som skapats av frågan.

>[!NOTE]
>
>Följande svar har trunkerats för att vara kortfattat.

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| Egenskap | Beskrivning |
|---|---|
| `queryId` | ID-värdet för frågan som skapades. |
| `resultsMeta` | Det här objektet innehåller metadata för varje kolumn som returneras i resultat, så att användarna vet namnet och typen för varje kolumn. |
| `resultsMeta._adhoc` | Ett XDM-schema (ad hoc Experience Data Model) med fält som bara namnges av en enda datauppsättning. |
| `resultsMeta._adhoc.type` | Datatypen för ad hoc-schemat. |
| `resultsMeta._adhoc.meta:xdmType` | Detta är ett systemgenererat värde för XDM-fälttypen. Mer information om tillgängliga typer finns i dokumentationen om [tillgängliga XDM-typer](../../xdm/tutorials/custom-fields-api.md). |
| `resultsMeta._adhoc.properties` | Detta är kolumnnamnen för den efterfrågade datauppsättningen. |
| `resultsMeta._adhoc.results` | Detta är radnamnen för den efterfrågade datauppsättningen. De återspeglar var och en av de returnerade kolumnerna. |
