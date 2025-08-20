---
title: API-slutpunkt för granskningshändelser
description: Lär dig hur du hämtar granskningshändelser i Experience Platform med API:t för granskningsfråga.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Slutpunkt för granskningshändelser

Granskningsloggar används för att ge information om användaraktivitet för olika tjänster och funktioner. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen. Med slutpunkten `/audit/events` i API:t [!DNL Audit Query] kan du hämta händelsedata för din organisations aktivitet i [!DNL Experience Platform] programmatiskt.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett [!DNL Experience Platform] -API.

## Visa granskningshändelser

Du kan hämta händelsedata genom att göra en GET-begäran till `/audit/events`-slutpunkten och ange vilka händelser som ska hämtas i nyttolasten.

**API-format**

```http
GET /audit/events
```

API:t [!DNL Audit Query] har stöd för användning av frågeparametrar för att visa sidor och filtrera resultat när händelser listas.

| Parameter | Beskrivning |
| --- | --- |
| `limit` | Det maximala antalet poster som ska returneras i svaret. Standardvärdet `limit` är 50. |
| `start` | En pekare till det första objektet för de returnerade sökresultaten. Om du vill komma åt nästa resultatsida ska den här parametern ökas med samma mängd som anges i begränsningen. Exempel: Om du vill få åtkomst till nästa resultatsida för en begäran med limit=50 använder du parametern start=50, sedan start=100 för sidan därefter och så vidare. |
| `queryId` | När du gör en fråga till slutpunkten /audit/events innehåller svaret en queryId-strängegenskap. Om du vill göra samma fråga i ett separat anrop kan du inkludera ID-värdet som en enda frågeparameter i stället för att konfigurera sökparametrarna manuellt igen. |

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Svar**

Ett lyckat svar returnerar de resulterande datapunkterna för de mätvärden och filter som anges i begäran.

```json
{
  "_embedded": {
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `events` | En array vars objekt representerar var och en av händelserna som anges i begäran. Varje objekt innehåller information om filterkonfigurationen och returnerade händelsedata. |
| `userEmail` | E-postadressen till användaren som utförde händelsen. |
| `eventType` | Typ av händelse. Händelsetyperna är `Core` och `Enhanced`. |
| `imsOrgId` | ID för organisationen som händelsen ägde rum under. |
| `permissionResource` | Den produkt eller funktion som gav behörighet att utföra åtgärden. En resurs kan vara något av följande: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Behörighetstypen som används för åtgärden. |
| `assetType` | Den typ av Experience Platform-resurs som åtgärden utfördes på. |
| `assetId` | En unik identifierare för den Experience Platform-resurs som åtgärden utfördes på. |
| `assetName` | Namnet på den Experience Platform-resurs som åtgärden utfördes på. |
| `action` | Den typ av åtgärd som spelades in för händelsen. En åtgärd kan vara något av följande: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | Åtgärdens status. En status kan vara något av följande: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
