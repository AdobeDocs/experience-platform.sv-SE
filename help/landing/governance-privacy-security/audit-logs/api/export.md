---
title: API-slutpunkt för export av granskningshändelser
description: Lär dig hur du exporterar granskningshändelser i Experience Platform med API:t för granskningsfråga.
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 3%

---

# Exportera en lista med granskningshändelser

Du kan hämta händelsedata genom att göra en GET-förfrågan till `/audit/export` slutpunkt, ange de händelser som du vill hämta i nyttolasten.

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
| `assetType` | Typen av plattformsresurs som åtgärden utfördes på. <br/>Exempel: `?property=assetType==<an asset type>`. |

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

Resultatet genereras i en CSV-fil för export. Ett lyckat svar returnerar HTTP 307 utan svarstext. En länk till exportfilen finns i `Location` svarshuvud.
