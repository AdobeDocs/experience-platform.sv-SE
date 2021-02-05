---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;scheman;schema;api;API;
solution: Experience Platform
title: API-slutpunkt för scheman
topic: developer guide
description: Scheman är ett verktyg som kan användas för att automatiskt köra batchsegmenteringsjobb en gång om dagen.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 1%

---


# Slutpunkt för scheman

Scheman är ett verktyg som kan användas för att automatiskt köra batchsegmenteringsjobb en gång om dagen. Du kan använda slutpunkten `/config/schedules` för att hämta en lista med scheman, skapa ett nytt schema, hämta information om ett specifikt schema, uppdatera ett specifikt schema eller ta bort ett specifikt schema.

## Komma igång

Slutpunkterna som används i den här guiden ingår i [!DNL Adobe Experience Platform Segmentation Service]-API:t. Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med scheman {#retrieve-list}

Du kan hämta en lista över alla scheman för din IMS-organisation genom att göra en GET-förfrågan till `/config/schedules`-slutpunkten.

**API-format**

`/config/schedules`-slutpunkten har stöd för flera frågeparametrar som kan hjälpa dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader. Om du anropar den här slutpunkten utan parametrar hämtas alla scheman som är tillgängliga för din organisation. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{START}` | Anger vilken sida förskjutningen ska börja från. Som standard är det här värdet 0. |
| `{LIMIT}` | Anger antalet returnerade scheman. Som standard är det här värdet 100. |

**Begäran**

Följande begäran hämtar de tio senaste schemana som publicerats inom IMS-organisationen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över scheman för den angivna IMS-organisationen som JSON.

>[!NOTE]
>
>Följande svar har trunkerats för utrymme och visar endast det första schemat som returnerats.

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Egenskap | Beskrivning |
| -------- | ------------ |
| `_page.totalCount` | Det totala antalet returnerade scheman. |
| `_page.pageSize` | Sidstorleken för scheman. |
| `children.name` | Schemats namn som en sträng. |
| `children.type` | Typ av jobb som en sträng. De två typer som stöds är&quot;batch_segmentation&quot; och&quot;export&quot;. |
| `children.properties` | Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `children.properties.segments` | Om du använder `["*"]` säkerställs att alla segment inkluderas. |
| `children.schedule` | En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Mer information om cron-scheman finns i [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)-dokumentationen. I det här exemplet betyder &quot;0 0 1 * *&quot; att schemat kommer att köras vid midnatt den första i varje månad. |
| `children.state` | En sträng som innehåller schematillståndet. De två lägen som stöds är &quot;active&quot; och &quot;inactive&quot;. Som standard är läget inställt på &quot;inaktiv&quot;. |

## Skapa ett nytt schema {#create}

Du kan skapa ett nytt schema genom att göra en POST-förfrågan till `/config/schedules`-slutpunkten.

**API-format**

```http
POST /config/schedules
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Egenskap | Beskrivning |
| -------- | ------------ |
| `name` | **Obligatoriskt.** Schemats namn som en sträng. |
| `type` | **Obligatoriskt.** Typ av jobb som en sträng. De två typer som stöds är&quot;batch_segmentation&quot; och&quot;export&quot;. |
| `properties` | **Obligatoriskt.** Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `properties.segments` | **Obligatoriskt när  `type` är lika med&quot;batch_segmentation&quot;.** Med  `["*"]` säkerställs att alla segment ingår. |
| `schedule` | *Valfritt.* En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Mer information om cron-scheman finns i [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)-dokumentationen. I det här exemplet betyder &quot;0 0 1 * *&quot; att schemat kommer att köras vid midnatt den första i varje månad. <br><br>Om strängen inte anges genereras ett systemgenererat schema automatiskt. |
| `state` | *Valfritt.* En sträng som innehåller schematillståndet. De två lägen som stöds är &quot;active&quot; och &quot;inactive&quot;. Som standard är läget inställt på &quot;inaktiv&quot;. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade schema.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## Hämta ett specifikt schema {#get}

Du kan hämta detaljerad information om ett specifikt schema genom att göra en GET-begäran till `/config/schedules`-slutpunkten och ange ID:t för det schema som du vill hämta i sökvägen till begäran.

**API-format**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för schemat som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om det angivna schemat.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

| Egenskap | Beskrivning |
| -------- | ------------ |
| `name` | Schemats namn som en sträng. |
| `type` | Typ av jobb som en sträng. De två typer som stöds är `batch_segmentation` och `export`. |
| `properties` | Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `properties.segments` | Om du använder `["*"]` säkerställs att alla segment inkluderas. |
| `schedule` | En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Mer information om cron-scheman finns i [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)-dokumentationen. I det här exemplet betyder &quot;0 0 1 * *&quot; att schemat kommer att köras vid midnatt den första i varje månad. |
| `state` | En sträng som innehåller schematillståndet. De två lägen som stöds är `active` och `inactive`. Som standard är läget inställt på `inactive`. |

## Uppdatera information för ett specifikt schema {#update}

Du kan uppdatera ett specifikt schema genom att göra en PATCH-begäran till `/config/schedules`-slutpunkten och ange ID:t för det schema som du försöker uppdatera i sökvägen till begäran.

Med PATCH-begäran kan du uppdatera antingen [state](#update-state) eller [cron schedule](#update-schedule) för ett enskilt schema.

### Uppdatera schemastatus {#update-state}

Du kan använda en JSON-lagningsåtgärd för att uppdatera schemats status. Om du vill uppdatera läget deklarerar du egenskapen `path` som `/state` och anger `value` som antingen `active` eller `inactive`. Mer information om JSON Patch finns i [JSON Patch](http://jsonpatch.com/)-dokumentationen.

**API-format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för schemat som du vill uppdatera. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op": "add",
        "path": "/state",
        "value": "active"
    }
]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `path` | Sökvägen för det värde som du vill laga. I det här fallet måste du ange värdet `path` till /state eftersom du uppdaterar schemats tillstånd. |
| `value` | Det uppdaterade värdet för schemats tillstånd. Värdet kan antingen anges som aktivt eller inaktivt för att aktivera eller inaktivera schemat. |

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll).

### Uppdatera kundschemat {#update-schedule}

Du kan använda en JSON-korrigeringsåtgärd för att uppdatera kronschemat. Om du vill uppdatera schemat deklarerar du egenskapen `path` som `/schedule` och anger `value` som ett giltigt cron-schema. Mer information om JSON Patch finns i [JSON Patch](http://jsonpatch.com/)-dokumentationen. Mer information om cron-scheman finns i [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)-dokumentationen.

**API-format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för schemat som du vill uppdatera. |

**Begäran**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `path` | Sökvägen för det värde som du vill uppdatera. I det här fallet måste du ange `path` till `/schedule` eftersom du uppdaterar kronschemat. |
| `value` | Det uppdaterade värdet för cron-schemat. Värdet måste anges i form av ett kronschema. I det här exemplet körs schemat den andra varje månad. |

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll).

## Ta bort ett specifikt schema

Du kan begära att få ta bort ett specifikt schema genom att göra en DELETE-begäran till `/config/schedules`-slutpunkten och ange ID:t för det schema som du vill ta bort i sökvägen till begäran.

**API-format**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för schemat som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll).

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur scheman fungerar.