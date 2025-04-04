---
title: API-slutpunkt för granskningshändelser
description: Lär dig hur du hämtar granskningshändelser i Experience Platform med API:t för granskningsfråga.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
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
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `customerAuditLogList` | En array vars objekt representerar var och en av händelserna som anges i begäran. Varje objekt innehåller information om filterkonfigurationen och returnerade händelsedata. |
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
