---
solution: Experience Platform
title: Edge Segmentering med API
description: Det här dokumentet innehåller exempel på hur du använder kantsegmentering med Adobe Experience Platform Segmentation Service API.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: a1c9003a1b219325daf8fa38cda8bb1a019a55c6
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Edge segmentering

>[!NOTE]
>
>I följande dokument beskrivs hur du utför kantsegmentering med API:t. Mer information om kantsegmentering med hjälp av användargränssnittet finns i [gränssnittsguiden för kantsegmentering](../ui/edge-segmentation.md).
>
>Edge segmentering är nu allmänt tillgängligt för alla plattformsanvändare. Om du skapade definitioner för kantsegment under betaversionen kommer dessa segmentdefinitioner att fortsätta att fungera.

Edge segmentering är möjligheten att omedelbart utvärdera segmentdefinitioner i Adobe Experience Platform, vilket möjliggör användning av samma sida och nästa sida.

>[!IMPORTANT]
>
> Kantdata lagras på en edge-serverplats som ligger närmast den plats där de samlades in och kan lagras på en annan plats än den som anges som Adobe Experience Platform datacenter (eller huvudserver).
>
> Dessutom kommer kantsegmenteringsmotorn endast att efterleva begäranden på kanten där det finns **en** primär markerad identitet, vilket är förenligt med icke-kantbaserade primära identiteter.

## Komma igång

Den här utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform]-tjänster som är involverade i kantsegmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserat på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Gör att du kan skapa målgrupper från [!DNL Real-Time Customer Profile]-data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata med.

Om du vill kunna anropa alla Experience Platform API-slutpunkter läser du guiden [komma igång med plattforms-API:er](../../landing/api-guide.md) för att få information om vilka huvuden som krävs och hur du läser exempel-API-anrop.

## Edge segmenteringsfrågetyper {#query-types}

För att ett segment ska kunna utvärderas med hjälp av kantsegmentering måste frågan följa följande riktlinjer:

| Frågetyp | Information |
| ---------- | ------- |
| En händelse inom ett tidsfönster på mindre än 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse inom ett tidsfönster på mindre än 24 timmar. |
| Endast profil | En segmentdefinition som bara refererar till ett profilattribut. |
| En händelse med ett profilattribut inom ett relativt tidsfönster på mindre än 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse, med ett eller flera profilattribut, och som inträffar inom ett relativt tidsfönster på mindre än 24 timmar. |
| Segmentering | En segmentdefinition som innehåller en eller flera grupper eller direktuppspelningssegment. **Obs!** Om ett segment används, inaktiveras profiler **var 24:e timme**. |
| Flera händelser med ett profilattribut | Alla segmentdefinitioner som refererar till flera händelser **under de senaste 24 timmarna** och (valfritt) har ett eller flera profilattribut. |

Dessutom måste segmentet **** vara kopplat till en sammanfogningsprincip som är aktiv på kanten. Mer information om sammanfogningsprinciper finns i [policyguiden för sammanfogning](../../profile/api/merge-policies.md).

En segmentdefinition kommer **inte** att aktiveras för kantsegmentering i följande scenarier:

- Segmentdefinitionen innehåller en kombination av en enda händelse och en `inSegment`-händelse.
   - Om segmentet i `inSegment`-händelsen bara är en profil aktiveras segmentdefinitionen **** för kantsegmentering.
- I segmentdefinitionen används&quot;Ignorera år&quot; som en del av tidsbegränsningarna.

## Hämta alla segment aktiverade för kantsegmentering

Du kan hämta en lista över alla segment som har aktiverats för kantsegmentering inom din organisation genom att göra en GET-förfrågan till slutpunkten `/segment/definitions`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med segment i organisationen som är aktiverade för kantsegmentering. Mer detaljerad information om den returnerade segmentdefinitionen finns i [stödlinjen för segmentdefinitioner](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

Du kan skapa ett segment som är aktiverat för kantsegmentering genom att göra en POST-förfrågan till `/segment/definitions`-slutpunkten som matchar någon av de [kantsegmenteringsfrågor som listas ovan](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
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

Om du vill lära dig hur du utför liknande åtgärder och arbetar med segment med Adobe Experience Platform användargränssnitt kan du gå till användarhandboken för [Segment Builder](../ui/segment-builder.md).

## Bilaga

I följande avsnitt visas vanliga frågor om kantsegmentering:

### Hur lång tid tar det innan ett segment blir tillgängligt på Edge Network?

Det tar upp till en timme för ett segment att vara tillgängligt på Edge Network.
