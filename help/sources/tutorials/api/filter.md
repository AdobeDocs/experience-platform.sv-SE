---
title: Filtrera radnivådata för en Source med API:t för flödestjänsten
description: I den här självstudiekursen beskrivs hur du filtrerar data på källnivå med API:t för Flow Service
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: 67abd5cda9cff1da8757ef691ebbf27e9a5550c5
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 2%

---

# Filtrera radnivådata för en källa med API:t [!DNL Flow Service]

>[!AVAILABILITY]
>
>Stöd för filtrering av data på radnivå är för närvarande bara tillgängligt för följande källor:
>
>* [[Amazon Redshift]](../../connectors/databases/redshift.md)
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Marketo Engage] standardaktiviteter](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

Läs den här guiden för steg om hur du filtrerar radnivådata för en källa med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Kom igång

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../landing/api-guide.md).

## Filtrera källdata {#filter-source-data}

Följande textkonturer används för att filtrera radnivådata för källan.

### Hämta dina anslutningsspecifikationer {#retrieve-your-connection-specs}

Det första steget för att filtrera data på radnivå för källan är att hämta källans anslutningsspecifikationer och avgöra vilka operatorer och språk som stöds av källan.

Om du vill hämta en viss källas anslutningsspecifikation gör du en GET-begäran till `/connectionSpecs`-slutpunkten för [!DNL Flow Service]-API:t och anger egenskapsnamnet för källan som en del av frågeparametrarna.

