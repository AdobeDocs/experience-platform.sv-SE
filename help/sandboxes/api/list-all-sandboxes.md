---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: Visa alla sandlådor
topic: developer guide
description: Om du vill visa en lista över alla sandlådor som tillhör din IMS-organisation (aktiv eller annan), gör du en GET-begäran till slutpunkten /sandbox.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Visa alla sandlådor

Om du vill visa en lista över alla sandlådor som tillhör din IMS-organisation (aktiv eller annan), gör du en GET-begäran till `/sandboxes` slutpunkten.

**API-format**

```http
GET /sandboxes
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med sandlådor som tillhör din organisation, inklusive information som `name`, `title`, `state`och `type`.

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
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på sandlådan. Används för uppslagssyften i API-anrop. |
| `title` | Visningsnamnet för sandlådan. |
| `state` | Sandlådans aktuella bearbetningstillstånd. En sandlådestatus kan vara något av följande: <br/><ul><li>**skapa**: Sandlådan har skapats, men etableras fortfarande av systemet.</li><li>**aktiv**: Sandlådan skapas och är aktiv.</li><li>**misslyckades**: På grund av ett fel kunde sandlådan inte etableras av systemet och är inaktiverad.</li><li>**borttagen**: Sandlådan har inaktiverats manuellt.</li></ul> |
| `type` | Sandlådetypen, antingen &quot;development&quot; eller &quot;production&quot;. |
| `isDefault` | En boolesk egenskap som anger om den här sandlådan är standardsandlådan för organisationen. Vanligtvis är det här produktionssandlådan. |
| `eTag` | En identifierare för en specifik version av sandlådan. Detta värde används för versionskontroll och cachelagring av effektivitet och uppdateras varje gång en ändring görs i sandlådan. |
