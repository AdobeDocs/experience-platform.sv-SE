---
title: Spela in ta bort arbetsorder
description: Lär dig hur du använder slutpunkten /workorder i API:t Data Hygiene för att hantera postborttagningsarbetsorder i Adobe Experience Platform. Den här guiden täcker kvoter, bearbetningstidslinjer och API-användning.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 4f4b668c2b29228499dc28b2c6c54656e98aaeab
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 1%

---

# Registrera borttagning av arbetsorder {#work-order-endpoint}

Använd slutpunkten `/workorder` i API:t för datahygien för att skapa, visa och hantera arbetsorder för borttagning av poster i Adobe Experience Platform. Med arbetsorder kan ni styra, övervaka och spåra borttagning av data mellan datauppsättningar för att upprätthålla datakvaliteten och stödja organisationens standarder för datastyrning.

>[!IMPORTANT]
>
>Arbetsorder för radering av poster används för datarensning, borttagning av anonyma data eller datamängning. **Använd inte postborttagning av arbetsorder för förfrågningar om rättigheter för registrerade i enlighet med sekretessbestämmelser som GDPR.** Använd [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) om du vill ha exempel på efterlevnad.

## Komma igång

Innan du börjar kan du läsa [översikten](./overview.md) för att lära dig mer om obligatoriska rubriker, hur du läser exempel-API-anrop och var du hittar relaterad dokumentation.

## Kvoter och bearbetningstidslinjer {#quotas}

Gränserna för att skicka in raderade arbetsorder gäller för dag- och månadsvisa ID-inlämningar, som bestäms av din organisations licensberättigande. Dessa begränsningar gäller för både UI- och API-baserade begäranden om postborttagning.

>[!NOTE]
>
>Du kan skicka upp till **1 000 000 identifierare per dag**, men bara om den återstående månadskvoten tillåter det. Om din månadskvot är mindre än 1 miljon, kan din dagliga inskickning inte överstiga denna gräns.

### Möjlighet att skicka in per produkt varje månad {#quota-limits}

I följande tabell visas inskicksgränser för identifierare per produkt och berättigandenivå. För varje produkt är den månatliga övre gränsen det lägsta av två värden: ett fast identifierartak eller ett procentbaserat tröskelvärde som är knutet till den licensierade datavolymen.

| Produkt | Tillståndsbeskrivning | Månatligt tak (den som är mindre) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP eller Adobe Journey Optimizer | Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | 2 000 000 identifierare eller 5 % av den adresserbara publiken |
| Real-Time CDP eller Adobe Journey Optimizer | Med tillägget Privacy and Security Shield eller Healthcare Shield | 15 000 000 identifierare eller 10 % av den adresserbara publiken |
| Customer Journey Analytics | Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | 2 000 000 identifierare eller 100 identifierare per miljon CJA-rader |
| Customer Journey Analytics | Med tillägget Privacy and Security Shield eller Healthcare Shield | 15 000 000 identifierare eller 200 identifierare per miljon CJA-rader |

>[!NOTE]
>
>De flesta organisationer har lägre månadsgränser baserat på den faktiska adresserbara målgruppen eller CJA-radrättigheterna.

>[!NOTE]
>
>Kvoterna återställs den första dagen i varje kalendermånad. Oanvänd kvot för överföring av **inte**.

>[!NOTE]
>
>Kvotanvändningen baseras på din organisations licensierade månadsberättigande för **skickade identifierare**. Kvoterna styrs inte av systemgarantisystem, men kan övervakas och granskas.\
>Posten för borttagning av arbetsorderkapacitet är en **delad tjänst**. Det högsta antalet licenser som gäller för Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics och eventuella tillägg till Shield.

### Bearbetar tidslinjer för identifieraröverföringar {#sla-processing-timelines}

När du har skickat in en post köas och bearbetas arbetsorder för borttagning baserat på din berättigandenivå.

| Produkt- och berättigandebeskrivning | Kövaraktighet | Maximal bearbetningstid (SLA) |
|------------------------------------|---------------------|-------------------------------|
| Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | Upp till 15 dagar | 30 dagar |
| Med tillägget Privacy and Security Shield eller Healthcare Shield | Normalt 24 timmar | 15 dagar |

Om din organisation kräver högre gränser kontaktar du Adobe för att få en tillståndsgranskning.

>[!TIP]
>
>Information om hur du kontrollerar din aktuella kvotanvändning eller tillståndsnivå finns i [referensguiden för kvoter](../api/quota.md).

## Lista post ta bort arbetsorder {#list}

