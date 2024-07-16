---
solution: Experience Platform
title: Utvärdera händelser i nära realtid med strömmande segmentering
description: Det här dokumentet innehåller exempel på hur du använder direktuppspelningssegmentering med Adobe Experience Platform Segmentation Service API.
role: Developer
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 0%

---

# Utvärdera händelser i nära realtid med strömmande segmentering

>[!NOTE]
>
>I följande dokument beskrivs hur du använder direktuppspelningssegmentering med API:t. Mer information om hur du använder direktuppspelningssegmentering med användargränssnittet finns i [gränssnittsguiden för direktuppspelning](../ui/streaming-segmentation.md).

Med direktuppspelningssegmentering på [!DNL Adobe Experience Platform] kan kunderna segmentera i nära realtid samtidigt som de fokuserar på datarikedom. Med direktuppspelningssegmentering sker nu segmentkvalificeringen när direktuppspelningsdata når [!DNL Platform], vilket minskar behovet av att schemalägga och köra segmenteringsjobb. Med den här funktionen kan de flesta segmentregler utvärderas när data skickas till [!DNL Platform], vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Direktuppspelningssegmentering fungerar på alla data som har importerats från en direktuppspelningskälla. Segment som importerats med hjälp av en batchbaserad källa utvärderas nightly, även om det kvalificerar för direktuppspelningssegmentering.
>
>Dessutom kan segmentdefinitioner som utvärderas med direktuppspelningssegmentering avvika mellan det ideala och det faktiska medlemskapet om segmentdefinitionen baseras på en annan segmentdefinition som utvärderas med gruppsegmentering. Om till exempel segment A är baserat på segment B och segment B utvärderas med gruppsegmentering, eftersom segment B bara uppdateras var 24:e timme, kommer segment A att flyttas längre bort från de faktiska data tills det synkroniseras om med segmentet B.

## Komma igång

Den här utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform]-tjänsterna som är involverade i direktuppspelningssegmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserat på aggregerade data från flera källor.
- [[!DNL Segmentation]](../home.md): Ger möjlighet att skapa målgrupper med hjälp av segmentdefinitioner och andra externa källor från dina [!DNL Real-Time Customer Profile]-data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata med.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa [!DNL Platform] API:er.

### Läser exempel-API-anrop

Utvecklarhandboken innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Content-Type: application/json

Ytterligare rubriker kan behövas för att slutföra specifika begäranden. De rätta rubrikerna visas i vart och ett av exemplen i det här dokumentet. Var särskilt uppmärksam på exempelbegäranden för att se till att alla obligatoriska rubriker inkluderas.

### Strömmande segmenteringsaktiverade frågetyper {#query-types}

