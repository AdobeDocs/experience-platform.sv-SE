---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;Experience data model;data model;datamodell;granskning;granskningslogg;change log;rpc;
solution: Experience Platform
title: API-slutpunkt för granskningslogg
description: Med slutpunkten /audilog i API:t för schemaregister kan du hämta en kronologisk lista över ändringar som har gjorts i en befintlig XDM-resurs.
topic: utvecklarhandbok
translation-type: tm+mt
source-git-commit: 0727ffa0c72bcb6a85de1a13215b691b97889b70
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---


# Slutpunkt för granskningslogg

För varje Experience Data Model-resurs (XDM) sparar [!DNL Schema Registry] en logg över alla ändringar som har gjorts mellan olika uppdateringar. Med slutpunkten `/auditlog` i API:t [!DNL Schema Registry] kan du hämta en granskningslogg för alla klasser, mixin, datatyper eller scheman som anges av ID.

## Komma igång

Slutpunkten som används i den här guiden ingår i [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anropen i det här dokumentet och viktig information om vilka huvuden som krävs för att anropa ett Experience Platform-API.

Slutpunkten `/auditlog` är en del av RPC-anropen (Remote Procedure Call) som stöds av [!DNL Schema Registry]. Till skillnad från andra slutpunkter i API:t [!DNL Schema Registry], kräver RPC-slutpunkter inga ytterligare rubriker som `Accept` eller `Content-Type`, och använder inte en `CONTAINER_ID`. I stället måste de använda namnutrymmet `/rpc`, vilket visas i API-anropet nedan.

## Hämta en granskningslogg för en resurs

Du kan hämta en granskningslogg för alla klasser, blandningar, datatyper eller scheman i schemabiblioteket genom att ange resursens ID i sökvägen till slutpunkten för en GET-begäran.`/auditlog`

**API-format**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` eller URL-kodad `$id` för resursen vars granskningslogg du vill hämta. |

**Begäran**

Följande begäran hämtar granskningsloggen för en `Restaurant`-blandning.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en kronologisk lista över ändringar som gjorts i resursen, från senaste till senaste.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| Egenskap | Beskrivning |
| --- | --- |
| `auditTrails` | En array med objekt där varje objekt representerar en ändring som gjorts i den angivna resursen eller en av dess beroende resurser. |
| `id` | `$id` för resursen som ändrades. Det här värdet representerar vanligtvis den resurs som anges i sökvägen, men kan representera en beroende resurs om det är källan till ändringen. |
| `action` | Den typ av ändring som gjordes. |
| `path` | En [JSON-pekare](../../landing/api-fundamentals.md#json-pointer)-sträng som anger sökvägen till det specifika fält som har ändrats eller lagts till. |
| `value` | Värdet som tilldelats det nya eller uppdaterade fältet. |