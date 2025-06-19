---
title: Begäranden om radering av post (arbetsorderslutpunkt)
description: Med slutpunkten /workorder i Data Hygiene API kan du programmässigt hantera borttagningsåtgärder för identiteter.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 1%

---

# Posta borttagningsbegäranden (arbetsorderslutpunkt) {#work-order-endpoint}

Med slutpunkten `/workorder` i API:t för datahygien kan du programmässigt hantera begäranden om postborttagning i Adobe Experience Platform.

>[!IMPORTANT]
> 
>Borttagning av poster ska användas för datarensning, borttagning av anonyma data eller datamängning. De **får inte** användas för förfrågningar om rättigheter för registrerade (efterlevnad) som gäller sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). Använd [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället för alla kompatibilitetsfall.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Innan du fortsätter bör du gå igenom [översikten](./overview.md) och se om det finns länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anrop i det här dokumentet samt viktig information om vilka huvuden som krävs för att anropa Experience Platform-API:er.

## Kvoter och bearbetningstidslinjer {#quotas}

Begäran om att radera poster omfattas av dagliga och månadsvisa gränser för hur många identifierare som får skickas in, beroende på organisationens licensberättigande. Dessa begränsningar gäller för både UI- och API-baserade borttagningsbegäranden.

>[!NOTE]
>
>Du kan skicka upp till **1 000 000 identifierare per dag**, men bara om den återstående månadskvoten tillåter det. Om din månadskvot är mindre än 1 miljon, kan din dagliga inskickning inte överstiga denna gräns.

### Möjlighet att skicka in per produkt varje månad {#quota-limits}

Tabellen nedan visar inlämningsgränser för identifierare per produkt och berättigandenivå. För varje produkt är den månatliga övre gränsen det lägsta av två värden: ett fast identifierartak eller ett procentbaserat tröskelvärde som är knutet till den licensierade datavolymen.

| Produkt | Tillståndsbeskrivning | Månatligt tak (den som är mindre) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP eller Adobe Journey Optimizer | Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | 2 000 000 identifierare eller 5 % av den adresserbara publiken |
| Real-Time CDP eller Adobe Journey Optimizer | Med tillägget Privacy and Security Shield eller Healthcare Shield | 15 000 000 identifierare eller 10 % av den adresserbara publiken |
| Customer Journey Analytics | Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | 2 000 000 identifierare eller 100 identifierare per miljon CJA-rader |
| Customer Journey Analytics | Med tillägget Privacy and Security Shield eller Healthcare Shield | 15 000 000 identifierare eller 200 identifierare per miljon CJA-rader |

>[!NOTE]
>
> De flesta organisationer har lägre månadsgränser baserat på den faktiska adresserbara målgruppen eller CJA-radrättigheterna.

Kvoterna återställs den första dagen i varje kalendermånad. Oanvänd kvot för överföring av **inte**.

>[!NOTE]
>
>Kvoterna baseras på din organisations licensierade månadsberättigande för **skickade identifierare**. Dessa används inte av systemskyddsräcken, men kan övervakas och granskas.
>
>Borttagning av post är en **delad tjänst**. Det högsta antalet licenser som gäller för Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics och eventuella tillägg till Shield.

### Bearbetar tidslinjer för identifieraröverföringar {#sla-processing-timelines}

När du har skickat in en post köas och bearbetas förfrågningar om radering baserat på din berättigandenivå.

| Produkt- och berättigandebeskrivning | Kövaraktighet | Maximal bearbetningstid (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Utan tillägg till sköld för skydd av privatlivet och säkerheten eller hälso- och sjukvårdsskölden | Upp till 15 dagar | 30 dagar |
| Med tillägget Privacy and Security Shield eller Healthcare Shield | Normalt 24 timmar | 15 dagar |

Om din organisation kräver högre gränser kontaktar du Adobe för att få en tillståndsgranskning.

>[!TIP]
>
>Information om hur du kontrollerar din aktuella kvotanvändning eller tillståndsnivå finns i [referensguiden för kvoter](../api/quota.md).

## Skapa en begäran om postborttagning {#create}

Du kan ta bort en eller flera identiteter från en enskild datauppsättning eller alla datauppsättningar genom att göra en POST-begäran till `/workorder`-slutpunkten.

>[!TIP]
>
>Varje postborttagningsbegäran som skickas via API kan innehålla upp till **100 000 identiteter**. För att maximera effektiviteten skickar du så många identiteter per begäran som möjligt och undviker att skicka in stora mängder, t.ex. enstaka ID-arbetsorder.

**API-format**

```http
POST /workorder
```

>[!NOTE]
>
>Data Lifecycle-begäranden kan bara ändra datauppsättningar som baseras på primära identiteter eller en identitetskarta. En begäran måste antingen ange den primära identiteten eller tillhandahålla en identitetskarta.

**Begäran**

Beroende på värdet för `datasetId` som anges i den begärda nyttolasten, tar API-anropet bort identiteter från alla datauppsättningar eller en enskild datauppsättning som du anger. Följande begäran tar bort tre identiteter från en specifik datauppsättning.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `action` | Den åtgärd som ska utföras. Värdet måste anges till `delete_identity` för postborttagningar. |
| `datasetId` | Om du tar bort från en enskild datauppsättning måste det här värdet vara ID:t för datauppsättningen i fråga. Om du tar bort från alla datauppsättningar anger du värdet till `ALL`.<br><br>Om du anger en enskild datauppsättning måste datasetens associerade XDM-schema (Experience Data Model) ha en primär identitet definierad. Om datauppsättningen inte har någon primär identitet måste den ha en identitetskarta för att kunna ändras av en begäran om datatillägslivet.<br>Om det finns en identitetskarta kommer den att finnas som ett fält på den översta nivån med namnet `identityMap`.<br>Observera att en datauppsättningsrad kan ha många identiteter i sin identitetskarta, men bara en kan markeras som primär. `"primary": true` måste inkluderas för att `id` ska matcha en primär identitet. |
| `displayName` | Visningsnamnet för postborttagningsbegäran. |
| `description` | En beskrivning av postborttagningsbegäran. |
| `identities` | En array som innehåller identiteterna för minst en användare vars information du vill ta bort. Varje identitet består av ett [ID-namnområde](../../identity-service/features/namespaces.md) och ett värde:<ul><li>`namespace`: Innehåller en enda strängegenskap, `code`, som representerar identitetsnamnutrymmet. </li><li>`id`: Identitetsvärdet.</ul>Om `datasetId` anger en enskild datauppsättning måste varje entitet under `identities` använda samma identitetsnamnutrymme som schemats primära identitet.<br><br>Om `datasetId` är `ALL` begränsas inte arrayen `identities` till ett enda namnutrymme eftersom varje datauppsättning kan vara olika. Dina förfrågningar är dock fortfarande begränsade till de namnutrymmen som är tillgängliga för din organisation, vilket rapporteras av [identitetstjänsten](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar informationen om postborttagningen.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | ID:t för raderingsordern. Detta kan användas för att senare slå upp borttagningsstatus. |
| `orgId` | Ditt organisations-ID. |
| `bundleId` | ID:t för det paket som den här borttagningsordern är kopplad till, används för felsökning. Flera raderingsorder paketeras ihop för att behandlas av tjänster i senare led. |
| `action` | Den åtgärd som utförs av arbetsordern. För postborttagningar är värdet `identity-delete`. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `updatedAt` | En tidsstämpel som anger när raderingsordningen senast uppdaterades. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |
| `datasetId` | ID:t för den datauppsättning som är föremål för begäran. Om begäran gäller alla datauppsättningar anges värdet till `ALL`. |

{style="table-layout:auto"}

## Hämta status för en postborttagning {#lookup}

När du har [skapat en begäran om postborttagning](#create) kan du kontrollera dess status med en GET-begäran.

**API-format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | `workorderId` för den post som du letar upp tas bort. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar information om borttagningsåtgärden, inklusive dess aktuella status.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | ID:t för raderingsordern. Detta kan användas för att senare slå upp borttagningsstatus. |
| `orgId` | Ditt organisations-ID. |
| `bundleId` | ID:t för det paket som den här borttagningsordern är kopplad till, används för felsökning. Flera raderingsorder paketeras ihop för att behandlas av tjänster i senare led. |
| `action` | Den åtgärd som utförs av arbetsordern. För postborttagningar är värdet `identity-delete`. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `updatedAt` | En tidsstämpel som anger när raderingsordningen senast uppdaterades. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |
| `datasetId` | ID:t för den datauppsättning som är föremål för begäran. Om begäran gäller alla datauppsättningar anges värdet till `ALL`. |
| `productStatusDetails` | En array som visar den aktuella statusen för processer som är relaterade till begäran. Varje arrayobjekt innehåller följande egenskaper:<ul><li>`productName`: Namnet på den underordnade tjänsten.</li><li>`productStatus`: Den aktuella bearbetningsstatusen för begäran från den underordnade tjänsten.</li><li>`createdAt`: En tidsstämpel som anger när den senaste statusen bokfördes av tjänsten.</li></ul> |

## Uppdatera en begäran om radering av post

Du kan uppdatera `displayName` och `description` för en postborttagning genom att göra en PUT-begäran.

**API-format**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | `workorderId` för den post som du letar upp tas bort. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `displayName` | Ett uppdaterat visningsnamn för postborttagningsbegäran. |
| `description` | En uppdaterad beskrivning av postborttagningsbegäran. |

{style="table-layout:auto"}

**Svar**

Ett godkänt svar returnerar informationen om postborttagningen.

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
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
| --- | --- |
| `workorderId` | ID:t för raderingsordern. Detta kan användas för att senare slå upp borttagningsstatus. |
| `orgId` | Ditt organisations-ID. |
| `bundleId` | ID:t för det paket som den här borttagningsordern är kopplad till, används för felsökning. Flera raderingsorder paketeras ihop för att behandlas av tjänster i senare led. |
| `action` | Den åtgärd som utförs av arbetsordern. För postborttagningar är värdet `identity-delete`. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `updatedAt` | En tidsstämpel som anger när raderingsordningen senast uppdaterades. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |
| `datasetId` | ID:t för den datauppsättning som är föremål för begäran. Om begäran gäller alla datauppsättningar anges värdet till `ALL`. |
| `productStatusDetails` | En array som visar den aktuella statusen för processer som är relaterade till begäran. Varje arrayobjekt innehåller följande egenskaper:<ul><li>`productName`: Namnet på den underordnade tjänsten.</li><li>`productStatus`: Den aktuella bearbetningsstatusen för begäran från den underordnade tjänsten.</li><li>`createdAt`: En tidsstämpel som anger när den senaste statusen bokfördes av tjänsten.</li></ul> |

{style="table-layout:auto"}