>[!NOTE]
>
>Du måste aktivera schemalagd segmentering för organisationen för att direktuppspelningssegmenteringen ska fungera. Information om att aktivera schemalagd segmentering finns i avsnittet [aktivera schemalagd segmentering](#enable-scheduled-segmentation)

För att en segmentdefinition ska kunna utvärderas med hjälp av direktuppspelningssegmentering måste frågan följa följande riktlinjer.

| Frågetyp | Information |
| ---------- | ------- |
| En händelse | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. |
| En händelse i ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse. |
| En händelse med ett tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse med ett tidsfönster. |
| Endast profil | En segmentdefinition som bara refererar till ett profilattribut. |
| En händelse med ett profilattribut inom ett relativt tidsfönster på mindre än 24 timmar | En segmentdefinition som refererar till en enda inkommande händelse, med ett eller flera profilattribut, och som inträffar inom ett relativt tidsfönster på mindre än 24 timmar. |
| Segmentering | En segmentdefinition som innehåller en eller flera grupper eller direktuppspelningssegment. **Obs!** Om ett segment används, inaktiveras profiler **var 24:e timme**. |
| Flera händelser med ett profilattribut | Alla segmentdefinitioner som refererar till flera händelser **under de senaste 24 timmarna** och (valfritt) har ett eller flera profilattribut. |

En segmentdefinition kommer **inte** att aktiveras för direktuppspelningssegmentering i följande scenarier:

- Segmentdefinitionen innehåller Adobe Audience Manager (AAM) segment eller egenskaper.
- Segmentdefinitionen innehåller flera enheter (frågor om flera enheter).
- Segmentdefinitionen innehåller en kombination av en enda händelse och en `inSegment`-händelse.
   - Om segmentet i `inSegment`-händelsen bara är en profil aktiveras segmentdefinitionen **** för direktuppspelningssegmentering.
- I segmentdefinitionen används&quot;Ignorera år&quot; som en del av tidsbegränsningarna.

Observera att följande riktlinjer gäller vid direktuppspelningssegmentering:

| Frågetyp | Riktlinje |
| ---------- | -------- |
| Enkel händelsefråga | Det finns inga begränsningar för uppslagsfönstret. |
| Fråga med händelsehistorik | <ul><li>Uppslagsfönstret är begränsat till **en dag**.</li><li>Det finns ett strikt tidsordningsvillkor **måste** mellan händelserna.</li><li>Frågor med minst en negerad händelse stöds. Hela händelsen **kan dock inte** vara en negation.</li></ul> |

Om en segmentdefinition ändras så att den inte längre uppfyller villkoren för direktuppspelningssegmentering, kommer segmentdefinitionen automatiskt att växla från&quot;direktuppspelning&quot; till&quot;Gruppering&quot;.

Dessutom sker okvalificerat segment, på samma sätt som segmentkvalificering, i realtid. Om en profil inte längre kvalificerar sig för en segmentdefinition blir den därför omedelbart okvalificerad. Om segmentdefinitionen till exempel frågar efter&quot;Alla användare som har köpt röda skor de senaste tre timmarna&quot;, efter tre timmar, kommer alla profiler som ursprungligen kvalificerades för segmentdefinitionen att vara okvalificerade.

## Hämta alla segmentdefinitioner aktiverade för direktuppspelningssegmentering

Du kan hämta en lista över alla segmentdefinitioner som har aktiverats för direktuppspelningssegmentering inom organisationen genom att göra en GET-förfrågan till slutpunkten `/segment/definitions`.

**API-format**

Om du vill hämta definitioner för direktuppspelningsaktiverade segment måste du ta med frågeparametern `evaluationInfo.continuous.enabled=true` i sökvägen för begäran.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en array med segmentdefinitioner i organisationen som är aktiverade för direktuppspelningssegmentering.

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

## Skapa en segmentdefinition som kan direktuppspelas

En segmentdefinition aktiveras automatiskt för direktuppspelning om den matchar någon av de [typer av direktuppspelningssegmentering som listas ovan](#query-types).

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

>[!NOTE]
>
>Detta är en standardbegäran om att skapa en segmentdefinition. Mer information om hur du skapar en segmentdefinition finns i självstudiekursen [om hur du skapar en segmentdefinition](../tutorials/create-a-segment.md).

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade segmentdefinitionen som är aktiverad för direktuppspelning.

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

När utvärderingen av direktuppspelning har aktiverats måste en baslinje skapas (efter vilken segmentdefinitionen alltid är aktuell). Schemalagd utvärdering (även kallad schemalagd segmentering) måste först aktiveras för att systemet automatiskt ska kunna utföra baselering. Med schemalagd segmentering kan organisationen följa ett återkommande schema för att automatiskt köra exportjobb för att utvärdera segmentdefinitioner.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanslagningsprinciper för [!DNL XDM Individual Profile]. Om din organisation har fler än fem sammanfogningsprinciper för [!DNL XDM Individual Profile] i en enda sandlådemiljö kommer du inte att kunna använda schemalagd utvärdering.

### Skapa ett schema

Genom att göra en schemaförfrågan till slutpunkten `/config/schedules` kan du skapa ett schema och inkludera den POST då schemat ska utlösas.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `properties.segments` | **(Krävs när `type` är lika med `batch_segmentation`)** Med `["*"]` säkerställs att alla segmentdefinitioner ingår. |
| `schedule` | **(Obligatoriskt)** En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Det exempel som visas (`0 0 1 * * ?`) betyder att jobbet utlöses varje dag vid 1:00:00 UTC. Mer information finns i bilagan för formatet [cron expression](./schedules.md#appendix) i dokumentationen om scheman inom segmentering. |
| `state` | *(Valfritt)* Sträng som innehåller schemats tillstånd. Tillgängliga värden: `active` och `inactive`. Standardvärdet är `inactive`. En organisation kan bara skapa ett schema. Steg för att uppdatera schemat är tillgängliga senare i den här självstudiekursen. |

**Svar**

Ett lyckat svar returnerar information om det nya schemat.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{ORG_ID}",
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

Som standard är ett schema inaktivt när det skapas, såvida inte egenskapen `state` är inställd på `active` i texten för skapandebegäran (POST). Du kan aktivera ett schema (ange `state` till `active`) genom att göra en PATCH-begäran till `/config/schedules`-slutpunkten och inkludera ID:t för schemat i sökvägen.

**API-format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Begäran**

Följande begäran använder [JSON Patch-formatering](https://datatracker.ietf.org/doc/html/rfc6902) för att uppdatera `state` för schemat till `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Nu när du har aktiverat både nya och befintliga segmentdefinitioner för direktuppspelningssegmentering och aktiverat schemalagd segmentering för att utveckla en baslinje och utföra återkommande utvärderingar, kan du börja skapa segmentdefinitioner som är aktiverade för din organisation.

Om du vill lära dig hur du utför liknande åtgärder och arbetar med segmentdefinitioner med Adobe Experience Platform användargränssnitt kan du gå till användarhandboken för [Segment Builder](../ui/segment-builder.md).

## Bilaga

I följande avsnitt visas vanliga frågor om direktuppspelningssegmentering:

### Händer direktuppspelad segmentering&quot;utan kvalificering&quot; också i realtid?

I de flesta fall sker icke-kvalificering av direktuppspelad segmentering i realtid. Däremot är definitioner för direktuppspelningssegment som använder segment av segment **inte** okvalificerade i realtid, utan efter 24 timmar.

### Vilka data fungerar direktuppspelningssegmentering på?

Direktuppspelningssegmentering fungerar på alla data som har importerats från en direktuppspelningskälla. Segment som importerats med hjälp av en batchbaserad källa utvärderas nightly, även om det kvalificerar för direktuppspelningssegmentering. Händelser som direktuppspelas i systemet med en tidsstämpel som är äldre än 24 timmar kommer att bearbetas i det efterföljande batchjobbet.

### Hur definieras segmentdefinitioner som grupp- eller direktuppspelningssegmentering?

En segmentdefinition definieras som antingen batch- eller direktuppspelningssegmentering baserat på en kombination av frågetyp och händelsehistorikens varaktighet. En lista över vilka segmentdefinitioner som ska utvärderas som ett direktuppspelningssegment finns i avsnittet [frågetyper för direktuppspelningssegmentering](#query-types).

Observera att om ett segment innehåller **både** och `inSegment` uttryck och en direkt enkel händelsekedja, kan det inte kvalificera sig för direktuppspelningssegmentering. Om du vill att den här segmentdefinitionen ska vara giltig för direktuppspelningssegmentering, bör du göra den direkta single-event-kedjan till en egen segmentdefinition.

### Varför fortsätter antalet&quot;totala kvalificerade&quot; segmentdefinitioner att öka medan antalet under&quot;De senaste X dagarna&quot; är noll i avsnittet med segmentdefinitionsdetaljer?

Antalet totala kvalificerade segmentdefinitioner hämtas från det dagliga segmenteringsjobbet, som omfattar målgrupper som är kvalificerade för både batch- och direktuppspelningssegmentdefinitioner. Det här värdet visas för både gruppsegmentsdefinitioner och segmentdefinitioner för direktuppspelning.

Talet under de senaste X dagarna **endast** innehåller målgrupper som är kvalificerade för direktuppspelningssegmentering, och **endast** ökar om du har direktuppspelade data i systemet och det räknas mot den direktuppspelningsdefinitionen. Det här värdet visas **endast** för definitioner av direktuppspelade segment. Därför kan det här värdet **** visas som 0 för gruppsegmentsdefinitioner.

Om du ser att talet under&quot;De senaste X dagarna&quot; är noll och linjediagrammet också visar noll, har du **inte** direktuppspelat några profiler i systemet som skulle vara kvalificerade för den segmentdefinitionen.

### Hur lång tid tar det innan en segmentdefinition är tillgänglig?

Det tar upp till en timme innan en segmentdefinition är tillgänglig.

### Finns det några begränsningar för de data som strömmas in?

För att direktuppspelade data ska kunna användas vid direktuppspelningssegmentering måste det finnas **ett** mellanrum mellan de direktuppspelade händelserna. Om för många händelser direktuppspelas inom samma sekund kommer Platform att behandla dessa händelser som robotgenererade data och de kommer att ignoreras. Som bästa praxis bör du ha **minst** fem sekunder mellan händelsedata för att säkerställa att data används på rätt sätt.
