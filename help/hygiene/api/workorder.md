---
title: API-slutpunkt för arbetsorder
description: Med slutpunkten /workorder i Data Hygiene API kan du programmässigt hantera borttagningsåtgärder för konsumentidentiteter.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---

# Slutpunkt för arbetsorder

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt skölden.

The `/workorder` -slutpunkten i Data Hygiene API gör att du kan hantera borttagningsåtgärder för konsumentidentiteter i Adobe Experience Platform programmatiskt.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Läs igenom [översikt](./overview.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Ta bort identiteter {#delete-identities}

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
| `action` | Den åtgärd som ska utföras. Värdet måste anges till `delete_identity` när identiteter tas bort. |
| `datasetId` | Om du tar bort från en enskild datauppsättning måste det här värdet vara ID:t för datauppsättningen i fråga. Om du tar bort från alla datauppsättningar anger du värdet till `ALL`.<br><br>Om du anger en enskild datauppsättning måste datamängdens associerade XDM-schema (Experience Data Model) ha en primär identitet definierad. |
| `identities` | En array som innehåller identiteterna för minst en användare vars information du vill ta bort. Varje identitet består av en [identity namespace](../../identity-service/namespaces.md) och ett värde:<ul><li>`namespace`: Innehåller en enda strängegenskap, `code`, som representerar identitetsnamnutrymmet. </li><li>`id`: Identitetsvärdet.</ul>If `datasetId` anger en enda datauppsättning, varje enhet under `identities` måste använda samma identitetsnamnutrymme som schemats primära identitet.<br><br>If `datasetId` är inställd på `ALL`, `identities` arrayen är inte begränsad till ett enda namnutrymme eftersom varje datamängd kan vara olika. Dina förfrågningar är dock fortfarande begränsade till de namnutrymmen som är tillgängliga för din organisation, enligt rapporter från [Identitetstjänst](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett godkänt svar returnerar information om identitetsborttagningen.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | ID:t för raderingsordern. Detta kan användas för att senare slå upp borttagningsstatus. |
| `orgId` | Organisationens ID. |
| `batchId` | ID:t för gruppen som den här borttagningsordern är associerad med, används för felsökning. Flera raderingsorder paketeras i en batch som ska bearbetas av tjänster i senare led. |
| `bundleOrdinal` | Den ordning som borttagningsordern togs emot i när den paketerades i en batch för bearbetning i efterföljande led. Används för felsökning. |
| `payloadByteSize` | Storleken, i byte, på listan över identiteter som angavs i den begärandenyttolast som skapade den här borttagningsordern. |
| `operationCount` | Antalet identiteter som den här raderingsordningen gäller för. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `responseMessage` | Det senaste svaret som returnerades av systemet. Om ett fel inträffar under bearbetningen är det här värdet en JSON-sträng som innehåller detaljerad felinformation som hjälper dig förstå vad som kan ha gått fel. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |

{style=&quot;table-layout:auto&quot;}

## Visa statusvärden för alla identitetsborttagningar {#list}

Du kan visa statusvärden för alla identitetsborttagningar genom att göra en GET-förfrågan.

**API-format**

```http
GET /workorder?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMS}` | En lista med valfria frågeparametrar för listanropet, med flera parametrar avgränsade med `&` tecken. Godkända frågeparametrar är följande:<ul><li>`data` - ett booleskt värde som, när det anges till `true`, innehåller alla ytterligare begärande- och svarsdata som tagits emot för raderingsordern. Standardvärdet är `false`.</li><li>`start` - En tidsstämpel för början av tidsramen för att söka efter raderingsorder.</li><li>`end` - En tidsstämpel för slutet av tidsramen för att söka efter raderingsorder.</li><li>`page` - Den specifika svarssidan som ska returneras.</li><li>`limit` - antalet poster som ska visas per sida.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar information om alla borttagningsåtgärder, inklusive deras aktuella status. Exemplet nedan har trunkerats för blanksteg.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `results` | Innehåller en lista med raderingsorder och deras information. Mer information om egenskaperna för en borttagningsordning finns i exempelsvaret i avsnittet om [söka efter en raderingsordning](#lookup). |
| `total` | Det totala antalet raderingsorder som hittades baserat på aktuella filter. |
| `count` | Det totala antalet raderingsorder som finns på varje sida i svaret. |
| `_links` | Innehåller sidnumreringsinformation som hjälper dig att utforska resten av svaret:<ul><li>`next`: Innehåller en URL för nästa sida i svaret.</li><li>`page`: Innehåller en URL-mall för att komma åt en annan sida i svaret eller justera antalet objekt som returneras på varje sida.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Hämta status för en identitetsborttagning (#lookup)

När en begäran har skickats till [ta bort en identitet](#delete-identities)kan du kontrollera status med hjälp av en GET-förfrågan.

**API-format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{WORK_ORDER_ID}` | The `workorderId` av identitetsborttagningen som du letar efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar information om borttagningsåtgärden, inklusive dess aktuella status.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | ID:t för raderingsordern. Detta kan användas för att senare slå upp borttagningsstatus. |
| `orgId` | Organisationens ID. |
| `batchId` | ID:t för gruppen som den här borttagningsordern är associerad med, används för felsökning. Flera raderingsorder paketeras i en batch som ska bearbetas av tjänster i senare led. |
| `bundleOrdinal` | Den ordning som borttagningsordern togs emot i när den paketerades i en batch för bearbetning i efterföljande led. Används för felsökning. |
| `payloadByteSize` | Storleken, i byte, på listan över identiteter som angavs i den begärandenyttolast som skapade den här borttagningsordern. |
| `operationCount` | Antalet identiteter som den här raderingsordningen gäller för. |
| `createdAt` | En tidsstämpel som anger när raderingsordningen skapades. |
| `responseMessage` | Det senaste svaret som returnerades av systemet. Om ett fel inträffar under bearbetningen är det här värdet en JSON-sträng som innehåller detaljerad felinformation som hjälper dig förstå vad som kan ha gått fel. |
| `status` | Den aktuella statusen för borttagningsordern. |
| `createdBy` | Användaren som skapade borttagningsordningen. |
