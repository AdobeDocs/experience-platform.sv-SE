---
keywords: Experience Platform;hemindelning;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;kantsegmentering;Kantsegmentering;Strömningskant;
solution: Experience Platform
title: Kantsegmentering med API
topic-legacy: developer guide
description: Det här dokumentet innehåller exempel på hur du använder kantsegmentering med Adobe Experience Platform Segmentation Service API.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 8c7c1273feb2033bf338f7669a9b30d9459509f7
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Kantsegmentering

>[!NOTE]
>
>I följande dokument beskrivs hur du utför kantsegmentering med API:t. Mer information om kantsegmentering med användargränssnittet finns i [gränssnittsguide för kantsegmentering](../ui/edge-segmentation.md).
>
>Kantsegmentering är nu allmänt tillgängligt för alla plattformsanvändare. Om du skapade kantsegment under betaversionen kommer dessa segment att fortsätta fungera.

Kantsegmentering är möjligheten att utvärdera segment i Adobe Experience Platform direkt, vilket möjliggör användning av samma sida och nästa sida vid personalisering.

>[!IMPORTANT]
>
> Kantdata lagras på en edge-serverplats som ligger närmast den plats där de samlades in och kan lagras på en annan plats än den som anges som Adobe Experience Platform datacenter (eller huvudserver).
>
> Dessutom kommer kantsegmenteringsmotorn endast att efterleva begäranden på kanten där det finns **en** primär markerad identitet, vilket är förenligt med icke-kantbaserade primära identiteter.

## Komma igång

Den här utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform] tjänster som rör kantsegmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid, baserad på aggregerade data från flera källor.
- [[!DNL Segmentation]](../home.md): Ger möjlighet att skapa segment och målgrupper utifrån [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.

Om du vill kunna anropa någon Experience Platform API-slutpunkt läser du i guiden [komma igång med plattforms-API:er](../../landing/api-guide.md) om du vill veta mer om obligatoriska rubriker och hur du läser exempel-API-anrop.

## Frågetyper för kantsegmentering {#query-types}

För att ett segment ska kunna utvärderas med hjälp av kantsegmentering måste frågan följa följande riktlinjer:

| Frågetyp | Information | Exempel | PQL-exempel |
| ---------- | ------- | ------- | ----------- |
| En händelse | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. | Personer som har lagt till ett objekt i kundvagnen. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| En profil | Alla segmentdefinitioner som refererar till ett enskilt profilattribut | Folk som bor i USA. | `homeAddress.countryCode = "US"` |
| En händelse som refererar till en profil | En segmentdefinition som refererar till ett eller flera profilattribut och en enda inkommande händelse utan tidsbegränsning. | Folk som bor i USA som besökte hemsidan. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Negerad enkel händelse med ett profilattribut | En segmentdefinition som refererar till en negerad enkel inkommande händelse och ett eller flera profilattribut | Personer som bor i USA och har **not** besökte hemsidan. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| En händelse i ett tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse inom en angiven tidsperiod. | Personer som besökt hemsidan de senaste 24 timmarna. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| En händelse med ett profilattribut i ett tidsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en enda inkommande händelse inom en angiven tidsperiod. | Personer som bor i USA och som har besökt hemsidan de senaste 24 timmarna. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| Negerad enkel händelse med ett profilattribut i ett tidsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en negerad enkel inkommande händelse inom en tidsperiod. | Personer som bor i USA och har **not** besökte hemsidan de senaste 24 timmarna. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)]))` |
| Frekvenshändelse inom ett 24-timmarsfönster | En segmentdefinition som refererar till en händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer som besökte hemsidan **minst** fem gånger de senaste 24 timmarna. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Frekvenshändelse med ett profilattribut inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer från USA som besökte hemsidan **minst** fem gånger de senaste 24 timmarna. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Negerad frekvenshändelse med en profil inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och en negerad händelse som inträffar ett visst antal gånger inom ett tidsfönster på 24 timmar. | Personer som inte har besökt hemsidan **mer** än fem gånger de senaste 24 timmarna. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Flera inkommande träffar inom en tidsprofil på 24 timmar | En segmentdefinition som refererar till flera händelser som inträffar inom ett tidsfönster på 24 timmar. | Personer som besökte hemsidan **eller** har besökt utcheckningssidan inom de senaste 24 timmarna. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Flera händelser med en profil inom ett 24-timmarsfönster | En segmentdefinition som refererar till ett eller flera profilattribut och flera händelser som inträffar inom ett tidsfönster på 24 timmar. | Personer från USA som besökte hemsidan **och** har besökt utcheckningssidan inom de senaste 24 timmarna. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmentering | En segmentdefinition som innehåller en eller flera grupper eller direktuppspelningssegment. | Personer som bor i USA och som är i segmentet &quot;befintligt&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Fråga som refererar till en karta | En segmentdefinition som refererar till en egenskapskarta. | Personer som har lagt till i kundvagnen baserat på externa segmentdata. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Dessutom kan segmentet **måste** vara knuten till en kopplingsregel som är aktiv vid sidan. Mer information om kopplingsprofiler finns i [guide för sammanslagningsprinciper](../../profile/api/merge-policies.md).

En segmentdefinition **not** aktiveras för kantsegmentering i följande scenarier:

- Segmentdefinitionen innehåller en kombination av en enda händelse och en `inSegment` -händelse.
   - Om segmentet i `inSegment` -händelsen är bara profil, segmentdefinitionen **kommer** aktiveras för kantsegmentering.

## Hämta alla segment som är aktiverade för kantsegmentering

Du kan hämta en lista över alla segment som är aktiverade för kantsegmentering inom IMS-organisationen genom att göra en GET-förfrågan till `/segment/definitions` slutpunkt.

**API-format**

Om du vill hämta segment som är aktiverade för kantsegmentering måste du ta med frågeparametern `evaluationInfo.synchronous.enabled=true` i sökvägen till begäran.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med segment i IMS-organisationen som är aktiverade för kantsegmentering. Mer detaljerad information om den returnerade segmentdefinitionen finns i [slutpunktsguide för segmentdefinitioner](./segment-definitions.md).

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

Du kan skapa ett segment som är aktiverat för kantsegmentering genom att göra en begäran om POST till `/segment/definitions` slutpunkt som matchar en av [frågetyper för kantsegmentering som listas ovan](#query-types).

**API-format**

```http
POST /segment/definitions
```

**Begäran**

>[!NOTE]
>
>Exemplet nedan är en standardbegäran om att skapa ett segment. Mer information om hur du skapar en segmentdefinition finns i självstudiekursen om [skapa ett segment](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    }
}'
```

**Svar**

Ett lyckat svar returnerar detaljerna om den nyligen skapade segmentdefinitionen som är aktiverad för kantsegmentering.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
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
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
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

Om du vill veta hur du utför liknande åtgärder och arbetar med segment med Adobe Experience Platform användargränssnitt kan du gå till [Användarhandbok för Segment Builder](../ui/segment-builder.md).

## Bilaga

I följande avsnitt visas vanliga frågor om kantsegmentering:

### Hur lång tid tar det innan ett segment blir tillgängligt i Edge Network?

Det tar upp till en timme för ett segment att vara tillgängligt på Edge Network.