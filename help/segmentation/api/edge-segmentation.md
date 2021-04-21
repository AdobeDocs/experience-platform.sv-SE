---
keywords: Experience Platform;hemindelning;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;kantsegmentering;Kantsegmentering;Strömningskant;
solution: Experience Platform
title: 'Kantsegmentering med API '
topic-legacy: developer guide
description: Det här dokumentet innehåller exempel på hur du använder kantsegmentering med Adobe Experience Platform Segmentation Service API.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Kantsegmentering (beta)

>[!NOTE]
>
>I följande dokument beskrivs hur du utför kantsegmentering med API:t. Mer information om kantsegmentering med användargränssnittet finns i [användargränssnittsguiden för kantsegmentering](../ui/edge-segmentation.md). Kantsegmentering är för närvarande en betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

Kantsegmentering är möjligheten att utvärdera segment i Adobe Experience Platform direkt, vilket möjliggör användning av samma sida och nästa sida vid personalisering.

## Komma igång

Den här utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform]-tjänster som är involverade i kantsegmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid, baserad på aggregerade data från flera källor.
- [[!DNL Segmentation]](../home.md): Ger möjlighet att skapa segment och målgrupper utifrån era  [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Platform] organiserar kundupplevelsedata.

Om du vill kunna ringa anrop till [!DNL Data Prep] API-slutpunkter läser du guiden [komma igång med plattforms-API:er](../../landing/api-guide.md) för att lära dig mer om obligatoriska rubriker och hur du läser exempel-API-anrop.

## Frågetyper för kantsegmentering {#query-types}

För att ett segment ska kunna utvärderas med hjälp av kantsegmentering måste frågan följa följande riktlinjer:

| Frågetyp | Detaljer |
| ---------- | ------- |
| Inkommande träff | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. |
| Inkommande träde som refererar till en profil | En segmentdefinition som refererar till en enda inkommande händelse, utan tidsbegränsning, och ett eller flera profilattribut. |
| Frekvensfråga | En segmentdefinition som refererar till en händelse som inträffar minst ett visst antal gånger. |
| Frekvensfråga som refererar till en profil | En segmentdefinition som refererar till en händelse som inträffar minst ett visst antal gånger och har ett eller flera profilattribut. |

{style=&quot;table-layout:auto&quot;}

Följande frågetyper är **inte** som för närvarande stöds av kantsegmentering:

| Frågetyp | Detaljer |
| ---------- | ------- |
| Fönster för relativ tid | Om en fråga refererar till ett tidsfönster kan den inte utvärderas med kantsegmentering. |
| Negation | Om en fråga innehåller en negation, eller en `not`-händelse, kan den inte utvärderas med kantsegmentering. |
| Flera händelser | Om en fråga innehåller mer än en händelse kan den inte utvärderas med kantsegmentering. |

{style=&quot;table-layout:auto&quot;}

## Hämta alla segment som är aktiverade för kantsegmentering

Du kan hämta en lista över alla segment som är aktiverade för kantsegmentering inom IMS-organisationen genom att göra en GET-begäran till `/segment/definitions`-slutpunkten.

**API-format**

Om du vill hämta segment som är aktiverade för kantsegmentering måste du ta med frågeparametern `evaluationInfo.synchronous.enabled=true` i sökvägen för begäran.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med segment i IMS-organisationen som är aktiverade för kantsegmentering. Mer detaljerad information om den returnerade segmentdefinitionen finns i [slutpunktshandboken för segmentdefinitioner](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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
            "imsOrgId": "{IMS_ORG_ID}",
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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

## Skapa ett segment som är aktiverat för kantsegmentering

Du kan skapa ett segment som är aktiverat för kantsegmentering genom att göra en POST-förfrågan till `/segment/definitions`-slutpunkten. Förutom att matcha en av [frågetyperna för kantsegmentering som listas ovan](#query-types), måste du ange flaggan `evaluationInfo.synchronous.enabled` i nyttolasten till true.

**API-format**

```http
POST /segment/definitions
```

**Begäran**

>[!NOTE]
>
>Exemplet nedan är en standardbegäran om att skapa ett segment. Mer information om hur du skapar en segmentdefinition finns i självstudiekursen om att [skapa ett segment](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | Objektet `evaluationInfo` avgör vilken typ av utvärdering som segmentdefinitionen ska genomgå. Om du vill använda kantsegmentering anger du `evaluationInfo.synchronous.enabled` med värdet `true`. |

**Svar**

Ett lyckat svar returnerar detaljerna om den nyligen skapade segmentdefinitionen som är aktiverad för kantsegmentering.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
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
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Nästa steg

Nu när ni vet hur ni skapar segment med stöd för kantsegmentering kan ni använda dem för att skapa personalisering på samma sida och nästa sida.

Om du vill veta hur du utför liknande åtgärder och arbetar med segment med Adobe Experience Platform användargränssnitt kan du läsa [användarhandboken för Segment Builder](../ui/segment-builder.md).
