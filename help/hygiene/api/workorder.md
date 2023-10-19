---
title: API-slutpunkt för arbetsorder
description: Med slutpunkten /workorder i Data Hygiene API kan du programmässigt hantera borttagningsåtgärder för identiteter.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 6e97b3a6b3830cf88802a8dd89944b6ce8791f02
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 0%

---

# [!BADGE Beta]{type=Informative} Slutpunkt för arbetsorder {#work-order-endpoint}

The `/workorder` -slutpunkten i Data Hygiene API gör att du kan hantera begäranden om postborttagning i Adobe Experience Platform programmässigt.

>[!IMPORTANT]
> 
>Funktionen Ta bort post är för närvarande i betaversionen och endast tillgänglig i en **begränsad release**. Det är inte tillgängligt för alla kunder. Begäranden om postborttagning är bara tillgängliga för organisationer i den begränsade versionen.
>
>Borttagning av poster ska användas för datarensning, borttagning av anonyma data eller datamängning. De är **not** som ska användas för förfrågningar om registrerade rättigheter (överensstämmelse) som rör sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). För all användning av regelefterlevnad [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Innan du fortsätter bör du granska [översikt](./overview.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Skapa en begäran om postborttagning {#create}

Du kan ta bort en eller flera identiteter från en enskild datauppsättning eller alla datauppsättningar genom att göra en POST-förfrågan till `/workorder` slutpunkt.

>[!IMPORTANT]
> 
>Det finns olika gränser för det totala antalet unika ID-postborttagningar som kan skickas varje månad. Dessa begränsningar baseras på ditt licensavtal. Organisationer som har köpt alla utgåvor av Adobe Real-time Customer Data Platform och Adobe Journey Optimizer kan skicka in upp till 100 000 identitetspostborttagningar varje månad. Organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield** kan skicka in upp till 600 000 identitetsposter som tas bort varje månad.<br>En enstaka [posta borttagningsbegäran via användargränssnittet](../ui/record-delete.md) kan du skicka 10 000 ID:n åt gången. API-metoden för att ta bort poster tillåter att 100 000 ID:n skickas samtidigt.<br>Det är en god vana att skicka så många ID:n som möjligt per begäran, upp till din ID-gräns. Om du tänker ta bort en stor mängd ID:n bör du inte skicka in en låg volym eller ett enda ID per postborttagningsbegäran.

**API-format**

```http
POST /workorder
```

**Begäran**

Beroende på värdet på `datasetId` som anges i nyttolasten för begäran tar API-anropet bort identiteter från alla datauppsättningar eller en enskild datauppsättning som du anger. Följande begäran tar bort tre identiteter från en specifik datauppsättning.

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
| `action` | Den åtgärd som ska utföras. Värdet måste anges till `delete_identity` för radering av poster. |
| `datasetId` | Om du tar bort från en enskild datauppsättning måste det här värdet vara ID:t för datauppsättningen i fråga. Om du tar bort från alla datauppsättningar anger du värdet till `ALL`.<br><br>Om du anger en enskild datauppsättning måste datamängdens associerade XDM-schema (Experience Data Model) ha en primär identitet definierad. |
| `displayName` | Visningsnamnet för postborttagningsbegäran. |
| `description` | En beskrivning av postborttagningsbegäran. |
| `identities` | En array som innehåller identiteterna för minst en användare vars information du vill ta bort. Varje identitet består av en [namnutrymme för identitet](../../identity-service/namespaces.md) och ett värde:<ul><li>`namespace`: Innehåller en enda strängegenskap, `code`, som representerar identitetsnamnutrymmet. </li><li>`id`: Identitetsvärdet.</ul>If `datasetId` anger en enda datauppsättning, varje enhet under `identities` måste använda samma identitetsnamnutrymme som schemats primära identitet.<br><br>If `datasetId` är inställd på `ALL`, `identities` arrayen är inte begränsad till ett enda namnutrymme eftersom varje datamängd kan vara olika. Dina förfrågningar är dock fortfarande begränsade till de namnutrymmen som är tillgängliga för din organisation, enligt rapporter från [Identitetstjänst](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

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

## Hämta status för en postborttagning (#lookup)

Efter [skapa en postborttagningsbegäran](#create)kan du kontrollera status med hjälp av en GET-förfrågan.

**API-format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | The `workorderId` av den post som du letar upp. |

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

Du kan uppdatera `displayName` och `description` om du vill ta bort en post genom att göra en PUT-begäran.

**API-format**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | The `workorderId` av den post som du letar upp. |

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
| `bundleId` | ID:t för det paket som den här borttagningsordern är kopplad till, används för felsökning. Flera raderingsorder paketeras ihop för att behandlas av tjänster i senare led. |
| `action` | Den åtgärd som utförs av arbetsordern. För postborttagningar är värdet `identity-delete`. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `updatedAt` | En tidsstämpel som anger när raderingsordningen senast uppdaterades. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |
| `datasetId` | ID:t för den datauppsättning som är föremål för begäran. Om begäran gäller alla datauppsättningar anges värdet till `ALL`. |
| `productStatusDetails` | En array som visar den aktuella statusen för processer som är relaterade till begäran. Varje arrayobjekt innehåller följande egenskaper:<ul><li>`productName`: Namnet på den underordnade tjänsten.</li><li>`productStatus`: Den aktuella bearbetningsstatusen för begäran från den underordnade tjänsten.</li><li>`createdAt`: En tidsstämpel som anger när den senaste statusen bokfördes av tjänsten.</li></ul> |

{style="table-layout:auto"}
