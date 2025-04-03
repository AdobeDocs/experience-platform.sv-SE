---
title: Gruppsegmenteringshandbok
description: Lär dig mer om gruppsegmentering, inklusive vad det är, hur du skapar en målgrupp som utvärderas med batchsegmentering och hur du visar målgrupper som skapats med batchsegmentering.
exl-id: b6fba2fb-8eec-4429-92fd-ece5c79d379d
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Gruppsegmenteringsguide

Gruppsegmentering är en metod för segmenteringsutvärdering som gör att du kan flytta alla profildata samtidigt för att skapa motsvarande målgrupper.

Med gruppsegmentering kan ni skapa detaljerade och detaljerade målgrupper och köra segmenteringsjobb för att avgöra när ni vill att dessa data ska spridas till tjänster längre fram i kedjan.

## Berättigade frågetyper {#query-types}

Alla frågor kan gruppsegmenteras.

## Skapa målgrupper {#create-audience}

Du kan skapa en målgrupp som utvärderas med batchsegmentering med hjälp av segmenteringstjänstens API eller genom målgruppsportalen i användargränssnittet.

>[!BEGINTABS]

>[!TAB Segmenteringstjänstens API]

**API-format**

```http
POST /segment/definitions
```

**Begäran**

+++ En exempelbegäran om att skapa en segmentdefinition som är aktiverad för batchsegmentering

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": true
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den segmentdefinition du nyss skapade.

+++Ett exempelsvar när du skapar en segmentdefinition.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

Mer information om hur du använder den här slutpunkten finns i [segmentdefinitionsguiden](../api/segment-definitions.md).

>[!TAB Målgruppsportal]

Välj **[!UICONTROL Create audience]** i Audience Portal.

![Knappen Skapa målgrupp är markerad i målgruppsportalen.](../images/methods/batch/select-create-audience.png)

En pover visas. Välj **[!UICONTROL Build rules]** om du vill ange Segment Builder.

![Knappen Skapa regler markeras i porten för att skapa målgrupper.](../images/methods/batch/select-build-rules.png)

När du har skapat segmentdefinitionen väljer du **[!UICONTROL Batch]** som **[!UICONTROL Evaluation method]**.

![Segmentdefinitionen visas. Utvärderingstypen är markerad och visar att segmentdefinitionen kan utvärderas med hjälp av direktuppspelningssegmentering.](../images/methods/batch/batch-evaluation-method.png)

Mer information om hur du skapar segmentdefinitioner finns i guiden [Segment Builder](../ui/segment-builder.md)

>[!ENDTABS]

## Hämta målgrupper {#retrieve-audiences}

Du kan hämta alla målgrupper som utvärderas med batchsegmentering med hjälp av segmenteringstjänstens API eller genom målgruppsportalen i användargränssnittet.

>[!BEGINTABS]

>[!TAB Segmenteringstjänstens API]

Hämta en lista över alla segmentdefinitioner som har utvärderats med batchsegmentering i organisationen genom att göra en GET-begäran till slutpunkten `/segment/definitions`.

**API-format**

Du måste inkludera frågeparametern `evaluationInfo.batch.enabled=true` i sökvägen för begäran för att hämta segmentdefinitioner som utvärderats med gruppsegmentering.

```http
GET /segment/definitions?evaluationInfo.batch.enabled=true
```

**Begäran**

+++ En exempelbegäran om att lista alla gruppaktiverade segmentdefinitioner

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.batch.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en array med segmentdefinitioner i organisationen som utvärderas med gruppsegmentering.

+++Ett exempelsvar som innehåller en lista med alla segmentdefinitioner som utvärderas i grupp för gruppsegmentering i din organisation

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

Mer detaljerad information om den returnerade segmentdefinitionen finns i [stödlinjen för segmentdefinitioner](../api/segment-definitions.md).

+++

>[!TAB Målgruppsportal]

Du kan hämta alla målgrupper som har aktiverats för batchsegmentering inom organisationen med hjälp av filter i Audience Portal. Välj ![filterikonen](../../images/icons/filter.png) för att visa filterlistan.

![Filterikonen är markerad i målportalen.](../images/methods/filter-audiences.png)

Gå till **[!UICONTROL Update frequency]** och välj [!UICONTROL Batch] inom de tillgängliga filtren. När du använder det här filtret visas alla målgrupper i organisationen som utvärderas med batchsegmentering.

![Frekvensen för batchuppdatering är markerad och visar alla målgrupper i organisationen som utvärderas med batchsegmentering.](../images/methods/batch/filter-batch.png)

Om du vill veta mer om hur du visar målgrupper i Experience Platform kan du läsa [guiden för målportalen](../ui/audience-portal.md).

>[!ENDTABS]

## Nästa steg

I den här guiden beskrivs hur du skapar en segmentdefinition som kan utvärderas med gruppsegmentering i Adobe Experience Platform.

Läs [Användarhandboken för segmentering](../ui/overview.md) om du vill veta mer om hur du använder användargränssnittet i Experience Platform.

Vanliga frågor om gruppsegmentering finns i avsnittet [gruppsegmentering i Frågor och svar](../faq.md#batch-segmentation).
