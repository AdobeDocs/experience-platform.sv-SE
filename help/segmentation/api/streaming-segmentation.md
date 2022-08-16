---
keywords: Experience Platform;hemmabruk;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;direktuppspelningssegmentering;Kontinuerlig utvärdering;
solution: Experience Platform
title: 'Utvärdera händelser i nära realtid med strömmande segmentering '
topic-legacy: developer guide
description: Det här dokumentet innehåller exempel på hur du använder direktuppspelningssegmentering med Adobe Experience Platform Segmentation Service API.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 654e141735b6882b4c0233b8e1c73d0838c8374e
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 0%

---

# Utvärdera händelser i nära realtid med strömmande segmentering

>[!NOTE]
>
>I följande dokument beskrivs hur du använder direktuppspelningssegmentering med API:t. Mer information om hur du använder direktuppspelningssegmentering med användargränssnittet finns i [gränssnittsguide för direktuppspelningssegmentering](../ui/streaming-segmentation.md).

Direktuppspelningssegmentering på [!DNL Adobe Experience Platform] gör det möjligt för kunderna att segmentera i nära realtid samtidigt som de fokuserar på datamöjligheter. Med direktuppspelningssegmentering sker nu segmentkvalificeringen i takt med att data strömmas in i [!DNL Platform], vilket minskar behovet av att schemalägga och köra segmenteringsjobb. Med den här funktionen kan de flesta segmentregler utvärderas när data skickas till [!DNL Platform], vilket innebär att segmentmedlemskapet hålls uppdaterat utan att schemalagda segmenteringsjobb körs.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>Direktuppspelningssegmentering fungerar på alla data som har importerats från en direktuppspelningskälla. Segment som importerats med hjälp av en batchbaserad källa utvärderas nightly, även om det kvalificerar för direktuppspelningssegmentering.
>
>Dessutom kan segment som utvärderas med direktuppspelningssegmentering avvika från det idealiska och det faktiska medlemskapet om segmentet är baserat på ett annat segment som utvärderas med gruppsegmentering. Om till exempel segment A är baserat på segment B och segment B utvärderas med gruppsegmentering, eftersom segment B bara uppdateras var 24:e timme, kommer segment A att flyttas längre bort från de faktiska data tills det synkroniseras om med segmentet B.

## Komma igång

