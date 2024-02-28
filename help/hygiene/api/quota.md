---
title: API-slutpunkt för kvot
description: Med slutpunkten /quota i API:t för datahygien kan du övervaka användningen av den avancerade livscykelhanteringen av data mot organisationens månatliga kvotgränser för varje jobbtyp.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Kvotslutpunkt

The `/quota` -slutpunkten i API:t för datahygien gör att du kan övervaka användningen av livscykelhantering för avancerade data i förhållande till organisationens kvotgränser för varje jobbtyp.

Kvoter används för varje jobbtyp i datalängd på följande sätt:

* Borttagningar och uppdateringar av poster begränsas till ett visst antal förfrågningar varje månad.
* Datauppsättningens förfallodatum har en fast gräns för antalet samtidigt aktiva jobb, oavsett när förfallotiderna kommer att köras.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Innan du fortsätter bör du granska [översikt](./overview.md) för följande information:

* Länkar till relaterad dokumentation
* En guide till hur du läser exempelanrop till API i det här dokumentet
* Viktig information om obligatoriska huvuden som behövs för att kunna anropa ett Experience Platform-API

## Listkvoter {#list}

Du kan visa din organisations kvotinformation genom att göra en GET-förfrågan till `/quota` slutpunkt.

**API-format**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUOTA_TYPE}` | En valfri frågeparameter som anger vilken typ av kvot som ska hämtas. Om nej `quotaType` parametern anges, alla kvotvärden returneras i API-svaret. Godkända typvärden är:<ul><li>`expirationDatasetQuota`: Giltighetstid för datauppsättning</li><li>`deleteIdentityWorkOrderDatasetQuota`: Posten tas bort</li><li>`fieldUpdateWorkOrderDatasetQuota`: Postuppdateringar</li></ul> |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Svar**

Ett lyckat svar returnerar information om era livscykelkvoter för data.

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `quotas` | Visar kvotinformation för varje jobbtyp under datalängd. Varje kvotobjekt innehåller följande egenskaper:<ul><li>`name`: Datatillverkarens jobbtyp:<ul><li>`expirationDatasetQuota`: Giltighetstid för datauppsättning</li><li>`deleteIdentityWorkOrderDatasetQuota`: Posten tas bort</li></ul></li><li>`description`: En beskrivning av jobbtypen för livscykeln för data.</li><li>`consumed`: Antalet jobb av den här typen som körs under den aktuella månadsperioden.</li><li>`quota`: Kvotgränsen för den här jobbtypen. För postborttagningar och uppdateringar representerar detta antalet jobb som kan köras för varje månadsperiod. För datauppsättningens förfallodatum representerar detta antalet jobb som kan vara aktiva samtidigt vid en given tidpunkt.</li></ul> |

{style="table-layout:auto"}
