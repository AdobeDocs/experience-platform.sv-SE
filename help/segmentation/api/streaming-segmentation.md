---
keywords: Experience Platform;hemmabruk;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;direktuppspelningssegmentering;Kontinuerlig utvärdering;
solution: Experience Platform
title: Direktuppspelningssegmentering
topic: developer guide
description: Det här dokumentet innehåller exempel på hur du använder direktuppspelningssegmentering med API:t för direktuppspelningssegmentering.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---


# Utvärdera händelser i nära realtid med strömmande segmentering

>[!NOTE]
>
>I följande dokument beskrivs hur du använder direktuppspelningssegmentering med API:t. Mer information om hur du använder direktuppspelningssegmentering med användargränssnittet finns i [gränssnittsguiden för direktuppspelningssegmentering](../ui/streaming-segmentation.md).

Med direktuppspelningssegmentering på [!DNL Adobe Experience Platform] kan kunderna segmentera i nära realtid samtidigt som de fokuserar på datamöjligheter. Med direktuppspelningssegmentering sker nu segmentkvalificering när strömmande data når [!DNL Platform], vilket minskar behovet av att schemalägga och köra segmenteringsjobb. Med den här funktionen kan de flesta segmentregler utvärderas när data skickas till [!DNL Platform], vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Direktuppspelningssegmentering kan bara användas för att utvärdera data som direktuppspelas på plattformen. Med andra ord kommer data som hämtas via batchinmatning inte att utvärderas genom direktuppspelningssegmentering, utan kommer att utvärderas tillsammans med det nightly schemalagda segmenterade jobbet.

## Komma igång

Den här utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform]-tjänster som är involverade i direktuppspelningssegmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid, baserad på aggregerade data från flera källor.
- [[!DNL Segmentation]](../home.md): Ger möjlighet att skapa segment och målgrupper utifrån era  [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Platform] organiserar kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:er för [!DNL Platform].

### Läser exempel-API-anrop

Utvecklarhandboken innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

Ytterligare rubriker kan behövas för att slutföra specifika begäranden. De rätta rubrikerna visas i vart och ett av exemplen i det här dokumentet. Var särskilt uppmärksam på exempelbegäranden för att se till att alla obligatoriska rubriker inkluderas.

### Strömmande segmentering aktiverade frågetyper {#streaming-segmentation-query-types}