Den här utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform] tjänster som rör direktuppspelningssegmentering. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid, baserad på aggregerade data från flera källor.
- [[!DNL Segmentation]](../home.md): Ger möjlighet att skapa segment och målgrupper utifrån [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ringa [!DNL Platform] API:er.

### Läser exempel-API-anrop

Utvecklarhandboken innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

Ytterligare rubriker kan behövas för att slutföra specifika begäranden. De rätta rubrikerna visas i vart och ett av exemplen i det här dokumentet. Var särskilt uppmärksam på exempelbegäranden för att se till att alla obligatoriska rubriker inkluderas.

### Strömmande segmenteringsaktiverade frågetyper {#query-types}

>[!NOTE]
>
>Du måste aktivera schemalagd segmentering för organisationen för att direktuppspelningssegmenteringen ska fungera. Information om att aktivera schemalagd segmentering finns i [aktivera avsnitt för schemalagd segmentering](#enable-scheduled-segmentation)

För att ett segment ska kunna utvärderas med hjälp av direktuppspelningssegmentering måste frågan följa följande riktlinjer.

| Frågetyp | Detaljer |
| ---------- | ------- |
| En händelse | En segmentdefinition som refererar till en enda inkommande händelse utan tidsbegränsning. |
| En händelse i ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse. |
| En händelse med ett tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse med ett tidsfönster. |
| Endast profil | En segmentdefinition som bara refererar till ett profilattribut. |
| En händelse med ett profilattribut | En segmentdefinition som refererar till en enda inkommande händelse, utan tidsbegränsning, och ett eller flera profilattribut. **Obs!** Frågan utvärderas omedelbart när händelsen kommer. Om en profilhändelse inträffar måste den dock vänta i 24 timmar för att införlivas. |
| En händelse med ett profilattribut i ett relativt tidsfönster | En segmentdefinition som refererar till en enda inkommande händelse och ett eller flera profilattribut. |
| Segmentering | En segmentdefinition som innehåller en eller flera grupper eller direktuppspelningssegment. **Obs!** Om ett segment används, diskvalificeras profilen **var 24:e timme**. |
| Flera händelser med ett profilattribut | En segmentdefinition som refererar till flera händelser **inom de senaste 24 timmarna** och (valfritt) har ett eller flera profilattribut. |

En segmentdefinition **not** aktiveras för direktuppspelningssegmentering i följande scenarier:

- Segmentdefinitionen innehåller Adobe Audience Manager (AAM) segment eller egenskaper.
- Segmentdefinitionen innehåller flera enheter (frågor om flera enheter).

Observera att följande riktlinjer gäller vid direktuppspelningssegmentering:

| Frågetyp | Riktlinje |
| ---------- | -------- |
| Enkel händelsefråga | Det finns inga begränsningar för uppslagsfönstret. |
| Fråga med händelsehistorik | <ul><li>Uppslagsfönstret är begränsat till **en dag**.</li><li>Ett strikt tidsordningsvillkor **måste** finns mellan händelserna.</li><li>Frågor med minst en negerad händelse stöds. Hela händelsen **inte** vara en negation.</li></ul> |

Om en segmentdefinition ändras så att den inte längre uppfyller villkoren för direktuppspelningssegmentering, kommer segmentdefinitionen automatiskt att växla från&quot;direktuppspelning&quot; till&quot;Gruppering&quot;.

Dessutom sker okvalificerat segment, på samma sätt som segmentkvalificering, i realtid. Om en publik inte längre kvalificerar sig för ett segment blir det därför omedelbart okvalificerat. Om segmentdefinitionen till exempel frågar efter&quot;Alla användare som har köpt röda skor de senaste tre timmarna&quot;, efter tre timmar, kommer alla profiler som ursprungligen kvalificerades för segmentdefinitionen att vara okvalificerade.

## Hämta alla segment som är aktiverade för direktuppspelningssegmentering

Du kan hämta en lista över alla segment som är aktiverade för direktuppspelningssegmentering inom IMS-organisationen genom att göra en GET-förfrågan till `/segment/definitions` slutpunkt.

**API-format**

Om du vill hämta direktuppspelningsaktiverade segment måste du ta med frågeparametern `evaluationInfo.continuous.enabled=true` i sökvägen till begäran.

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

## Skapa ett direktuppspelningsaktiverat segment

Ett segment aktiveras automatiskt för direktuppspelning om det matchar ett av [segmenteringstyper för direktuppspelning som listas ovan](#query-types).

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
    }
}'
```

>[!NOTE]
>
>Det här är en standardbegäran om att skapa ett segment. Mer information om hur du skapar en segmentdefinition finns i självstudiekursen om [skapa ett segment](../tutorials/create-a-segment.md).

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

När utvärdering av direktuppspelning har aktiverats måste en baslinje skapas (efter vilken segmentet alltid är uppdaterat). Schemalagd utvärdering (även kallad schemalagd segmentering) måste först aktiveras för att systemet automatiskt ska kunna utföra baselering. Med schemalagd segmentering kan IMS-organisationen följa ett återkommande schema för att automatiskt köra exportjobb för att utvärdera segment.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanfogningsprinciper för [!DNL XDM Individual Profile]. Om din organisation har fler än fem samkörningspolicyer för [!DNL XDM Individual Profile] i en enda sandlådemiljö kommer du inte att kunna använda schemalagd utvärdering.

### Skapa ett schema

Genom att göra en POST-förfrågan till `/config/schedules` kan du skapa ett schema och inkludera den specifika tidpunkt då schemat ska utlösas.

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
| `properties.segments` | **(Krävs när `type` är lika med `batch_segmentation`)** Använda `["*"]` säkerställer att alla segment ingår. |
| `schedule` | **(Obligatoriskt)** En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Exemplet (`0 0 1 * * ?`) innebär att jobbet utlöses varje dag kl. 1:00:00 UTC. Mer information finns i bilagan på [cron, uttrycksformat](./schedules.md#appendix) i dokumentationen om scheman inom segmentering. |
| `state` | *(Valfritt)* Sträng som innehåller schemats tillstånd. Tillgängliga värden: `active` och `inactive`. Standardvärdet är `inactive`. En IMS-organisation kan bara skapa ett schema. Steg för att uppdatera schemat är tillgängliga senare i den här självstudiekursen. |

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

Som standard är ett schema inaktivt när det skapas såvida inte `state` egenskapen är inställd på `active` i texten för skapandebegäran (POST). Du kan aktivera ett schema (ange `state` till `active`) genom att göra en begäran från PATCH till `/config/schedules` slutpunkten och inklusive ID för schemat i sökvägen.

**API-format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Begäran**

Följande begäran använder [JSON Patch-formatering](https://datatracker.ietf.org/doc/html/rfc6902) för att uppdatera `state` av schemat till `active`.

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

Nu när du har aktiverat både nya och befintliga segment för direktuppspelningssegmentering och aktiverat schemalagd segmentering för att utveckla en baslinje och utföra återkommande utvärderingar, kan du börja skapa direktuppspelningsaktiverade segment för din organisation.

Om du vill veta hur du utför liknande åtgärder och arbetar med segment med Adobe Experience Platform användargränssnitt kan du gå till [Användarhandbok för Segment Builder](../ui/segment-builder.md).

## Bilaga

I följande avsnitt visas vanliga frågor om direktuppspelningssegmentering:

### Händer direktuppspelningssegmentering&quot;utan kvalificering&quot; också i realtid?

I de flesta fall sker icke-kvalificering av direktuppspelad segmentering i realtid. Det gör emellertid direktuppspelningssegment som använder segment av segment **not** diskvalificera i realtid, utan att kvalificera sig efter 24 timmar.

### Vilka data fungerar direktuppspelningssegmentering på?

Direktuppspelningssegmentering fungerar på alla data som har importerats från en direktuppspelningskälla. Segment som importerats med hjälp av en batchbaserad källa utvärderas nightly, även om det kvalificerar för direktuppspelningssegmentering. Händelser som direktuppspelas i systemet med en tidsstämpel som är äldre än 24 timmar kommer att bearbetas i det efterföljande batchjobbet.

### Hur definieras segment som grupp- eller direktuppspelningssegmentering?

Ett segment definieras som antingen batch- eller direktuppspelningssegmentering baserat på en kombination av frågetyp och händelsehistorikens varaktighet. En lista över vilka segment som ska utvärderas som ett direktuppspelningssegment finns i [frågetyper för direktuppspelningssegmentering](#query-types).

### Varför ökar antalet&quot;totala kvalificerade&quot; segment medan antalet under&quot;De senaste X dagarna&quot; är noll i segmentinformationsavsnittet?

Antalet kvalificerade segment baseras på det dagliga segmenteringsjobbet, som omfattar målgrupper som är kvalificerade för både batch- och direktuppspelningssegment. Detta värde visas för både grupp- och direktuppspelningssegment.

Numret under de senaste X dagarna **endast** omfattar målgrupper som är kvalificerade för direktuppspelningssegmentering, och **endast** ökar om du har direktuppspelade data i systemet och den räknas in i den direktuppspelningsdefinitionen. Detta värde är **endast** visas för direktuppspelningssegment. Detta resulterar i att detta värde **kan** visas som 0 för gruppsegment.

Om du ser att talet under&quot;De senaste X dagarna&quot; är noll och linjediagrammet också visar noll, har du **not** strömmade alla profiler till systemet som skulle vara kvalificerade för det segmentet.