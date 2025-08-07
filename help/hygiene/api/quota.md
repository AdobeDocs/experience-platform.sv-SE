---
title: API-slutpunkt för kvot
description: Med slutpunkten /quota i API:t för datahygien kan du övervaka användningen av livscykelhantering för avancerade data i förhållande till organisationens månatliga kvotgränser för varje jobbtyp.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---

# Kvotslutpunkt

Använd slutpunkten `/quota` i Data Hygiene API för att kontrollera din organisations aktuella användning och begränsningar. Kvoterna varierar beroende på vilka rättigheter som gäller, t.ex. sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden.

Övervaka den aktuella kvotförbrukningen för att säkerställa att organisatoriska gränser för varje jobbtyp följs.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Granska [översikten](./overview.md) för följande information innan du fortsätter:

* Länkar till relaterad dokumentation
* Läs exempel-API-anrop
* Nödvändiga rubriker för Experience Platform API-anrop

## Kvoter och bearbetningstidslinjer {#quotas}

Registrera borttagningsbegäranden omfattas av kvoter och förväntningar på servicenivå baserat på din licensbehörighet. Dessa begränsningar gäller för både UI- och API-baserade borttagningsbegäranden.

>[!TIP]
>
>I det här dokumentet visas hur du frågar efter användningen mot berättigandebaserade begränsningar. En fullständig beskrivning av kvotnivåer, borttagningsrättigheter för poster och SLA-beteende finns i dokumenten [UI-baserad postborttagning](../ui/record-delete.md#quotas) eller [API-baserad postborttagning](./workorder.md#quotas).

## Listkvoter {#list}

Du kan visa din organisations kvotinformation genom att göra en GET-förfrågan till slutpunkten `/quota`.

**API-format**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

>[!NOTE]
>
>Kvotförbrukningen återställs dagligen och månadsvis den 1 i varje månad kl. 00:00 GMT.
>
>Endast accepterade begäranden räknas in i din kvot. Avvisade arbetsorder minskar inte din kvot.

| Parameter | Beskrivning |
| --- | --- |
| `{QUOTA_TYPE}` | En valfri frågeparameter som anger vilken typ av kvot som ska hämtas. Om ingen `quotaType`-parameter anges returneras alla kvotvärden i API-svaret. Godkända värden är:<ul><li>`datasetExpirationQuota`: Antalet aktiva datauppsättningens förfallodatum och din totala tillåten mängd.</li><li>`dailyConsumerDeleteIdentitiesQuota`: Antalet poster tas bort idag och din dagliga kvot.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: Antalet poster tar bort den här månaden och din månadskvot.</li></ul> |

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
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| Egenskap | Beskrivning |
| -------- | ------- |
| `quotas` | Visar kvotinformation för varje jobbtyp under datalängd. Varje kvotobjekt innehåller följande egenskaper:<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | Identifierare för kvottyp. |
| `description` | En beskrivning av vad denna kvot begränsar. |
| `consumed` | Den mängd kvot som för närvarande förbrukas. Den förbrukade mängden återställs den 1:e i månaden vid 00:00 GMT och 00:00 GMT för daglig kvot. |
| `quota` | Den maximala tilldelningen av den här kvottypen för din organisation. |