**API-format**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMS}` | De valfria frågeparametrarna som resultaten ska filtreras efter. Du kan hämta anslutningsspecifikationen [!DNL Google BigQuery] genom att använda egenskapen `name` och ange `"google-big-query"` i sökningen. |

+++Begäran

Följande begäran hämtar anslutningsspecifikationerna för [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++svar

Ett lyckat svar returnerar statuskoden 200 och anslutningsspecifikationerna för [!DNL Google BigQuery], inklusive information om dess frågespråk och logiska operatorer som stöds.

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

+++

#### Jämförelseoperatorer {#comparison-operators}

| Operatör | Beskrivning |
| --- | --- |
| `==` | Filtrerar efter om egenskapen är lika med det angivna värdet. |
| `!=` | Filtrerar efter om egenskapen inte är lika med det angivna värdet. |
| `<` | Filtrerar efter om egenskapen är mindre än det angivna värdet. |
| `>` | Filtrerar efter om egenskapen är större än det angivna värdet. |
| `<=` | Filtrerar efter om egenskapen är mindre än eller lika med det angivna värdet. |
| `>=` | Filtrerar efter om egenskapen är större än eller lika med det angivna värdet. |
| `like` | Filtrerar genom att användas i en `WHERE`-sats för att söka efter ett angivet mönster. |
| `in` | Filtrerar efter om egenskapen ligger inom ett angivet intervall. |

{style="table-layout:auto"}

### Ange filtervillkor för förtäring {#specify-filtering-conditions-for-ingestion}

När du har identifierat de logiska operatorerna och frågespråket som din källa stöder kan du använda Profile Query Language (PQL) för att ange de filtreringsvillkor som du vill tillämpa på dina källdata.

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

### Förhandsgranska data {#preview-your-data}

Du kan förhandsgranska dina data genom att göra en GET-begäran till `/explore`-slutpunkten för [!DNL Flow Service] API:t, samtidigt som du anger `filters` som en del av frågeparametrarna och anger dina PQL-indatavillkor i [!DNL Base64].

**API-format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Källans grundläggande anslutnings-ID. |
| `{TABLE_PATH}` | Egenskapen path för den tabell som du vill inspektera. |
| `{FILTERS}` | Dina PQL-filtreringsvillkor kodade i [!DNL Base64]. |

+++Begäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++svar

Ett lyckat svar returnerar innehållet och strukturen för dina data.

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

+++

### Skapa en källanslutning för filtrerade data

Om du vill skapa en källanslutning och importera filtrerade data skapar du en POST-begäran till `/sourceConnections`-slutpunkten och anger filtervillkoren i parametrarna för begärandeinnehållet.

**API-format**

```http
POST /sourceConnections
```

+++Begäran

Följande begäran skapar en källanslutning för import av data från `test1.fasTestTable` där `city` = `DDN`.

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

+++

+++svar

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade källanslutningen.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## Filtrera aktivitetsenheter för [!DNL Marketo Engage] {#filter-for-marketo}

Du kan använda filtrering på radnivå för att filtrera efter aktivitetsenheter när du använder [[!DNL Marketo Engage] källkopplingen](../../connectors/adobe-applications/marketo/marketo.md). För närvarande kan du bara filtrera efter aktivitetsenheter och standardaktivitetstyper. Anpassade aktiviteter styrs fortfarande under [[!DNL Marketo] fältmappningar](../../connectors/adobe-applications/mapping/marketo.md).

### [!DNL Marketo] standardaktivitetstyper {#marketo-standard-activity-types}

Följande tabell visar standardaktivitetstyperna för [!DNL Marketo]. Använd den här tabellen som referens för filtervillkoren.

| ID för aktivitetstyp | Namn på aktivitetstyp |
| --- | --- |
| 1 | Besök webbsidan |
| 2 | Fyll i formulär |
| 3 | Klicka på Länk |
| 6 | Skicka e-post |
| 7 | E-post levererad |
| 8 | E-post studsade |
| 9 | Avbeställ e-post |
| 10 | Öppna e-post |
| 11 | Klicka på E-post |
| 12 | Nytt lead |
| 21 | Konvertera lead |
| 22 | Ändra poäng |
| 24 | Lägg till i listan |
| 25 | Ta bort från lista |
| 27 | Mjuk e-poststudsning |
| 32 | Sammanfoga leads |
| 34 | Lägg till i affärsmöjlighet |
| 35 | Ta bort från affärsmöjlighet |
| 36 | Uppdatera affärsmöjlighet |
| 46 | Intressant stund |
| 101 | Ändra intäktsfas |
| 104 | Ändra status i progression |
| 110 | Ring webkrok |
| 113 | Lägg till i struktur |
| 114 | Ändra strukturspår |
| 115 | Ändra vårdnad |

{style="table-layout:auto"}

Följ stegen nedan för att filtrera standardenheter för aktivitet när du använder [!DNL Marketo]-källkopplingen.

### Skapa ett utkast till dataflöde

Skapa först ett [[!DNL Marketo] dataflöde](../ui/create/adobe-applications/marketo.md) och spara det som ett utkast. Mer information om hur du skapar ett utkast till dataflöde finns i följande dokumentation:

* [Spara ett dataflöde som ett utkast med användargränssnittet](../ui/draft.md)
* [Spara ett dataflöde som ett utkast med API:t](../api/draft.md)

### Hämta ditt dataflödes-ID

När du har ett utkast till dataflöde måste du hämta dess motsvarande ID.

Gå till källkatalogen i användargränssnittet och välj sedan **[!UICONTROL Dataflows]** i den övre rubriken. Använd statuskolumnen för att identifiera alla dataflöden som har sparats i utkastläge och välj sedan dataflödets namn. Använd sedan panelen **[!UICONTROL Properties]** till höger för att hitta ditt dataflöde-ID.

### Hämta dataflödesinformation

Därefter måste du hämta dataflödesinformationen, särskilt källanslutnings-ID:t som är kopplat till dataflödet. Om du vill hämta information om dataflödet skickar du en GET-begäran till slutpunkten `/flows` och anger ditt dataflödes-ID som en sökvägsparameter.

**API-format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{FLOW_ID}` | ID:t för det dataflöde som du vill hämta. |

+++Begäran

Följande begäran hämtar information om dataflödes-ID: `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++svar

Ett lyckat svar returnerar dina dataflödesdetaljer, inklusive information om dess motsvarande käll- och målanslutningar. Du måste tänka på ditt käll- och målanslutnings-ID, eftersom dessa värden krävs senare, för att kunna publicera dataflödet.

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### Hämta din källanslutningsinformation

Använd sedan ditt källanslutnings-ID och gör en GET-begäran till slutpunkten `/sourceConnections` för att hämta din källanslutningsinformation.

**API-format**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | ID för den källanslutning som du vill hämta. |

+++Begäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++svar

Ett lyckat svar returnerar information om din källanslutning. Notera versionen eftersom du behöver det här värdet i nästa steg för att kunna uppdatera din källanslutning.

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### Uppdatera din källanslutning med filtervillkor

Nu när du har ditt källanslutnings-ID och dess motsvarande version kan du göra en PATCH-begäran med filtervillkoren som anger dina standardaktivitetstyper.

Om du vill uppdatera din källanslutning gör du en PATCH-begäran till `/sourceConnections`-slutpunkten och anger ditt källanslutnings-ID som en frågeparameter. Dessutom måste du ange en `If-Match`-huvudparameter med motsvarande version av källanslutningen.

>[!TIP]
>
>Huvudet `If-Match` krävs när en PATCH-begäran görs. Värdet för den här rubriken är den unika versionen/taggen för det dataflöde som du vill uppdatera. Versions-/etag-värdet uppdateras med varje lyckad uppdatering av ett dataflöde.

**API-format**

```http
PATCH /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | ID:t för den källanslutning som du vill uppdatera |

