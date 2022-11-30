---
title: API-slutpunkt för kvot
description: Med slutpunkten /quota i Data Hygiene API kan du övervaka din datahygien mot organisationens månatliga kvotgränser för varje jobbtyp.
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 1c6a5df6473e572cae88a5980fe0db9dfcf9944e
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 1%

---

# Kvotslutpunkt

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**.

The `/quota` -slutpunkten i Data Hygiene API gör att du kan övervaka din datahygien mot organisationens kvotgränser för varje jobbtyp.

För varje jobbtyp för datahygien används kvoter på följande sätt:

* Borttagningar och uppdateringar av poster begränsas till ett visst antal förfrågningar varje månad.
* Datauppsättningens förfallodatum har en fast gräns för antalet samtidigt aktiva jobb, oavsett när förfallotiderna kommer att köras.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Läs igenom [översikt](./overview.md) för följande information:

* Länkar till relaterad dokumentation
* En guide till hur du läser exempelanrop till API:t i det här dokumentet
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
| `{QUOTA_TYPE}` | En valfri frågeparameter som anger vilken typ av kvot som ska hämtas. Om nej `quotaType` parametern anges, alla kvotvärden returneras i API-svaret. Godkända typvärden är:<ul><li>`expirationDatasetQuota`: Utgångsdatum för datauppsättning</li><li>`deleteIdentityWorkOrderDatasetQuota`: Posten tas bort</li><li>`fieldUpdateWorkOrderDatasetQuota`: Spela in uppdateringar</li></ul> |

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

Ett lyckat svar returnerar detaljerna om dina datahygien.

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
| `quotas` | Visar kvotinformation för varje datahygien-jobbtyp. Varje kvotobjekt innehåller följande egenskaper:<ul><li>`name`: Typ av datahygien:<ul><li>`expirationDatasetQuota`: Utgångsdatum för datauppsättning</li><li>`deleteIdentityWorkOrderDatasetQuota`: Posten tas bort</li></ul></li><li>`description`: En beskrivning av jobbtypen för datahygien.</li><li>`consumed`: Antalet jobb av den här typen som körs under den aktuella månadsperioden.</li><li>`quota`: Kvotgränsen för den här jobbtypen. För postborttagningar och uppdateringar representerar detta antalet jobb som kan köras för varje månadsperiod. För datauppsättningens förfallodatum representerar detta antalet jobb som kan vara aktiva samtidigt vid en given tidpunkt.</li></ul> |

{style=&quot;table-layout:auto&quot;}
