---
title: Anslut ditt Snowflake Streaming-konto till Adobe Experience Platform
description: Lär dig hur du ansluter Adobe Experience Platform till Snowflake Streaming med API:t för Flow Service.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: 8bc232034301fa713f61bd3f11fbde122afcdcf9
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 1%

---

# Strömma [!DNL Snowflake] data till Experience Platform med [!DNL Flow Service] API

>[!IMPORTANT]
>
>* The [!DNL Snowflake] strömningskällan är i betaversion. Läs [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.
>* API-stöd för [!DNL Snowflake] strömningskälla är endast tillgänglig för kunder som har köpt Real-Time CDP Ultimate.


Den här självstudiekursen innehåller steg för hur du ansluter och direktuppspelar data från [!DNL Snowflake] till Adobe Experience Platform med [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

För nödvändig installation och information om [!DNL Snowflake] direktuppspelningskälla. Läs [[!DNL Snowflake] översikt över direktuppspelningskälla](../../../../connectors/databases/snowflake-streaming.md).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning {#create-a-base-connection}

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Snowflake] autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Snowflake]:

>[!TIP]
>
>The `auth.specName` värdet måste anges exakt som exemplet nedan, inklusive blanksteg.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.account` | Namnet på [!DNL Snowflake] direktuppspelningskonto. |
| `auth.params.database` | Namnet på [!DNL Snowflake] databas från vilken data hämtas. |
| `auth.params.warehouse` | Namnet på [!DNL Snowflake] lagerställe. The [!DNL Snowflake] dist.lager hanterar frågekörningsprocessen för programmet. Varje lagerställe är oberoende av varandra och måste nås individuellt när data skickas till plattformen. |
| `auth.params.username` | Användarnamnet för [!DNL Snowflake] direktuppspelningskonto. |
| `auth.params.schema` | (Valfritt) Databasschemat som är associerat med din [!DNL Snowflake] direktuppspelningskonto. |
| `auth.params.password` | Lösenordet för [!DNL Snowflake] direktuppspelningskonto. |
| `auth.params.role` | (Valfritt) Användarens roll för detta [!DNL Snowflake] anslutning. Om det inte anges används standardvärdet `public`. |
| `connectionSpec.id` | The [!DNL Snowflake] anslutningsspecifikation-ID: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Svar**

Ett lyckat svar returnerar den nyskapade basanslutningen och dess motsvarande tagg.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Utforska era datatabeller {#explore-your-data-tables}

Använd sedan basanslutnings-ID:t för att utforska och navigera i källans datatabeller genom att göra en GET-förfrågan till `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` slutpunkt när du anger ditt basanslutnings-ID som parameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Basanslutnings-ID för din [!DNL Snowflake] direktuppspelningskälla. |


**Begäran**

Följande begäran hämtar strukturen och innehållet i din [!DNL Snowflake] direktuppspelningskonto.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar strukturen och innehållet i källans data på rotnivå.

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `items.type` | Tabellens typ. |
| `items.names` | Tabellens namn. |

## Skapa en källanslutning {#create-a-source-connection}

En källanslutning skapar och hanterar anslutningen till den externa källan som data importeras från.

Om du vill skapa en källanslutning skickar du en POST till `/sourceConnections` slutpunkt för [!DNL Flow Service] API.

**API-format**

```http
POST /sourceConnections
```

**Begäran**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `baseConnectionId` | Det autentiserade basanslutnings-ID:t för din [!DNL Snowflake] direktuppspelningskälla. Detta ID genererades i ett tidigare steg. |
| `connectionSpec.id` | Anslutningens spec-ID för [!DNL Snowflake] direktuppspelningskälla. |
| `params.tableName` | Namnet på tabellen i [!DNL Snowflake] databas som du vill ta med till plattformen. |
| `params.timestampColumn` | Namnet på den tidsstämpelkolumn som ska användas för att hämta inkrementella värden. |
| `params.backfill` | En boolesk flagga som avgör om data hämtas från början (0 epok-tid) eller från den tidpunkt då källan initieras. Mer information om det här värdet finns i [[!DNL Snowflake] översikt över direktuppspelningskälla](../../../../connectors/databases/snowflake-streaming.md). |

**Svar**

Ett lyckat svar returnerar ditt källanslutnings-ID och dess motsvarande tagg. Källanslutnings-ID används i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Skapa ett dataflöde

Skapa ett dataflöde för att strömma data från en rundtur [!DNL Snowflake] konto till Platform måste du göra en POST-förfrågan till `/flows` slutpunkt med följande värden:

>[!TIP]
>
>Följ länkarna nedan för att få stegvisa guider om hur du hämtar följande ID:n.

* [Källanslutnings-ID](#create-a-source-connection)
* [Målanslutnings-ID](../../collect/database-nosql.md#create-a-target-connection)
* [Flödesspekt-ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [Mappnings-ID](../../collect/database-nosql.md#create-a-mapping)

**API-format**

```http
POST /flows
```

**Begäran**

Följande begäran skapar ett strömmande dataflöde för [!DNL Snowflake] konto.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `sourceConnectionIds` | Källanslutnings-ID för din [!DNL Snowflake] direktuppspelningskälla. |
| `targetConnectionIds` | Målanslutnings-ID för din [!DNL Snowflake] direktuppspelningskälla. |
| `flowSpec.id` | Flödesspecifikation-ID för att skapa ett dataflöde för [!DNL Snowflake] direktuppspelningskälla. Med det här flödets spec-ID kan du skapa ett direktuppspelat dataflöde med mappningsomvandlingar. Detta ID är fast och är: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | Mappnings-ID för dataflödet. |

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och dess motsvarande tagg.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för direktuppspelning för [!DNL Snowflake] data med [!DNL Flow Service] API. Mer information om Adobe Experience Platform Sources finns i följande dokumentation:

* [Översikt över källor](../../../../home.md)
* [Övervaka dataflödet med API:er](../../monitor.md)