---
title: Målgrupps-API-slutpunkt
description: Använd målgruppsslutpunkten i Adobe Experience Platform Segmentation Service API för att skapa, hantera och uppdatera målgrupper för er organisation programmatiskt.
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 914174de797d7d5f6c47769d75380c0ce5685ee2
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 0%

---

# Målgruppsslutpunkt

En publik är en samling personer som har liknande beteenden och/eller egenskaper. Dessa samlingar med personer kan genereras antingen med Adobe Experience Platform eller från externa källor. Du kan använda slutpunkten `/audiences` i segmenterings-API:t, som gör att du kan hämta, skapa, uppdatera och ta bort målgrupper med programkod.

## Komma igång

Slutpunkterna som används i den här guiden ingår i [!DNL Adobe Experience Platform Segmentation Service]-API:t. Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med målgrupper {#list}

Du kan hämta en lista över alla målgrupper för din organisation genom att göra en GET-förfrågan till slutpunkten `/audiences`.

**API-format**

Slutpunkten `/audiences` har stöd för flera frågeparametrar som kan hjälpa dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader när du listar resurser. Om du anropar den här slutpunkten utan parametrar hämtas alla målgrupper som är tillgängliga för din organisation. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

Följande frågeparametrar kan användas när en lista över målgrupper hämtas:

| Frågeparameter | Beskrivning | Exempel |
| --------------- | ----------- | ------- |
| `start` | Anger startförskjutningen för de returnerade målgrupperna. | `start=5` |
| `limit` | Anger det maximala antalet målgrupper som returneras per sida. | `limit=10` |
| `sort` | Anger den ordning som resultaten ska sorteras efter. Detta skrivs i formatet `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Ett filter som gör att du kan ange målgrupper som **exakt** matchar ett attributvärde. Detta skrivs i formatet `property=` | `property=audienceId==test-audience-id` |
| `name` | Ett filter som gör att du kan ange målgrupper vars namn **innehåller** det angivna värdet. Det här värdet är inte skiftlägeskänsligt. | `name=Sample` |
| `description` | Ett filter som gör att du kan ange målgrupper vars beskrivningar **innehåller** det angivna värdet. Det här värdet är inte skiftlägeskänsligt. | `description=Test Description` |

**Begäran**

Följande begäran hämtar de två sista målgrupperna som skapats i din organisation.

+++En exempelbegäran om att hämta en lista över målgrupper.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över målgrupper som skapats i din organisation som JSON.

+++Ett exempelsvar som innehåller de två senast skapade målgrupperna som tillhör din organisation

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "pageSize": 2,
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| Egenskap | Målgruppstyp | Beskrivning |
| -------- | ------------- | ----------- | 
| `id` | Båda | En systemgenererad skrivskyddad identifierare för målgruppen. |
| `audienceId` | Båda | Om målgruppen är en plattformsgenererad målgrupp är detta samma värde som `id`. Om målgruppen genereras externt anges det här värdet av klienten. |
| `schema` | Båda | Målgruppens XDM-schema (Experience Data Model). |
| `imsOrgId` | Båda | ID för organisationen som målgruppen tillhör. |
| `sandbox` | Båda | Information om sandlådan som målgruppen tillhör. Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md). |
| `name` | Båda | Namnet på publiken. |
| `description` | Båda | En beskrivning av publiken. |
| `expression` | Plattformsgenererad | Målgruppens Profile Query Language-uttryck (PQL). Mer information om PQL-uttryck finns i [handboken för PQL-uttryck](../pql/overview.md). |
| `mergePolicyId` | Plattformsgenererad | ID:t för den sammanfogningsprincip som målgruppen är kopplad till. Mer information om sammanfogningsprinciper finns i [guiden för sammanfogningsprinciper](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Plattformsgenererad | Visar hur målgruppen kommer att utvärderas. Möjliga utvärderingsmetoder är batch, synkron (direktuppspelning) eller kontinuerlig (kant). Mer information om utvärderingsmetoderna finns i [segmenteringsöversikten](../home.md) |
| `dependents` | Båda | En array med målgrupps-ID som är beroende av den aktuella målgruppen. Detta används om du skapar en målgrupp som är ett segment i ett segment. |
| `dependencies` | Båda | En array med målgrupps-ID:n som målgruppen är beroende av. Detta används om du skapar en målgrupp som är ett segment i ett segment. |
| `type` | Båda | Ett systemgenererat fält som visar om publiken genereras av plattformen eller är en externt genererad publik. Möjliga värden är `SegmentDefinition` och `ExternalSegment`. En `SegmentDefinition` refererar till en målgrupp som har skapats i Platform, medan en `ExternalSegment` refererar till en målgrupp som inte har genererats i Platform. |
| `originName` | Båda | Ett fält som refererar till namnet på målgruppens ursprung. För plattformsgenererade målgrupper är det här värdet `REAL_TIME_CUSTOMER_PROFILE`. För målgrupper som genereras i Audience Orchestration är det här värdet `AUDIENCE_ORCHESTRATION`. För målgrupper som genereras i Adobe Audience Manager är det här värdet `AUDIENCE_MANAGER`. För andra externt genererade målgrupper blir det här värdet `CUSTOM_UPLOAD`. |
| `createdBy` | Båda | ID för den användare som skapade målgruppen. |
| `labels` | Båda | Dataanvändning på objektnivå och attributbaserade etiketter för åtkomstkontroll som är relevanta för publiken. |
| `namespace` | Båda | Det namnutrymme som målgruppen tillhör. Möjliga värden är `AAM`, `AAMSegments`, `AAMTraits` och `AEPSegments`. |
| `linkedAudienceRef` | Båda | Ett objekt som innehåller identifierare för andra målgruppsrelaterade system. |

+++

## Skapa en ny målgrupp {#create}

Du kan skapa en ny målgrupp genom att göra en POST-förfrågan till slutpunkten `/audiences`.

**API-format**

```http
POST /audiences
```

**Begäran**

>[!BEGINTABS]

>[!TAB Plattformsgenererad publik]

+++ Ett exempel på en förfrågan om att skapa en plattformsgenererad publik

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `name` | Namnet på publiken. |
| `description` | En beskrivning av publiken. |
| `type` | Ett fält som visar om målgruppen är plattformsgenererad eller är en externt genererad målgrupp. Möjliga värden är `SegmentDefinition` och `ExternalSegment`. En `SegmentDefinition` refererar till en målgrupp som har skapats i Platform, medan en `ExternalSegment` refererar till en målgrupp som inte har genererats i Platform. |
| `expression` | Målgruppens Profile Query Language-uttryck (PQL). Mer information om PQL-uttryck finns i [handboken för PQL-uttryck](../pql/overview.md). |
| `schema` | Målgruppens XDM-schema (Experience Data Model). |
| `labels` | Dataanvändning på objektnivå och attributbaserade etiketter för åtkomstkontroll som är relevanta för publiken. |

+++

>[!TAB Externt genererad publik]

+++ En exempelbegäran för att skapa en externt genererad publik

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "audienceId":"test-external-audience-id",
        "name":"externalAudience",
        "namespace":"aam",
        "description":"Last 30 days",
        "type":"ExternalSegment",
        "originName":"CUSTOM_UPLOAD",
        "lifecycleState":"published",
        "datasetId":"6254cf3c97f8e31b639fb14d",
        "labels":[
            "core/C1"
        ],
        "linkedAudienceRef":{
            "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `audienceId` | Ett användarangivet ID för målgruppen. |
| `name` | Namnet på publiken. |
| `namespace` | Namnutrymmet för målgruppen. |
| `description` | En beskrivning av publiken. |
| `type` | Ett fält som visar om målgruppen är plattformsgenererad eller är en externt genererad målgrupp. Möjliga värden är `SegmentDefinition` och `ExternalSegment`. En `SegmentDefinition` refererar till en målgrupp som har skapats i Platform, medan en `ExternalSegment` refererar till en målgrupp som inte har genererats i Platform. |
| `originName` | Namnet på målgruppens ursprung. För externt genererade målgrupper är standardvärdet `CUSTOM_UPLOAD`. Andra värden som stöds är `REAL_TIME_CUSTOMER_PROFILE`, `CUSTOM_UPLOAD`, `AUDIENCE_ORCHESTRATION` och `AUDIENCE_MATCH`. |
| `lifecycleState` | Ett valfritt fält som bestämmer det inledande tillståndet för den målgrupp du försöker skapa. Värden som stöds är `draft`, `published` och `inactive`. |
| `datasetId` | ID:t för datauppsättningen där data som omfattar målgruppen kan hittas. |
| `labels` | Dataanvändning på objektnivå och attributbaserade etiketter för åtkomstkontroll som är relevanta för publiken. |
| `audienceMeta` | Metadata som tillhör den externt genererade målgruppen. |
| `linkedAudienceRef` | Ett objekt som innehåller identifierare för andra målgruppsrelaterade system. Detta kan omfatta följande: <ul><li>`flowId`: Detta ID används för att ansluta målgruppen till det dataflöde som användes för att hämta målgruppsdata. Mer information om vilka ID:n som krävs finns i [Skapa en dataflödesguide](../../sources/tutorials/api/collect/cloud-storage.md).</li><li>`aoWorkflowId`: Detta ID används för att ansluta målgruppen till en relaterad publikorchestration-komposition.&lt;/li/> <li>`payloadFieldGroupRef`: Detta ID används för att referera till XDM-fältgruppsschemat som beskriver målgruppens struktur. Mer information om värdet för det här fältet finns i [stödlinjen för XDM-fältgruppsslutpunkten](../../xdm/api/field-groups.md).</li><li>`audienceFolderId`: Detta ID används för att referera till mapp-ID:t i Adobe Audience Manager för målgruppen. Mer information om detta API finns i [Adobe Audience Manager API-handboken](https://bank.demdex.com/portal/swagger/index.html#/Segment%20Folder%20API).</ul> |

+++

>[!ENDTABS]

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målgruppen.

>[!BEGINTABS]

>[!TAB Plattformsgenererad publik]

+++Ett exempelsvar när du skapar en plattformsgenererad publik.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB Externt genererad publik]

+++Ett exempelsvar när du skapar en externt genererad publik.

```json
{
   "id": "322f9f62-cd27-11ec-9d64-0242ac120002",
   "audienceId": "test-external-audience-id",
   "name": "externalAudience",
   "namespace": "aam",
   "imsOrgId": "{ORG_ID}",
   "sandbox":{
      "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
      "sandboxName": "prod",
      "type": "production",
      "default": true
   },
   "isSystem": false,
   "description": "Last 30 days",
   "type": "ExternalSegment",
   "originName": "CUSTOM_UPLOAD",
   "lifecycleState": "published",
   "createdBy": "{CREATED_BY_ID}",
   "datasetId": "6254cf3c97f8e31b639fb14d",
   "labels": [
      "core/C1"
   ],
   "linkedAudienceRef": {
      "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
   },
   "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
   "creationTime": 1650251290000,
   "updateEpoch": 1650251290,
   "updateTime": 1650251290000,
   "createEpoch": 1650251290
}
```

+++

## Söka efter en viss målgrupp {#get}

Du kan söka efter detaljerad information om en viss målgrupp genom att göra en GET-förfrågan till slutpunkten `/audiences` och ange ID:t för den målgrupp som du vill hämta i sökvägen för begäran.

**API-format**

```http
GET /audiences/{AUDIENCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | ID:t för den målgrupp du försöker hämta. Observera att det här är fältet `id` och att det **inte** är fältet `audienceId`. |

**Begäran**

+++En exempelbegäran för att hämta en målgrupp

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den angivna målgruppen. Svaret varierar beroende på om målgruppen genereras med Adobe Experience Platform eller externa källor.

>[!BEGINTABS]

>[!TAB Plattformsgenererad publik]

+++Ett exempelsvar när en plattformsgenererad publik hämtas.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB Externt genererad publik]

+++Ett samplingssvar när en externt genererad publik hämtas.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "test-external-audience-id",
    "name": "externalAudience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

>[!ENDTABS]

## Uppdatera ett fält i en målgrupp {#update-field}

Du kan uppdatera fälten för en viss målgrupp genom att göra en PATCH-begäran till slutpunkten `/audiences` och ange ID:t för den målgrupp som du vill uppdatera i sökvägen till begäran.

**API-format**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID:t för den målgrupp som du vill uppdatera. Observera att det här är fältet `id` och att det **inte** är fältet `audienceId`. |

**Begäran**

+++Ett exempel på en begäran om att uppdatera ett fält i en målgrupp.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `op` | För uppdatering av målgrupper är det här värdet alltid `add`. |
| `path` | Sökvägen till det fält som du vill uppdatera. |
| `value` | Värdet som du vill uppdatera fältet till. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nyligen uppdaterade målgruppen.

+++Ett exempelsvar när ett fält uppdateras i en målgrupp.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Uppdatera en målgrupp {#put}

Du kan uppdatera (skriva över) en viss målgrupp genom att göra en PUT-begäran till slutpunkten `/audiences` och ange ID:t för den målgrupp som du vill uppdatera i sökvägen till begäran.

**API-format**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID:t för den målgrupp som du vill uppdatera. Observera att det här är fältet `id` och att det **inte** är fältet `audienceId`. |

**Begäran**

+++Ett exempel på en förfrågan om att uppdatera en hel publik.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `audienceId` | Målgruppens ID. För externt genererade målgrupper kan det här värdet anges av användaren. |
| `name` | Namnet på publiken. |
| `namespace` | Namnutrymmet för målgruppen. |
| `description` | En beskrivning av publiken. |
| `type` | Ett systemgenererat fält som visar om publiken genereras av plattformen eller är en externt genererad publik. Möjliga värden är `SegmentDefinition` och `ExternalSegment`. En `SegmentDefinition` refererar till en målgrupp som har skapats i Platform, medan en `ExternalSegment` refererar till en målgrupp som inte har genererats i Platform. |
| `lifecycleState` | Publiken. Möjliga värden är `draft`, `published` och `inactive`. `draft` representerar när målgruppen skapas, `published` när målgruppen publiceras och `inactive` när målgruppen inte längre är aktiv. |
| `datasetId` | ID:t för datauppsättningen som målgruppsdata kan hittas. |
| `labels` | Dataanvändning på objektnivå och attributbaserade etiketter för åtkomstkontroll som är relevanta för publiken. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om din nya uppdaterade målgrupp. Observera att informationen om er målgrupp varierar beroende på om det är en plattformsgenererad publik eller en externt genererad målgrupp.

+++Ett exempelsvar när en hel publik uppdateras.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Ta bort en målgrupp {#delete}

Du kan ta bort en viss målgrupp genom att göra en DELETE-begäran till slutpunkten `/audiences` och ange ID:t för den målgrupp som du vill ta bort i sökvägen för begäran.

**API-format**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID för den målgrupp som du vill ta bort. Observera att det här är fältet `id` och att det **inte** är fältet `audienceId`. |

**Begäran**

+++ Ett exempel på begäran om att ta bort en målgrupp.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 204 utan något meddelande.

## Hämta flera målgrupper {#bulk-get}

Du kan hämta flera målgrupper genom att göra en begäran om POST till `/audiences/bulk-get`-slutpunkten och ange ID:n för de målgrupper som du vill hämta.

**API-format**

```http
POST /audiences/bulk-get
```

**Begäran**

+++ En exempelbegäran för hämtning av flera målgrupper.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 2007 med information om de begärda målgrupperna.

+++ Ett exempelsvar när du hämtar flera målgrupper.

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
         "evaluationInfo": {
            "batch": {
               "enabled": false
            },
            "continuous": {
               "enabled": true
            },
            "synchronous": {
               "enabled": false
            }
         },
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
         "dependents": [],
         "definedOn": [
            {
               "meta:resourceType": "unions",
               "meta:containerId": "tenant",
               "$ref": "https://ns.adobe.com/xdm/context/profile__union"
            }
         ],
         "dependencies": [],
         "type": "SegmentDefinition",
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++


## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur du skapar, hanterar och tar bort målgrupper med Adobe Experience Platform API. Mer information om målgruppshantering med användargränssnittet finns i [segmenteringsgränssnittsguiden](../ui/overview.md).
