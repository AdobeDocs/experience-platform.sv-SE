---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Scheman
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Utvecklarhandbok för scheman

intro

- Hämta en lista med scheman
- Skapa ett nytt schema
- Hämta ett specifikt schema
- Uppdatera ett specifikt schema
- Ta bort ett specifikt schema

## Komma igång

API-slutpunkterna som används i den här guiden ingår i segmenterings-API:t. Läs utvecklarhandboken för [segmentering innan du fortsätter](./getting-started.md).

Avsnittet [](./getting-started.md#getting-started) Komma igång i utvecklarhandboken för segmentering innehåller länkar till relaterade ämnen, en guide till hur du läser exempelanropen för API i dokumentet och viktig information om vilka huvuden som krävs för att anropa något Experience Platform-API.

## Hämta en lista med scheman

Du kan hämta en lista över alla scheman för din IMS-organisation genom att göra en GET-begäran till `/config/schedules` slutpunkten.

**API-format**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Valfritt*) Parametrar har lagts till i sökvägen för begäran som konfigurerar resultaten som returneras i svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`). De tillgängliga parametrarna visas nedan.

**Frågeparametrar**

Nedan följer en lista över tillgängliga frågeparametrar för att lista scheman. Alla dessa parametrar är valfria. Om du anropar den här slutpunkten utan parametrar hämtas alla scheman som är tillgängliga för din organisation.

| Parameter | Beskrivning |
| --------- | ----------- |
| `start` | Anger vilken sida förskjutningen ska börja från. Som standard är det här värdet 0. |
| `limit` | Anger antalet returnerade scheman. Som standard är det här värdet 100. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över scheman för den angivna IMS-organisationen som JSON.

```json
{
    "_page": {
        "totalCount": 1,
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

## Skapa ett nytt schema

Du kan skapa ett nytt schema genom att göra en POST-begäran till `/config/schedules` slutpunkten.

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
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| Parameter | Beskrivning |
| --------- | ------------ |
| `name` | **Obligatoriskt.** Schemats namn som en sträng. |
| `type` | **Obligatoriskt.** Typ av jobb som en sträng. De två typerna som stöds är `batch_segmentation` och `export`. |
| `properties` | **Obligatoriskt.** Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `properties.segments` | **Krävs när`type`är lika med`batch_segmentation`.** Om du använder `["*"]` säkerställs att alla segment ingår. |
| `schedule` | **Obligatoriskt.** En sträng som innehåller jobbschemat. Mer information om cron-scheman finns i [dokumentationen för cron-uttrycksformat](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . I det här exemplet betyder &quot;0 0 1 * *&quot; att schemat kommer att köras vid midnatt den första i varje månad. |
| `state` | *Valfritt.* En sträng som innehåller schematillståndet. De två lägen som stöds är `active` och `inactive`. Som standard är läget inställt på `inactive`. |

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

## Hämta ett specifikt schema

Du kan hämta detaljerad information om ett specifikt schema genom att göra en GET-begäran till `/config/schedules` slutpunkten och ange schemats `id` värde i sökvägen för begäran.

**API-format**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Värdet `id` för schemat som du vill hämta.

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
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
```

## Uppdatera information om ett specifikt schema

Du kan uppdatera ett angivet schema genom att göra en PATCH-begäran till `/config/schedules` slutpunkten och ange schemats `id` värde i sökvägen för begäran.

PATCH-begäran stöder två olika sökvägar: `/state` och `/schedule`.

### Uppdatera schematillstånd

Du kan använda `/state` för att uppdatera schemats status - AKTIVT eller INAKTIVT. Om du vill uppdatera läget måste du ange värdet som `active` eller `inactive`.

**API-format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Värdet `id` för schemat som du vill uppdatera.

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
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
]
'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `path` | Sökvägen för det värde som du vill laga. I det här fallet måste du ange värdet för `path` till `/state`eftersom du uppdaterar schemats tillstånd. |
| `value` | Det uppdaterade värdet för `/state`filen. Värdet kan antingen anges som `active` eller `inactive` för att aktivera eller inaktivera schemat. |

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll).

### Uppdatera schemats kundschema

Du kan använda `schedule` för att uppdatera cron-schemat. Mer information om cron-scheman finns i [dokumentationen för cron-uttrycksformat](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) .

**API-format**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Värdet `id` för schemat som du vill uppdatera.

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `path` | Sökvägen för det värde som du vill laga. I det här fallet måste du ange värdet för `path` till `/schedule`eftersom du uppdaterar schemats kundschema. |
| `value` | Det uppdaterade värdet för `/state`filen. Värdet måste anges i form av ett kronschema. I det här exemplet körs schemat den andra varje månad. |

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll).

## Ta bort ett specifikt schema

Du kan begära att få ta bort ett angivet schema genom att göra en DELETE-begäran till `/config/schedules` och ange schemats `id` värde i sökvägen till begäran.

**API-format**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Värdet `id` för schemat som du vill ta bort.

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) med följande meddelande:

```json
(No Content) Schedule deleted successfully
```

## Nästa steg
