---
keywords: Experience Platform;hem;populära ämnen;lista över tillgängliga sandlådor;lissandlådor
solution: Experience Platform
title: API-slutpunkt för tillgängliga sandlådor
description: Du kan lista de sandlådor som är tillgängliga för den aktuella användaren genom att göra en GET-begäran till den tillgängliga sandlådeslutpunkten.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Tillgänglig sandlådeslutpunkt

>[!NOTE]
>
>Till skillnad från andra slutpunkter som finns i sandlådes-API:t är den här slutpunkten tillgänglig för alla användare, inklusive dem som saknar åtkomstbehörighet för sandlådeadministration.

Du kan lista de sandlådor som är tillgängliga för den aktuella användaren genom att göra en GET-begäran till den tillgängliga sandlådeslutpunkten.

**API-format**

```http
GET /{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. Se [appendix-dokument](./appendix.md#query) för en lista över tillgängliga parametrar. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett lyckat svar returnerar en lista över sandlådor som är tillgängliga för den aktuella användaren, inklusive information som `name`, `title`, `state`och `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på sandlådan. Används för uppslagssyften i API-anrop. |
| `title` | Visningsnamnet för sandlådan. |
| `state` | Sandlådans aktuella bearbetningstillstånd. En sandlådestatus kan vara något av följande: <ul><li>`creating`: Sandlådan har skapats, men etableras fortfarande av systemet.</li><li>`active`: Sandlådan skapas och är aktiv.</li><li>`failed`: På grund av ett fel kunde sandlådan inte etableras av systemet och är inaktiverad.</li><li>`deleted`: Sandlådan har inaktiverats manuellt.</li></ul> |
| `type` | Sandlådetypen, antingen &quot;development&quot; eller &quot;production&quot;. |
| `isDefault` | En boolesk egenskap som anger om den här sandlådan är standardproduktionssandlådan för organisationen. |
| `eTag` | En identifierare för en specifik version av sandlådan. Detta värde används för versionskontroll och cachelagring av effektivitet och uppdateras varje gång en ändring görs i sandlådan. |
