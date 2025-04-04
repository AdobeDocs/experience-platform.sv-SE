---
title: API-slutpunkt för export av granskningshändelser
description: Lär dig hur du exporterar granskningshändelser i Experience Platform med API:t för granskningsfråga.
role: Developer
feature: Audits, API
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Exportera en lista med granskningshändelser

Du kan hämta händelsedata genom att göra en GET-begäran till `/audit/export`-slutpunkten och ange vilka händelser som ska hämtas i nyttolasten.

**API-format**

```http
GET /audit/export
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `timestamp` | När du filtrerar efter tidsstämpel är det bäst att använda ett intervall med operatorerna > och &lt; i stället för ett exakt värde. <br/>Exempel: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | Åtgärdens status. En status kan vara något av följande: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>Exempel: `?property=status==Deny`. |
| `action` | Den typ av åtgärd som spelades in för händelsen. En åtgärd kan vara något av följande: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> Exempel: `?property=action==Create`. |
| `user` | Den användare som utförde händelsen. |
| `assetType` | Den typ av Experience Platform-resurs som åtgärden utfördes på. <br/>Exempel: `?property=assetType==<an asset type>`. |

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Svar**

Resultatet genereras i en CSV-fil för export. Ett lyckat svar returnerar HTTP 307 utan svarstext. En länk till exportfilen finns i svarsrubriken `Location`.
