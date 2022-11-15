---
title: API-slutpunkt för arbetsorder
description: Med slutpunkten /workorder i Data Hygiene API kan du programmässigt hantera borttagningsåtgärder för konsumentidentiteter.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 7679de9d30c00873b279c5315aa652870d8c34fd
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Slutpunkt för arbetsorder

The `/workorder` -slutpunkten i API:t för datahygien gör att du kan hantera konsumentborttagningsbegäranden i Adobe Experience Platform programmatiskt.

>[!IMPORTANT]
>
>Förfrågningar om borttagning av kund är bara tillgängliga för organisationer som har köpt **Adobe Healthcare Shield**.
>
>
>Konsumentborttagningar är avsedda att användas för datarensning, borttagning av anonyma data eller datamängning. De är **not** som ska användas för förfrågningar om registrerade rättigheter (överensstämmelse) som rör sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). För all användning av regelefterlevnad [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Läs igenom [översikt](./overview.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Skapa en begäran om att ta bort en kund {#delete-consumers}

Du kan ta bort en eller flera konsumentidentiteter från en enskild datauppsättning eller alla datauppsättningar genom att göra en POST-förfrågan till `/workorder` slutpunkt.

**API-format**

```http
POST /workorder
```

**Begäran**

Beroende på värdet på `datasetId` som anges i nyttolasten för begäran tar API-anropet bort konsumentidentiteter från alla datauppsättningar eller en enda datauppsättning som du anger. Följande begäran tar bort tre konsumentidentiteter från en specifik datauppsättning.

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
        "displayName": "Example Consumer Delete Request",
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
| `action` | Den åtgärd som ska utföras. Värdet måste anges till `delete_identity` för konsumentborttagningar. |
| `datasetId` | Om du tar bort från en enskild datauppsättning måste det här värdet vara ID:t för datauppsättningen i fråga. Om du tar bort från alla datauppsättningar anger du värdet till `ALL`.<br><br>Om du anger en enskild datauppsättning måste datamängdens associerade XDM-schema (Experience Data Model) ha en primär identitet definierad. |
| `displayName` | Visningsnamnet för konsumentborttagningsbegäran. |
| `description` | En beskrivning av konsumentborttagningsbegäran. |
| `identities` | En array som innehåller identiteterna för minst en användare vars information du vill ta bort. Varje identitet består av en [identity namespace](../../identity-service/namespaces.md) och ett värde:<ul><li>`namespace`: Innehåller en enda strängegenskap, `code`, som representerar identitetsnamnutrymmet. </li><li>`id`: Identitetsvärdet.</ul>If `datasetId` anger en enda datauppsättning, varje enhet under `identities` måste använda samma identitetsnamnutrymme som schemats primära identitet.<br><br>If `datasetId` är inställd på `ALL`, `identities` arrayen är inte begränsad till ett enda namnutrymme eftersom varje datamängd kan vara olika. Dina förfrågningar är dock fortfarande begränsade till de namnutrymmen som är tillgängliga för din organisation, enligt rapporter från [Identitetstjänst](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett godkänt svar returnerar information om konsumentborttagningen.

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
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | ID:t för raderingsordern. Detta kan användas för att senare slå upp borttagningsstatus. |
| `orgId` | Ditt organisations-ID. |
| `bundleId` | ID:t för paketet som den här borttagningsordern är kopplad till, används för felsökning. Flera raderingsorder paketeras ihop för att behandlas av tjänster i senare led. |
| `action` | Den åtgärd som utförs av arbetsordern. För konsumentborttagningar är värdet `identity-delete`. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `updatedAt` | En tidsstämpel som anger när raderingsordningen senast uppdaterades. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |
| `datasetId` | ID:t för den datauppsättning som är föremål för begäran. Om begäran gäller alla datauppsättningar anges värdet till `ALL`. |

{style=&quot;table-layout:auto&quot;}

## Hämta status för en konsumentborttagning (#lookup)

Efter [skapa en begäran om att ta bort en kund](#delete-consumers)kan du kontrollera status med hjälp av en GET-förfrågan.

**API-format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | The `workorderId` av den kund som du letar upp. |

{style=&quot;table-layout:auto&quot;}

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
  "displayName": "Example Consumer Delete Request",
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
| `bundleId` | ID:t för paketet som den här borttagningsordern är kopplad till, används för felsökning. Flera raderingsorder paketeras ihop för att behandlas av tjänster i senare led. |
| `action` | Den åtgärd som utförs av arbetsordern. För konsumentborttagningar är värdet `identity-delete`. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `updatedAt` | En tidsstämpel som anger när raderingsordningen senast uppdaterades. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |
| `datasetId` | ID:t för den datauppsättning som är föremål för begäran. Om begäran gäller alla datauppsättningar anges värdet till `ALL`. |
| `productStatusDetails` | En array som visar den aktuella statusen för processer som är relaterade till begäran. Varje arrayobjekt innehåller följande egenskaper:<ul><li>`productName`: Namnet på den underordnade tjänsten.</li><li>`productStatus`: Aktuell bearbetningsstatus för begäran från den underordnade tjänsten.</li><li>`createdAt`: En tidsstämpel som anger när den senaste statusen bokfördes av tjänsten.</li></ul> |

## Uppdatera en begäran om att ta bort en kund

Du kan uppdatera `displayName` och `description` för en konsument ta bort genom att göra en PUT-förfrågan.

**API-format**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | The `workorderId` av den kund som du letar upp. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
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
| `displayName` | Ett uppdaterat visningsnamn för konsumentborttagningsbegäran. |
| `description` | En uppdaterad beskrivning av konsumentborttagningsbegäran. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett godkänt svar returnerar information om konsumentborttagningen.

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
  "displayName" : "Update - displayName",
  "description" : "Update - description",
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
| `bundleId` | ID:t för paketet som den här borttagningsordern är kopplad till, används för felsökning. Flera raderingsorder paketeras ihop för att behandlas av tjänster i senare led. |
| `action` | Den åtgärd som utförs av arbetsordern. För konsumentborttagningar är värdet `identity-delete`. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `updatedAt` | En tidsstämpel som anger när raderingsordningen senast uppdaterades. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |
| `datasetId` | ID:t för den datauppsättning som är föremål för begäran. Om begäran gäller alla datauppsättningar anges värdet till `ALL`. |
| `productStatusDetails` | En array som visar den aktuella statusen för processer som är relaterade till begäran. Varje arrayobjekt innehåller följande egenskaper:<ul><li>`productName`: Namnet på den underordnade tjänsten.</li><li>`productStatus`: Aktuell bearbetningsstatus för begäran från den underordnade tjänsten.</li><li>`createdAt`: En tidsstämpel som anger när den senaste statusen bokfördes av tjänsten.</li></ul> |

{style=&quot;table-layout:auto&quot;}