Hämta en sidnumrerad lista med arbetsorder för att ta bort poster för datahygien i organisationen. Filtrera resultat med frågeparametrar. Varje arbetsorderpost innehåller åtgärdstypen (till exempel `identity-delete`), status, relaterad datauppsättning och användarinformation samt granskningsmetadata.

**API-format**

```http
GET /workorder
```

I följande tabell beskrivs de frågeparametrar som är tillgängliga för att lista arbetsorder för radering av poster.

| Frågeparameter | Beskrivning |
| --------------- | ------------|
| `search` | Skiftlägeskänslig partiell matchning (jokerteckensökning) mellan fält: författare, visningsnamn, beskrivning eller datauppsättningsnamn. Matchar även exakt förfallodatum-ID. |
| `type` | Filtrera resultat efter arbetsordertyp (t.ex. `identity-delete`). |
| `status` | Kommaavgränsad lista över arbetsorderstatusar. Statusvärden är skiftlägeskänsliga.<br>Uppräkning: `received`, `validated`, `submitted`, `ingested`, `completed`, `failed` |
| `author` | Hitta den person som senast uppdaterade arbetsordern (eller den som skapade originalet). Accepterar literalt eller SQL-mönster. |
| `displayName` | Skiftlägesokänslig matchning för arbetsorderns visningsnamn. |
| `description` | Skiftlägesokänslig matchning för arbetsorderbeskrivning. |
| `workorderId` | Exakt matchning för arbetsorder-ID. |
| `sandboxName` | Exakt matchning för sandlådenamn som används i begäran, eller använd `*` för att inkludera alla sandlådor. |
| `fromDate` | Filtrera efter arbetsorder som skapats på eller efter detta datum. Kräver att `toDate` anges. |
| `toDate` | Filtrera efter arbetsorder som skapats på eller före detta datum. Kräver att `fromDate` anges. |
| `filterDate` | Returnerar endast arbetsorder som har skapats, uppdaterats eller ändrats detta datum. |
| `page` | Sidindex som ska returneras (börjar vid 0). |
| `limit` | Högsta antal resultat per sida (1-100, standard: 25). |
| `orderBy` | Sorteringsordning för resultat. Använd prefixet `+` eller `-` för stigande/fallande. Exempel: `orderBy=-datasetName`. |
| `properties` | Kommaavgränsad lista med ytterligare fält som ska inkluderas per resultat. Valfritt. |


**Begäran**

Följande begäran hämtar alla slutförda arbetsorder för radering av poster, begränsat till två per sida:

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en numrerad lista över arbetsorder för radering av poster.

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

I följande tabell beskrivs egenskaperna i svaret.

| Egenskap | Beskrivning |
| --- | --- |
| `results` | Array med postborttagningar av arbetsorderobjekt. Varje objekt innehåller fälten nedan. |
| `workorderId` | Den unika identifieraren för postens arbetsorder för borttagning. |
| `orgId` | Din unika organisations-ID. |
| `bundleId` | Den unika identifieraren för paketet som innehåller den här postens arbetsorder för borttagning. Med paketering kan flera raderingsorder grupperas och bearbetas tillsammans av underordnade tjänster. |
| `action` | Åtgärdstypen som begärdes i arbetsordern. |
| `createdAt` | Tidsstämpeln när arbetsordern skapades. |
| `updatedAt` | Tidsstämpeln när arbetsordern senast uppdaterades. |
| `operationCount` | Antalet åtgärder som ingår i arbetsordern. |
| `targetServices` | Lista över måltjänster för arbetsordern. |
| `status` | Aktuell status för arbetsordern. Möjliga värden är: `received`,`validated`, `submitted`, `ingested`, `completed` och `failed`. |
| `createdBy` | E-postadress och identifierare för den användare som skapade arbetsordern. |
| `datasetId` | Den unika identifieraren för den datauppsättning som är associerad med arbetsordern. Om begäran gäller alla datauppsättningar ställs fältet in på ALL. |
| `datasetName` | Namnet på datauppsättningen som är associerad med arbetsordern. |
| `displayName` | En etikett som kan läsas av människor för arbetsordern. |
| `description` | En beskrivning av arbetsorderns syfte. |
| `total` | Totalt antal arbetsorder för borttagning av poster som matchar frågan. |
| `count` | Antal arbetsorder för radering av poster på den aktuella sidan. |
| `_links` | Sidnumrering och navigeringslänkar. |
| `next` | Objekt med `href` (sträng) och `templated` (booleskt) för nästa sida. |
| `page` | Objekt med `href` (sträng) och `templated` (booleskt) för sidnavigering. |

{style="table-layout:auto"}

## Skapa en post för borttagning av arbetsorder {#create}

Om du vill ta bort poster som är associerade med en eller flera identiteter från en enskild datamängd eller alla datamängder, gör du en POST-begäran till `/workorder`-slutpunkten.

