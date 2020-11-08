---
keywords: Experience Platform;home;popular topics;list active sandboxes;list sandboxes
solution: Experience Platform
title: Visa aktiva sandlådor för den aktuella användaren
topic: developer guide
description: Du kan lista de sandlådor som är aktiva för den aktuella användaren genom att göra en GET-begäran till rotslutpunkten.
translation-type: tm+mt
source-git-commit: 6326b3072737acf30ba2aee7081ce28dc9627a9a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Visa aktiva sandlådor för den aktuella användaren

>[!NOTE]
>
>Till skillnad från andra slutpunkter som finns i sandlådes-API:t är den här slutpunkten tillgänglig för alla användare, inklusive dem som saknar åtkomstbehörighet för sandlådeadministration.

Du kan visa de sandlådor som är aktiva för den aktuella användaren genom att göra en GET-begäran till roten (`/`).

**API-format**

```http
GET /{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. Mer information finns i avsnittet om [frågeparametrar](#query) . |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med sandlådor som är aktiva för den aktuella användaren, inklusive information som `name`, `title`, `state`och `type`.

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
| `state` | Sandlådans aktuella bearbetningstillstånd. En sandlådestatus kan vara något av följande: <ul><li>**skapa**: Sandlådan har skapats, men etableras fortfarande av systemet.</li><li>**aktiv**: Sandlådan skapas och är aktiv.</li><li>**misslyckades**: På grund av ett fel kunde sandlådan inte etableras av systemet och är inaktiverad.</li><li>**borttagen**: Sandlådan har inaktiverats manuellt.</li></ul> |
| `type` | Sandlådetypen, antingen &quot;development&quot; eller &quot;production&quot;. |
| `isDefault` | En boolesk egenskap som anger om den här sandlådan är standardsandlådan för organisationen. Vanligtvis är det här produktionssandlådan. |
| `eTag` | En identifierare för en specifik version av sandlådan. Detta värde används för versionskontroll och cachelagring av effektivitet och uppdateras varje gång en ändring görs i sandlådan. |

## Använda frågeparametrar {#query}

API:t har stöd för användning av frågeparametrar för att skicka och filtrera resultat när sandlådor listas. [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml)

>[!NOTE]
>
>Parametrarna `limit` och `offset` frågeparametrarna måste anges tillsammans. Om du bara anger ett fel returneras det. Om du anger ingen är standardgränsen 50 och förskjutningen 0.

| Parameter | Beskrivning |
| --------- | ----------- |
| `limit` | Det maximala antalet poster som ska returneras i svaret. |
| `offset` | Antalet enheter från den första posten att starta (förskjuta) svarslistan från. |
