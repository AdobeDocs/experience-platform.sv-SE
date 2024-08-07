---
title: API-slutpunkt för arbetsorder
description: Med slutpunkten /workorder i Data Hygiene API kan du programmässigt hantera borttagningsåtgärder för identiteter.
badgeBeta: label="Beta" type="Informative"
role: Developer
badge: Beta
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: bf819d506b0ee6f3aba6850f598ee46f16695dfa
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# Slutpunkt för arbetsorder {#work-order-endpoint}

Med slutpunkten `/workorder` i API:t för datahygien kan du programmässigt hantera begäranden om postborttagning i Adobe Experience Platform.

>[!IMPORTANT]
> 
>Funktionen Ta bort post finns för närvarande i Beta och är endast tillgänglig i en **begränsad version**. Det är inte tillgängligt för alla kunder. Begäranden om postborttagning är bara tillgängliga för organisationer i den begränsade versionen.
>
>Borttagning av poster ska användas för datarensning, borttagning av anonyma data eller datamängning. De **får inte** användas för förfrågningar om rättigheter för registrerade (efterlevnad) som gäller sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). Använd [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället för alla kompatibilitetsfall.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Innan du fortsätter bör du gå igenom [översikten](./overview.md) och se om det finns länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anrop i det här dokumentet samt viktig information om vilka huvuden som krävs för att anropa ett Experience Platform-API.

## Skapa en begäran om postborttagning {#create}

Du kan ta bort en eller flera identiteter från en enskild datauppsättning eller alla datauppsättningar genom att göra en POST-förfrågan till slutpunkten `/workorder`.

>[!IMPORTANT]
> 
>Det finns olika gränser för det totala antalet unika ID-postborttagningar som kan skickas varje månad. Dessa begränsningar baseras på ditt licensavtal. Organisationer som har köpt alla utgåvor av Adobe Real-time Customer Data Platform och Adobe Journey Optimizer kan skicka in upp till 100 000 identitetspostborttagningar varje månad. Organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield** kan skicka in upp till 600 000 identitetspostborttagningar varje månad.<br>En enstaka [begäran om borttagning av post via användargränssnittet](../ui/record-delete.md) gör att du kan skicka 10 000 ID:n åt gången. API-metoden för att ta bort poster tillåter att 100 000 ID:n skickas samtidigt.<br>Det är bäst att skicka så många ID:n som möjligt per begäran, upp till din ID-gräns. Om du tänker ta bort en stor mängd ID:n bör du inte skicka in en låg volym eller ett enda ID per postborttagningsbegäran.

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

När du har [skapat en begäran om postborttagning](#create) kan du kontrollera dess status med hjälp av en GET-begäran.

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