>[!NOTE]
>
>Du måste aktivera schemalagd segmentering för organisationen för att direktuppspelningssegmenteringen ska fungera. Information om att aktivera schemalagd segmentering finns i [Aktivera schemalagd segmentering](#enable-scheduled-segmentation)

För att ett segment ska kunna utvärderas med hjälp av direktuppspelningssegmentering måste frågan följa följande riktlinjer.

| Frågetyp | Detaljer |
| ---------- | ------- |
| Inkommande träff | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. |
| Inkommande träff inom ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse. |
| Endast profil | En segmentdefinition som bara refererar till ett profilattribut. |
| Inkommande träde som refererar till en profil | En segmentdefinition som refererar till en enda inkommande händelse, utan tidsbegränsning, och ett eller flera profilattribut. |
| Inkommande träde som refererar till en profil inom ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse och ett eller flera profilattribut. |
| Flera händelser som refererar till en profil | Alla segmentdefinitioner som refererar till flera händelser **under de senaste 24 timmarna** och (valfritt) har ett eller flera profilattribut. |

En segmentdefinition kommer **inte** att aktiveras för direktuppspelningssegmentering i följande scenarier:

- Segmentdefinitionen innehåller Adobe Audience Manager (AAM) segment eller egenskaper.
- Segmentdefinitionen innehåller flera enheter (frågor om flera enheter).

Dessutom gäller vissa riktlinjer för direktuppspelningssegmentering:

| Frågetyp | Riktlinje |
| ---------- | -------- |
| Enkel händelsefråga | Det finns inga begränsningar för uppslagsfönstret. |
| Fråga med händelsehistorik | <ul><li>Uppslagsfönstret är begränsat till **en dag**.</li><li>Det finns ett strikt tidsordningsvillkor **måste** mellan händelserna.</li><li>Frågor med minst en negerad händelse stöds. Hela händelsen **kan inte** vara en negation.</li></ul> |

## Hämta alla segment som är aktiverade för direktuppspelningssegmentering

Du kan hämta en lista över alla segment som är aktiverade för direktuppspelningssegmentering inom IMS-organisationen genom att göra en GET-begäran till `/segment/definitions`-slutpunkten.

**API-format**

Om du vill hämta direktuppspelningsaktiverade segment måste du ta med frågeparametern `evaluationInfo.continuous.enabled=true` i sökvägen för begäran.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med segment i IMS-organisationen som är aktiverade för direktuppspelningssegmentering.

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
                    "enabled": true
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

## Skapa ett direktuppspelningsaktiverat segment

Ett segment aktiveras automatiskt för direktuppspelning om det matchar någon av de [typer av direktuppspelningssegmentering som listas ovan](#streaming-segmentation-query-types).

**API-format**

```http
POST /segment/definitions
```

**Begäran**

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
    }
}'
```

>[!NOTE]
>
>Det här är en standardbegäran om att skapa ett segment. Mer information om hur du skapar en segmentdefinition finns i självstudiekursen om att [skapa ett segment](../tutorials/create-a-segment.md).

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade segmentdefinitionen som är aktiverad för direktuppspelning.

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
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Aktivera schemalagd utvärdering {#enable-scheduled-segmentation}

När utvärdering av direktuppspelning har aktiverats måste en baslinje skapas (efter vilken segmentet alltid är uppdaterat). Schemalagd utvärdering (även kallad schemalagd segmentering) måste först aktiveras för att systemet automatiskt ska kunna utföra baselering. Med schemalagd segmentering kan IMS-organisationen följa ett återkommande schema för att automatiskt köra exportjobb för att utvärdera segment.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanslagningsprinciper för [!DNL XDM Individual Profile]. Om din organisation har fler än fem sammanfogningsprinciper för [!DNL XDM Individual Profile] i en enda sandlådemiljö kan du inte använda schemalagd utvärdering.

### Skapa ett schema

Genom att göra en begäran om POST till `/config/schedules`-slutpunkten kan du skapa ett schema och inkludera den tidpunkt då schemat ska utlösas.

**API-format**

```http
POST /config/schedules
```

**Begäran**

Följande begäran skapar ett nytt schema baserat på specifikationerna i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | **(Obligatoriskt)** Schemats namn. Måste vara en sträng. |
| `type` | **(Obligatoriskt)** Jobbtypen i strängformat. Typerna som stöds är `batch_segmentation` och `export`. |
| `properties` | **(Obligatoriskt)** Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `properties.segments` | **(Krävs när  `type` lika med  `batch_segmentation`används)** Alla segment  `["*"]` ingår. |
| `schedule` | **(Obligatoriskt)** En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Det exempel som visas (`0 0 1 * * ?`) betyder att jobbet utlöses varje dag kl. 1:00:00 UTC. Mer information finns i [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)-dokumentationen. |
| `state` | *(Valfritt)* Sträng som innehåller schemaläge. Tillgängliga värden: `active` och `inactive`. Standardvärdet är `inactive`. En IMS-organisation kan bara skapa ett schema. Steg för att uppdatera schemat är tillgängliga senare i den här självstudiekursen. |

**Svar**

Ett lyckat svar returnerar information om det nya schemat.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### Aktivera ett schema

Som standard är ett schema inaktivt när det skapas såvida inte egenskapen `state` är inställd på `active` i texten för skapandebegäran (POST). Du kan aktivera ett schema (ange `state` till `active`) genom att göra en PATCH-begäran till `/config/schedules`-slutpunkten och inkludera ID:t för schemat i sökvägen.

**API-format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Begäran**

Följande begäran använder [JSON Patch-formatering](http://jsonpatch.com/) för att uppdatera `state` för schemat till `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Svar**

En lyckad uppdatering returnerar en tom svarstext och HTTP-status 2004 (inget innehåll).

Samma åtgärd kan användas för att inaktivera ett schema genom att ersätta värdet i föregående begäran med inaktivt.

## Nästa steg

Nu när du har aktiverat både nya och befintliga segment för direktuppspelningssegmentering och aktiverat schemalagd segmentering för att utveckla en baslinje och utföra återkommande utvärderingar, kan du börja skapa segment för din organisation.

Om du vill veta hur du utför liknande åtgärder och arbetar med segment med Adobe Experience Platform användargränssnitt kan du läsa [användarhandboken för Segment Builder](../ui/segment-builder.md).