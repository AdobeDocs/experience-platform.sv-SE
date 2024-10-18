---
title: Uppdatera dataflöden med API:t för Flow Service
description: Lär dig hur du skapar ett dataflöde, inklusive dess namn, beskrivning och schema, med API:t för Flow Service.
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: 9e1edaa4183a8025b8391f58d480063adc834616
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Uppdatera dataflöden med API:t för Flow Service

I den här självstudiekursen beskrivs stegen för att uppdatera ett dataflöde, inklusive dess grundläggande information, schema och mappningsuppsättningar med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!TIP]
>
>Källanslutningen och målanslutningen bör mappas till ett enda dataflöde. Du bör inte uppdatera käll- och målanslutningarna separat eftersom ändringarna inte återspeglas i deras motsvarande dataflöde. Om ditt användningsfall kräver en uppdatering av käll- och målanslutningarna måste du skapa ett nytt par käll- och målanslutningar samt ett nytt dataflöde.

## Komma igång

Den här självstudiekursen kräver att du har ett giltigt flödes-ID. Om du inte har ett giltigt flödes-ID väljer du den önskade anslutningen i [källöversikten](../../home.md) och följer instruktionerna innan du provar den här självstudien.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Söka efter dataflödesdetaljer

Det första steget i att uppdatera dataflödet är att hämta dataflödesinformation med ditt flödes-ID. Du kan visa den aktuella informationen om ett befintligt dataflöde genom att göra en GET-förfrågan till slutpunkten `/flows`.

**API-format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Det unika `id`-värdet för dataflödet som du vill hämta. |

**Begäran**

Följande begäran hämtar uppdaterad information om ditt flödes-ID.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar aktuell information om dataflödet, inklusive version, schema och unik identifierare (`id`).

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## Uppdatera dataflöde

Om du vill uppdatera ditt dataflödes körningsschema, namn och beskrivning utför du en PATCH-begäran till [!DNL Flow Service]-API:t och anger ditt flödes-ID, version och det nya schema som du vill använda.

>[!IMPORTANT]
>
>Rubriken `If-Match` krävs när du gör en PATCH-begäran. Värdet för den här rubriken är den unika versionen av anslutningen som du vill uppdatera. Värdet för etag uppdateras med varje lyckad uppdatering av ett dataflöde.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäran uppdaterar ditt flödeskörningsschema samt dataflödets namn och beskrivning.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "Database Dataflow Feb2021"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Database dataflow for testing update API"
            }
        ]'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `op` | Åtgärdsanropet som används för att definiera den åtgärd som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace` och `remove`. |
| `path` | Definierar den del av flödet som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till API:t [!DNL Flow Service], samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Uppdatera mappning

Du kan uppdatera mappningsuppsättningen för ett befintligt dataflöde genom att göra en PATCH-begäran till [!DNL Flow Service]-API:t och tillhandahålla uppdaterade värden för `mappingId` och `mappingVersion`.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäran uppdaterar mappningsuppsättningen för ditt dataflöde.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
    -d '[
        {
            "op": "replace",
            "path": "/transformations/0",
            "value": {
                "name": "Mapping",
                "params": {
                    "mappingId": "c5f22f04e09f44498e528901546a83b1",
                    "mappingVersion": 2
                }
            }
        }
    ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `op` | Åtgärdsanropet som används för att definiera den åtgärd som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace` och `remove`. |
| `path` | Definierar den del av flödet som ska uppdateras. I det här exemplet uppdateras `transformations`. |
| `value.name` | Namnet på den egenskap som ska uppdateras. |
| `value.params.mappingId` | Det nya mappnings-ID som ska användas för att uppdatera dataflödets mappningsuppsättning. |
| `value.params.mappingVersion` | Den nya mappningsversionen som är associerad med det uppdaterade mappnings-ID:t. |

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-förfrågan till API:t [!DNL Flow Service], samtidigt som du anger ditt flödes-ID.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du uppdaterat grundläggande information, scheman och mappningsuppsättningar för ditt dataflöde med API:t [!DNL Flow Service]. Mer information om hur du använder källanslutningar finns i [källans översikt](../../home.md).