Arbetsorder bearbetas asynkront och visas i arbetsorderlistan när de har skickats.

>[!TIP]
>
>Varje postborttagningsarbetsorder som skickas via API kan innehålla upp till **100 000 identiteter**. Skicka så många identiteter per begäran som möjligt för att maximera effektiviteten. Undvik att skicka in stora mängder, t.ex. arbetsorder med ett enda ID.

**API-format**

```http
POST /workorder
```

>[!NOTE]
>
>Du kan bara ta bort poster från datauppsättningar vars associerade XDM-schema definierar en primär identitet eller identitetskarta.

>[!NOTE]
>
>Om du försöker skapa en postborttagningsarbetsorder för en datauppsättning som redan har en aktiv förfallotid, returnerar begäran HTTP 400 (Ogiltig begäran). En aktiv förfallotid är en schemalagd borttagning som ännu inte har slutförts.

**Begäran**

Följande begäran tar bort alla poster som är associerade med angivna e-postadresser från en viss datauppsättning.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

I följande tabell beskrivs egenskaperna för att skapa en postborttagningsarbetsordning.

| Egenskap | Beskrivning |
| --- | --- |
| `displayName` | En etikett som kan läsas av människor för den här posten tar bort arbetsorder. |
| `description` | En beskrivning av postens arbetsorder för borttagning. |
| `action` | Den begärda åtgärden för postborttagning av arbetsorder. Använd `delete_identity` om du vill ta bort poster som är associerade med en viss identitet. |
| `datasetId` | Den unika identifieraren för datauppsättningen. Använd datauppsättnings-ID:t för en specifik datauppsättning, eller `ALL` om du vill ange alla datauppsättningar som mål. Datauppsättningar måste ha en primär identitet eller identitetskarta. Om det finns en identitetskarta finns den som ett fält på den översta nivån med namnet `identityMap`.<br>Observera att en datauppsättningsrad kan ha många identiteter i sin identitetskarta, men bara en kan markeras som primär. `"primary": true` måste inkluderas för att `id` ska matcha en primär identitet. |
| `namespacesIdentities` | En array med objekt som var och en innehåller:<br><ul><li> `namespace`: Ett objekt med en `code`-egenskap som anger identitetsnamnutrymmet (t.ex. &quot;email&quot;).</li><li> `IDs`: En array med identitetsvärden som ska tas bort för det här namnområdet.</li></ul>Identitetsnamnutrymmen ger kontext till identitetsdata. Du kan använda standardnamnutrymmen från Experience Platform eller skapa egna. Mer information finns i dokumentationen för [identitetsnamnrymden](../../identity-service/features/namespaces.md) och [API-specifikationen för identitetstjänsten](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

**Svar**

Ett lyckat svar returnerar information om den nya postens arbetsorder för borttagning.

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

I följande tabell beskrivs egenskaperna i svaret.

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | Den unika identifieraren för postens arbetsorder för borttagning. Använd det här värdet för att slå upp status eller information om borttagningen. |
| `orgId` | Din unika organisations-ID. |
| `bundleId` | Den unika identifieraren för paketet som innehåller den här postens arbetsorder för borttagning. Med paketering kan flera raderingsorder grupperas och bearbetas tillsammans av underordnade tjänster. |
| `action` | Åtgärdstypen som begärdes i postens arbetsorder för borttagning. |
| `createdAt` | Tidsstämpeln när arbetsordern skapades. |
| `updatedAt` | Tidsstämpeln när arbetsordern senast uppdaterades. |
| `operationCount` | Antalet åtgärder som ingår i arbetsordern. |
| `targetServices` | En lista med måltjänster för postens radering av arbetsorder. |
| `status` | Aktuell status för postens radera arbetsorder. |
| `createdBy` | E-postadressen och identifieraren för den användare som skapade posten tar bort arbetsorder. |
| `datasetId` | Den unika identifieraren för datauppsättningen. Om begäran gäller alla datauppsättningar anges värdet till `ALL`. |
| `datasetName` | Namnet på datauppsättningen för den här posten tar bort arbetsorder. |
| `displayName` | En etikett som kan läsas av människor för arbetsorder för radering av poster. |
| `description` | En beskrivning av postens arbetsorder för borttagning. |

{style="table-layout:auto"}

>[!NOTE]
>
>Åtgärdsegenskapen för arbetsorder för att ta bort poster är för närvarande `identity-delete` i API-svar. Om API:t ändras till ett annat värde (till exempel `delete_identity`) uppdateras den här dokumentationen därefter.

## Hämta information för en viss postborttagningsarbetsorder {#lookup}

Hämta information för en viss postborttagningsarbetsordning genom att göra en GET-begäran till `/workorder/{WORKORDER_ID}`. Svaret innehåller åtgärdstyp, status, associerad datauppsättning och användarinformation samt granskningsmetadata.

**API-format**

```http
GET /workorder/{WORKORDER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | Den unika identifieraren för den postborttagningsarbetsorder som du söker upp. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om den angivna arbetsordern för borttagning av post.

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

I följande tabell beskrivs egenskaperna i svaret.

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | Den unika identifieraren för postens arbetsorder för borttagning. |
| `orgId` | Organisationens unika identifierare. |
| `bundleId` | Den unika identifieraren för paketet som innehåller den här postens arbetsorder för borttagning. Med paketering kan flera raderingsorder grupperas och bearbetas tillsammans av underordnade tjänster. |
| `action` | Åtgärdstypen som begärdes i postens arbetsorder för borttagning. |
| `createdAt` | Tidsstämpeln när arbetsordern skapades. |
| `updatedAt` | Tidsstämpeln när arbetsordern senast uppdaterades. |
| `operationCount` | Antalet åtgärder som ingår i arbetsordern. |
| `targetServices` | En lista över måltjänster som påverkas av den här posten tar bort arbetsorder. |
| `status` | Aktuell status för postens radera arbetsorder. |
| `createdBy` | E-postadressen och identifieraren för den användare som skapade posten tar bort arbetsorder. |
| `datasetId` | Den unika identifieraren för den datauppsättning som är associerad med arbetsordern. |
| `datasetName` | Namnet på datauppsättningen som är associerad med arbetsordern. |
| `displayName` | En etikett som kan läsas av människor för arbetsorder för radering av poster. |
| `description` | En beskrivning av postens arbetsorder för borttagning. |

## Uppdatera en post, ta bort arbetsorder

Uppdatera `name` och `description` för en postborttagning av arbetsorder genom att göra en PUT-begäran till slutpunkten `/workorder/{WORKORDER_ID}`.

**API-format**

```http
PUT /workorder/{WORKORDER_ID}
```

I följande tabell beskrivs parametern för denna begäran.

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | Den unika identifieraren för den postborttagningsarbetsorder som du vill uppdatera. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

I följande tabell beskrivs de egenskaper som du kan uppdatera.

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Den uppdaterade etiketten som kan läsas av människor för postens arbetsorder för radering. |
| `description` | Den uppdaterade beskrivningen för postens radering av arbetsorder. |

{style="table-layout:auto"}

**Svar**

Ett svar returnerar den uppdaterade arbetsorderbegäran.

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
  "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Egenskap | Beskrivning |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | Den unika identifieraren för postens arbetsorder för borttagning. |
| `orgId` | Organisationens unika identifierare. |
| `bundleId` | Den unika identifieraren för paketet som innehåller den här postens arbetsorder för borttagning. Med paketering kan flera raderingsorder grupperas och bearbetas tillsammans av underordnade tjänster. |
| `action` | Åtgärdstypen som begärdes i postens arbetsorder för borttagning. |
| `createdAt` | Tidsstämpeln när arbetsordern skapades. |
| `updatedAt` | Tidsstämpeln när arbetsordern senast uppdaterades. |
| `operationCount` | Antalet åtgärder som ingår i arbetsordern. |
| `targetServices` | En lista över måltjänster som påverkas av den här posten tar bort arbetsorder. |
| `status` | Aktuell status för postens radera arbetsorder. Möjliga värden är: `received`,`validated`, `submitted`, `ingested`, `completed` och `failed`. |
| `createdBy` | E-postadressen och identifieraren för den användare som skapade posten tar bort arbetsorder. |
| `datasetId` | Den unika identifieraren för den datauppsättning som är associerad med postens arbetsorder för borttagning. |
| `datasetName` | Namnet på den datauppsättning som är associerad med postens arbetsorder för borttagning. |
| `displayName` | En etikett som kan läsas av människor för arbetsorder för radering av poster. |
| `description` | En beskrivning av postens arbetsorder för borttagning. |
| `productStatusDetails` | En array som visar den aktuella statusen för processerna längre fram i kedjan för begäran. Varje objekt innehåller:<ul><li>`productName`: Namnet på den underordnade tjänsten.</li><li>`productStatus`: Aktuell bearbetningsstatus från den underordnade tjänsten.</li><li>`createdAt`: Tidsstämpeln när den senaste statusen bokfördes av tjänsten.</li></ul>Den här egenskapen är tillgänglig när arbetsordern har skickats till tjänster i senare led för att påbörja bearbetningen. |

{style="table-layout:auto"}
