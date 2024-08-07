---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;Experience data model;data model;datamodell;granskning;granskningslogg;change log;rpc;
solution: Experience Platform
title: API-slutpunkt för granskningslogg
description: Med slutpunkten /audilog i API:t för schemaregister kan du hämta en kronologisk lista över ändringar som har gjorts i en befintlig XDM-resurs.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# Slutpunkt för granskningslogg

För varje XDM-resurs (Experience Data Model) sparar [!DNL Schema Registry] en logg över alla ändringar som har gjorts mellan olika uppdateringar. Med slutpunkten `/auditlog` i API:t [!DNL Schema Registry] kan du hämta en granskningslogg för alla klasser, schemafältgrupper, datatyper eller scheman som anges av ID.

## Komma igång

Slutpunkten som används i den här guiden ingår i [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett Experience Platform-API.

Slutpunkten `/auditlog` är en del av RPC-anropen (Remote Procedure Call) som stöds av [!DNL Schema Registry]. Till skillnad från andra slutpunkter i API:t [!DNL Schema Registry] kräver RPC-slutpunkter inga ytterligare rubriker som `Accept` eller `Content-Type`, och använder inte `CONTAINER_ID`. I stället måste de använda namnutrymmet `/rpc`, vilket visas i API-anropet nedan.

## Hämta en granskningslogg för en resurs

Du kan hämta en granskningslogg för alla klasser, fältgrupper, datatyper eller scheman i schemabiblioteket genom att ange resursens ID i sökvägen för en GET-begäran till slutpunkten `/auditlog`.

**API-format**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` eller URL-kodad `$id` för resursen vars granskningslogg du vill hämta. |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar granskningsloggen för ett schema.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en kronologisk lista över ändringar som gjorts i resursen, från senaste till senaste.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| Egenskap | Beskrivning |
| --- | --- |
| `updates` | En array med objekt där varje objekt representerar en ändring som gjorts i den angivna resursen eller en av dess beroende resurser. |
| `id` | `$id` för resursen som ändrades. Det här värdet representerar vanligtvis den resurs som anges i sökvägen till begäran, men kan representera en beroende resurs om det är källan till ändringen. |
| `xdmType` | Den typ av resurs som ändrades. |
| `action` | Den typ av ändring som gjordes. |
| `path` | En [JSON-pekarsträng](../../landing/api-fundamentals.md#json-pointer) som anger sökvägen till det specifika fält som har ändrats eller lagts till. |
| `value` | Värdet som tilldelats det nya eller uppdaterade fältet. |

{style="table-layout:auto"}