+++Begäran

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++svar

Ett lyckat svar returnerar ditt källanslutnings-ID och -tagg (version).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### Publicera din källanslutning

När källanslutningen har uppdaterats med filtervillkoren kan du nu gå vidare från utkastläget och publicera källanslutningen. Om du vill göra det skickar du en POST-begäran till `/sourceConnections`-slutpunkten och anger ID:t för din utkastkällanslutning samt en åtgärd för publicering.

**API-format**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parameter | Beskrivning |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | ID för den källanslutning som du vill publicera. |
| `op` | En åtgärd som uppdaterar tillståndet för den efterfrågade källanslutningen. Om du vill publicera en utkastskällanslutning anger du `op` till `publish`. |

+++Begäran

Följande begäran publicerar en kopplad källanslutning.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++svar

Ett lyckat svar returnerar ditt källanslutnings-ID och -tagg (version).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### Publicera målanslutningen

På samma sätt som i föregående steg måste du även publicera målanslutningen för att kunna fortsätta och publicera ditt utkast till dataflöde. Gör en POST-begäran till `/targetConnections`-slutpunkten och ange ID:t för den utkastmålanslutning som du vill publicera samt en åtgärd för publicering.

**API-format**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parameter | Beskrivning |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | ID:t för målanslutningen som du vill publicera. |
| `op` | En åtgärd som uppdaterar tillståndet för den efterfrågade målanslutningen. Om du vill publicera ett utkast till målanslutning anger du `op` till `publish`. |

+++Begäran

Följande begäran publicerar målanslutningen med ID: `7e53e6e8-b432-4134-bb29-21fc6e8532e5`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++svar

Ett lyckat svar returnerar ID:t och motsvarande tagg för den publicerade målanslutningen.

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### Publicera dataflödet

Med både käll- och målanslutningarna publicerade kan du nu fortsätta till det sista steget och publicera ditt dataflöde. Om du vill publicera ditt dataflöde gör du en POST-begäran till `/flows`-slutpunkten och anger ditt dataflödes-ID och en åtgärd för publicering.

**API-format**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parameter | Beskrivning |
| --- | --- |
| `{FLOW_ID}` | ID för det dataflöde som du vill publicera. |
| `op` | En åtgärd som uppdaterar tillståndet för det efterfrågade dataflödet. Om du vill publicera ett dataflöde för utkast anger du `op` till `publish`. |

+++Begäran

Följande begäran publicerar ditt utkast till dataflöde.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++svar

Ett lyckat svar returnerar ID:t och motsvarande `etag` i dataflödet.

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

Du kan använda användargränssnittet i Experience Platform för att verifiera att dataflödet i utkastet har publicerats. Navigera till dataflödessidan i källkatalogen och referera till **[!UICONTROL Status]** i dataflödet. Om det lyckas bör statusen nu anges till **Aktiverad**.

>[!TIP]
>
>* Ett dataflöde med filtrering aktiverat fylls bara i i bakgrunden en gång. Alla ändringar i filtervillkoren (vare sig det är ett tillägg eller en borttagning) kan bara börja gälla för inkrementella data.
>* Om du behöver importera historiska data för nya aktivitetstyper rekommenderar vi att du skapar ett nytt dataflöde och definierar filtervillkoren med lämpliga aktivitetstyper i filtervillkoret.
>* Du kan inte filtrera anpassade aktivitetstyper.
>* Du kan inte förhandsgranska filtrerade data.

## Bilaga

Det här avsnittet innehåller ytterligare exempel på olika nyttolaster för filtrering.

### Enkelt villkor

Du kan utelämna den ursprungliga `fnApply` för scenarier som bara kräver ett villkor.

+++Markera för att visa exempel

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

+++

### Använda operatorn `in`

Se exempelnyttolasten nedan för ett exempel på operatorn `in`.

+++Markera för att visa exempel

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

+++

### Använda operatorn `isNull`

+++Markera för att visa exempel

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

+++

### Använda operatorn `NOT`

Se exempelnyttolasten nedan för ett exempel på operatorn `NOT`.


+++Markera för att visa exempel

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

+++

### Exempel med kapslade villkor

Se exempelnyttolasten nedan för ett exempel på komplexa kapslade villkor.

+++Markera för att visa exempel

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

+++