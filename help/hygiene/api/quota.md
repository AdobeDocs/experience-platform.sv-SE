---
title: API-slutpunkt för kvot
description: Med slutpunkten /quota i API:t för datahygien kan du övervaka användningen av livscykelhantering för avancerade data i förhållande till organisationens månatliga kvotgränser för varje jobbtyp.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Kvotslutpunkt

Slutpunkten `/quota` i API:t för datahygien gör att du kan övervaka användningen av livscykelhantering för avancerade data i förhållande till organisationens kvotgränser för varje jobbtyp.

Kvoter används för varje jobbtyp för datalifecycle på följande sätt:

* Borttagningar och uppdateringar av poster begränsas till ett visst antal förfrågningar varje månad.
* Datauppsättningens förfallodatum har en fast gräns för antalet samtidigt aktiva jobb, oavsett när förfallotiderna kommer att köras.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Granska [översikten](./overview.md) för följande information innan du fortsätter:

* Länkar till relaterad dokumentation
* En guide till hur du läser exempelanrop till API i det här dokumentet
* Viktig information om de rubriker som krävs för att anropa ett Experience Platform-API

## Listkvoter {#list}

Du kan visa din organisations kvotinformation genom att göra en GET-förfrågan till slutpunkten `/quota`.

**API-format**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUOTA_TYPE}` | En valfri frågeparameter som anger vilken typ av kvot som ska hämtas. Om ingen `quotaType`-parameter anges returneras alla kvotvärden i API-svaret. Godkända typvärden är:<ul><li>`datasetExpirationQuota`: Det här objektet visar hur många datamängder som förfaller samtidigt för din organisation, och din totala tillåtna gräns för förfallodatum. </li><li>`dailyConsumerDeleteIdentitiesQuota`: Det här objektet visar det totala antalet begäranden om borttagning av poster som din organisation har gjort idag och din totala dagsavgift.<br>Obs! Endast accepterade begäranden räknas. Om en arbetsorder refuseras på grund av att den inte kan valideras, räknas inte dessa identitetsborttagningar mot din kvot.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: Det här objektet visar det totala antalet begäranden om borttagning av poster som din organisation gjort den här månaden och din totala månadskvot.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: Det här objektet visar det totala antalet postuppdateringsbegäranden som din organisation har gjort den här månaden och din totala månadskvot.</li></ul> |

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
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 600000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 600000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `quotas` | Visar kvotinformation för varje jobbtyp under datalängd. Varje kvotobjekt innehåller följande egenskaper:<ul><li>`name`: Datatillverkarens jobbtyp:<ul><li>`expirationDatasetQuota`: Datauppsättningens förfallodatum</li><li>`deleteIdentityWorkOrderDatasetQuota`: Posten tas bort</li></ul></li><li>`description`: En beskrivning av jobbtypen för livscykeln för data.</li><li>`consumed`: Antalet jobb av den här typen körs under den aktuella perioden. Objektnamnet anger kvotperioden.</li><li>`quota`: Tilldelningen för den här jobbtypen för din organisation. För radering och uppdatering av poster representerar kvoten antalet jobb som kan köras för varje månadsperiod. För datauppsättningens förfallodatum representerar kvoten antalet jobb som kan vara aktiva samtidigt vid en given tidpunkt.</li></ul> |

{style="table-layout:auto"}
