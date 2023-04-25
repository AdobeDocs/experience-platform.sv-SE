---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;Flödestjänst-API;källor;Källor
title: Filtrera radnivådata för en källa med API:t för flödestjänsten
description: I den här självstudiekursen beskrivs hur du filtrerar data på källnivå med API:t för Flow Service
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: da6f5a79b1ee16fb0d44a5c2990ed1b8be1f99e2
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---

# Filtrera radnivådata för en källa med [!DNL Flow Service] API

>[!IMPORTANT]
>
>Stöd för filtrering av data på radnivå är för närvarande bara tillgängligt för följande källor:
>
>* [Google BigQuery](../../connectors/databases/bigquery.md)
>* [Microsoft Dynamics](../../connectors/crm/ms-dynamics.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Salesforce Marketing Cloud](../../connectors/marketing-automation/salesforce-marketing-cloud.md)
>* [Snowflake](../../connectors/databases/snowflake.md)


I den här självstudien beskrivs hur du filtrerar radnivådata för en källa med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Filtrera källdata

Följande textkonturer används för att filtrera radnivådata för källan.

### Söka efter anslutningsspecifikationer

Innan du kan använda API:t för att filtrera data på radnivå för en källa måste du först hämta källans anslutningsinformation för att kunna avgöra vilka operatorer och språk som stöds av en viss källa.

Om du vill hämta en viss källas anslutningsspecifikation skickar du en GET-begäran till `/connectionSpecs` slutpunkt för [!DNL Flow Service] API när du anger källans egenskapsnamn som en del av frågeparametrarna.

**API-format**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMS}` | De valfria frågeparametrarna som resultaten ska filtreras efter. Du kan hämta [!DNL Google BigQuery] anslutningsspecifikation genom att använda `name` egenskap och ange `"google-big-query"` i sökningen. |

**Begäran**

Följande begäran hämtar anslutningsspecifikationer för [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar anslutningsspecifikationerna för [!DNL Google BigQuery], inklusive information om vilka frågespråk som stöds och logiska operatorer.

>[!NOTE]
>
>API-svaret nedan är förkortat.

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes.filterAtSource.enabled` | Avgör om den efterfrågade källan stöder filtrering för radnivådata. |
| `attributes.filterAtSource.queryLanguage` | Bestämmer vilket frågespråk som den frågade källan stöder. |
| `attributes.filterAtSource.logicalOperators` | Avgör de logiska operatorer som du kan använda för att filtrera radnivådata för källan. |
| `attributes.filterAtSource.comparisonOperators` | Bestämmer jämförelseoperatorer som du kan använda för att filtrera radnivådata för källan. Se tabellen nedan för mer information om jämförelseoperatorer. |
| `attributes.filterAtSource.columnNameEscapeChar` | Anger vilket tecken som ska användas för att undvika kolumner. |
| `attributes.filterAtSource.valueEscapeChar` | Anger hur värden ska omges när en SQL-fråga skrivs. |

{style="table-layout:auto"}

#### Jämförelseoperatörer

| Operatör | Beskrivning |
| --- | --- |
| `==` | Filtrerar efter om egenskapen är lika med det angivna värdet. |
| `!=` | Filtrerar efter om egenskapen inte är lika med det angivna värdet. |
| `<` | Filtrerar efter om egenskapen är mindre än det angivna värdet. |
| `>` | Filtrerar efter om egenskapen är större än det angivna värdet. |
| `<=` | Filtrerar efter om egenskapen är mindre än eller lika med det angivna värdet. |
| `>=` | Filtrerar efter om egenskapen är större än eller lika med det angivna värdet. |
| `like` | Filtrera genom att använda i en `WHERE` -sats för att söka efter ett angivet mönster. |
| `in` | Filtrerar efter om egenskapen ligger inom ett angivet intervall. |

{style="table-layout:auto"}

### Ange filtervillkor för förtäring

När du har identifierat de logiska operatorerna och frågespråket som stöds av källan kan du använda PQL (Profile Query Language) för att ange de filtreringsvillkor som du vill tillämpa på källdata.

I exemplet nedan används villkor bara för att markera data som är lika med de angivna värdena för de nodtyper som anges som parametrar.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### Förhandsgranska data

Du kan förhandsgranska dina data genom att göra en GET-förfrågan till `/explore` slutpunkt för [!DNL Flow Service] API:n ger `filters` som en del av frågeparametrarna och specificera PQL-indatavillkoren i [!DNL Base64].

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Källans grundläggande anslutnings-ID. |
| `{TABLE_PATH}` | Egenskapen path för den tabell som du vill inspektera. |
| `{FILTERS}` | Dina PQL-filtreringsvillkor kodade i [!DNL Base64]. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

En slutförd begäran returnerar följande svar.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### Skapa en källanslutning för filtrerade data

Om du vill skapa en källanslutning och importera filtrerade data skickar du en POST till `/sourceConnections` slutpunkten samtidigt som du anger filtervillkoren som en del av innehållsparametrarna.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

Följande begäran skapar en källanslutning för att importera data från `test1.fasTestTable` där `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Bilaga

Det här avsnittet innehåller ytterligare exempel på olika nyttolaster för filtrering.

### Singulvillkor

Du kan utesluta den ursprungliga `fnApply` för scenarier som bara kräver ett villkor.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### Använda `in` operator

Se exempelnyttolasten nedan för ett exempel på operatorn `in`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### Använda `isNull` operator

Se exempelnyttolasten nedan för ett exempel på operatorn `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### Använda `NOT` operator

Se exempelnyttolasten nedan för ett exempel på operatorn `NOT`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### Exempel med kapslade villkor

Se exempelnyttolasten nedan för ett exempel på komplexa kapslade villkor.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
