---
title: Anslut ditt Snowflake Streaming-konto till Adobe Experience Platform
description: Lär dig hur du ansluter Adobe Experience Platform till Snowflake Streaming med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: 34b1676ebb5405d73cf37cd786d1e6c26cb8fdaa
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# Strömma [!DNL Snowflake]-data till Experience Platform med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>
> Direktuppspelningskällan [!DNL Snowflake] är tillgänglig i API:t för användare som har köpt Real-time Customer Data Platform Ultimate.

I den här självstudien beskrivs hur du ansluter och direktuppspelar data från ditt [!DNL Snowflake]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) .

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

För nödvändig konfiguration och information om strömningskällan [!DNL Snowflake]. Läs översikten över den [[!DNL Snowflake] strömmande källan](../../../../connectors/databases/snowflake-streaming.md).

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning {#create-a-base-connection}

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina [!DNL Snowflake] autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Snowflake]:

>[!TIP]
>
>Värdet `auth.specName` måste anges exakt som exemplet nedan, inklusive blanksteg.

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
| `auth.params.account` | Namnet på ditt [!DNL Snowflake]-direktuppspelningskonto. |
| `auth.params.database` | Namnet på din [!DNL Snowflake]-databas från vilken data hämtas. |
| `auth.params.warehouse` | Namnet på ditt [!DNL Snowflake]-lagerställe. Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje lagerställe är oberoende av varandra och måste nås individuellt när data skickas till plattformen. |
| `auth.params.username` | Användarnamnet för ditt [!DNL Snowflake]-direktuppspelningskonto. |
| `auth.params.schema` | (Valfritt) Databasschemat som är associerat med ditt [!DNL Snowflake]-direktuppspelningskonto. |
| `auth.params.password` | Lösenordet för ditt [!DNL Snowflake]-direktuppspelningskonto. |
| `auth.params.role` | (Valfritt) Användarrollen för den här [!DNL Snowflake]-anslutningen. Om det inte anges används standardvärdet `public`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Snowflake]: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Svar**

Ett lyckat svar returnerar den nyskapade basanslutningen och dess motsvarande tagg.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Utforska era datatabeller {#explore-your-data-tables}

Använd sedan basanslutnings-ID:t för att utforska och navigera genom källans datatabeller genom att göra en GET-förfrågan till `/connections/{BASE_CONNECTION_ID}/explore?objectType=root`-slutpunkten och ange ditt grundläggande anslutnings-ID som en parameter.

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Basanslutnings-ID för strömningskällan [!DNL Snowflake]. |


**Begäran**

Följande begäran hämtar strukturen och innehållet i ditt [!DNL Snowflake]-direktuppspelningskonto.

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

Om du vill skapa en källanslutning skickar du en POST till `/sourceConnections`-slutpunkten för [!DNL Flow Service] API:t.

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
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `baseConnectionId` | Det autentiserade basanslutnings-ID:t för strömningskällan [!DNL Snowflake]. Detta ID genererades i ett tidigare steg. |
| `connectionSpec.id` | Anslutningens spec-ID för strömningskällan [!DNL Snowflake]. |
| `params.tableName` | Namnet på tabellen i din [!DNL Snowflake]-databas som du vill hämta till plattformen. |
| `params.timestampColumn` | Namnet på den tidsstämpelkolumn som ska användas för att hämta inkrementella värden. |
| `params.backfill` | En boolesk flagga som avgör om data hämtas från början (0 epok-tid) eller från den tidpunkt då källan initieras. Mer information om det här värdet finns i [[!DNL Snowflake] översikten över den direktuppspelade källan](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | Tidszonsvärdet anger vilken tidszonens aktuella tid som ska hämtas när [!DNL Snowflake]-databasen efterfrågas. Den här parametern ska anges om tidsstämpelkolumnen i konfigurationen är inställd på `TIMESTAMP_NTZ`. Om det inte anges används UTC som standard `timezoneValue`. |

**Svar**

Ett lyckat svar returnerar ditt källanslutnings-ID och dess motsvarande tagg. Källanslutnings-ID används i ett senare steg för att skapa ett dataflöde.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Skapa ett dataflöde

Om du vill skapa ett dataflöde för att strömma data från rundtur [!DNL Snowflake]-konto till plattformen måste du göra en POST-förfrågan till slutpunkten `/flows` och samtidigt ange följande värden:

>[!TIP]
>
>Följ länkarna nedan för att få stegvisa guider om hur du hämtar följande ID:n.

* [Source-anslutnings-ID](#create-a-source-connection)
* [Målanslutnings-ID](../../collect/database-nosql.md#create-a-target-connection)
* [Flödesspekt-ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [Mappnings-ID](../../collect/database-nosql.md#create-a-mapping)

**API-format**

```http
POST /flows
```

**Begäran**

Följande begäran skapar ett dataflöde för direktuppspelning för ditt [!DNL Snowflake]-konto.

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
| `sourceConnectionIds` | Källanslutnings-ID för strömningskällan [!DNL Snowflake]. |
| `targetConnectionIds` | Målanslutnings-ID för strömningskällan [!DNL Snowflake]. |
| `flowSpec.id` | Flödesspec-ID för att skapa ett dataflöde för en [!DNL Snowflake]-strömningskälla. Med det här flödets spec-ID kan du skapa ett direktuppspelat dataflöde med mappningsomvandlingar. Detta ID är fast och är: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
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

Genom att följa den här självstudiekursen har du skapat ett dataflöde för direktuppspelning för dina [!DNL Snowflake]-data med API:t [!DNL Flow Service]. Mer information om Adobe Experience Platform Sources finns i följande dokumentation:

* [Översikt över källor](../../../../home.md)
* [Övervaka dataflödet med API:er](../../monitor.md)
