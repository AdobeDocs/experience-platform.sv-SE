---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Direktuppspelningssegmentering
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Utvärdera händelser i realtid med strömmande segmentering (beta)

>[!NOTE] Direktuppspelningssegmentering är en betafunktion som kommer att vara tillgänglig på begäran.

Direktuppspelningssegmentering (kallas även kontinuerlig frågeutvärdering) är möjligheten att omedelbart utvärdera en kund så snart en händelse kommer in i en viss segmentgrupp. Med den här funktionen kan de flesta segmentregler utvärderas när data överförs till Adobe Experience Platform, vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.

![](../images/api/streaming-segment-evaluation.png)

## Komma igång

Utvecklarhandboken kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänsterna som är involverade i direktuppspelningssegmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid, baserad på aggregerade data från flera källor.
- [Segmentering](../home.md): Ger möjlighet att skapa segment och målgrupper utifrån kundprofildata i realtid.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa plattforms-API:er.

### Läser exempel-API-anrop

Utvecklarhandboken innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Mer information om sandlådor i plattformen finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

Ytterligare rubriker kan behövas för att slutföra specifika begäranden. De rätta rubrikerna visas i vart och ett av exemplen i det här dokumentet. Var särskilt uppmärksam på exempelbegäranden för att se till att alla obligatoriska rubriker inkluderas.

### Strömmande segmenteringsaktiverade frågetyper

I följande tabell visas olika typer av segmenteringsfrågor och om de har stöd för direktuppspelningssegmentering eller inte.

| Frågetyp | Exempelfråga | Stöd för strömningssegmentering |
| ---------- | ------------ | --------------------------------- |
| Enkel demografisk | &quot;Ge mig alla vars hemadress är i Kanada.&quot; | Stöds |
| Tidsseriehändelser | &quot;Ge mig alla som laddade ned Lightroom.&quot; | Stöds |
| Demografi och tidsserie | &quot;Ge mig alla som bor i Kanada och har lagt en order de senaste 30 dagarna.&quot; | Stöds |
| Frånvaro av händelser | &quot;Ge mig alla som har övergett två separata varukorgar inom två dagar från varandra.&quot; | Stöds |
| Flera enheter | &quot;Ge mig alla vars berättigandetyp är &quot;Erfaren&quot;.&quot; | Stöds inte |
| Avancerade PQL-funktioner | &quot;Ge mig alla profiler som beställde under den senaste veckan och inkludera SKU och namn för alla köpta produkter.&quot; | Stöds inte |

## Hämta alla segment som är aktiverade för direktuppspelningssegmentering

Innan du skapar ett nytt direktuppspelningsaktiverat segment eller uppdaterar ett befintligt segment som ska vara direktuppspelningsaktiverat, bör du se till att du inte duplicerar information genom att hämta en lista över alla direktuppspelningsaktiverade segment.

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
  -H 'x-sandbox-name: {SANDBOX_NAME'
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

När du har bekräftat att det segment du vill skapa inte redan finns kan du skapa ett nytt segment som är aktiverat för direktuppspelningssegmentering.

**API-format**

```http
POST /segment/definitions
```

**Begäran**

Följande begäran skapar ett nytt segment som är aktiverat för direktuppspelningssegmentering. Observera att `continuous` avsnittet är inställt på `enabled: true`.

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
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    }
}'
```

>[!NOTE] Det här är en standardbegäran om att skapa ett segment med den extra parametern för `continuous` avsnittet inställd på `enabled: true`. Mer information om hur du skapar en segmentdefinition finns i dokumentationen om hur du skapar [segment](../tutorials/create-a-segment.md).

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

## Aktivera ett befintligt segment för direktuppspelningssegmentering

Du kan aktivera ett befintligt segment för direktuppspelningssegmentering genom att ange segmentdefinitionens ID i sökvägen till en PATCH-begäran. Dessutom måste nyttolasten för denna PATCH-begäran innehålla alla detaljer för den befintliga segmentdefinitionen, som du kan komma åt genom att göra en GET-begäran till segmentdefinitionen i fråga.

### Söka efter en befintlig segmentdefinition

Om du vill söka efter en befintlig segmentdefinition måste du ange dess ID i sökvägen till en GET-begäran.

**API-format**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID:t för segmentdefinitionen som du vill söka efter. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om den segmentdefinition du begärde.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] För nästa begäran behöver du den fullständiga informationen om segmentdefinitionen som returnerades i det här svaret. Please copy the details of this response to be used in the body of the next request.

### Aktivera det befintliga segmentet för direktuppspelningssegmentering

Nu när du känner till detaljerna för det segment som du vill uppdatera kan du utföra en PATCH-begäran om att uppdatera segmentet för att aktivera direktuppspelningssegmentering.

**API-format**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**Begäran**

Nyttolasten för följande begäran tillhandahåller information om segmentdefinitionen (som hämtades i [föregående steg](#look-up-an-existing-segment-definition)) och uppdaterar den genom att ändra dess `continuous.enabled` egenskap till `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
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
    }
}'
```

**Svar**

Ett godkänt svar returnerar information om den nyligen uppdaterade segmentdefinitionen.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
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
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## Aktivera schemalagd utvärdering

När utvärdering av direktuppspelning har aktiverats måste en baslinje skapas (efter vilken segmentet alltid är uppdaterat). Detta görs automatiskt av systemet, men schemalagd utvärdering (även kallad schemalagd segmentering) måste först aktiveras för att baseleringen ska kunna utföras.

Med schemalagd segmentering kan IMS-organisationen skapa ett återkommande schema som automatiskt kör exportjobb för att utvärdera segment.

>[!NOTE] Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanslagningsprinciper för den enskilda XDM-profilen. Om din organisation har fler än fem sammanfogningsprinciper för den enskilda XDM-profilen i en enda sandlådemiljö, kommer du inte att kunna använda schemalagd utvärdering.

### Skapa ett schema

Genom att göra en POST-begäran till `/config/schedules` slutpunkten kan du skapa ett schema och inkludera den specifika tid då schemat ska utlösas.

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
| `type` | **(Obligatoriskt)** Jobbtypen i strängformat. De typer som stöds är `batch_segmentation` och `export`. |
| `properties` | **(Obligatoriskt)** Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `properties.segments` | **(Krävs när`type`är lika med`batch_segmentation`)** Om du använder `["*"]` inkluderas alla segment. |
| `schedule` | **(Obligatoriskt)** En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Det exempel som visas (`0 0 1 * * ?`) innebär att jobbet utlöses varje dag kl. 1:00:00 UTC. Mer information finns i dokumentationen för [cron expression](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . |
| `state` | *(Valfritt)* Sträng som innehåller schemat. Tillgängliga värden: `active` och `inactive`. Standardvärdet är `inactive`. En IMS-organisation kan bara skapa ett schema. Steg för att uppdatera schemat är tillgängliga senare i den här självstudiekursen. |

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

Som standard är ett schema inaktivt när det skapas, såvida inte `state` egenskapen är inställd på `active` i texten för skapandebegäran (POST). Du kan aktivera ett schema (ange `state` till `active`) genom att göra en PATCH-begäran till `/config/schedules` slutpunkten och inkludera ID:t för schemat i sökvägen.

**API-format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Begäran**

Följande begäran använder [JSON Patch-formatering](http://jsonpatch.com/) för att uppdatera `state` schemat till `active`.

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

Om du vill veta hur du utför liknande åtgärder och arbetar med segment med användargränssnittet i Adobe Experience Platform kan du läsa användarhandboken för [Segment Builder](../ui/overview.md).