---
keywords: Experience Platform;hem;populära ämnen;lissandlådor
solution: Experience Platform
title: List Sandboxes i API
topic: developer guide
description: Om du vill visa en lista över alla sandlådor som tillhör din IMS-organisation (aktiv eller annan), gör du en GET-begäran till slutpunkten /sandbox.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Lista sandlådor i API

Om du vill visa en lista över alla sandlådor som tillhör din IMS-organisation (aktiv eller annan), gör du en GET-begäran till `/sandboxes`-slutpunkten.

**API-format**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. Mer information finns i avsnittet [frågeparametrar](#query). |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med sandlådor som tillhör din organisation, inklusive information som `name`, `title`, `state` och `type`.

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
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform-int.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
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

## Använda frågeparametrar {#query}

API:t [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) har stöd för användning av frågeparametrar för att visa och filtrera resultat när sandlådor listas.

>[!NOTE]
>
>Frågeparametrarna `limit` och `offset` måste anges tillsammans. Om du bara anger ett fel returneras det. Om du anger ingen är standardgränsen 50 och förskjutningen 0.

| Parameter | Beskrivning |
| --------- | ----------- |
| `limit` | Det maximala antalet poster som ska returneras i svaret. |
| `offset` | Antalet enheter från den första posten att starta (förskjuta) svarslistan från. |