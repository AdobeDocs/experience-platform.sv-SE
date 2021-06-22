---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;förhandsvisning;exempel
title: API-slutpunkt för exempelstatus för förhandsgranskning (förhandsgranskning av profil)
description: Med förhandsgranskningsexemplets statusslutpunkt, som ingår i kundprofils-API:t i realtid, kan du förhandsgranska det senaste framgångsrika exemplet av dina profildata, lista profildistribution per datauppsättning och per identitet och generera en överlappningsrapport för datauppsättningar.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 0c7dc02ed0bacf7e0405b836f566149a872fc31a
workflow-type: tm+mt
source-wordcount: '2445'
ht-degree: 0%

---

# Förhandsgranska exempelstatusslutpunkt (förhandsgranskning av profil)

Med Adobe Experience Platform kan ni importera kunddata från flera olika källor för att skapa en robust, enhetlig profil för varje enskild kund. När data hämtas till Platform körs ett exempeljobb för att uppdatera profilantalet och andra datarelaterade mått för kundprofiler i realtid.

Resultaten av det här exempeljobbet kan visas med slutpunkten `/previewsamplestatus`, som ingår i kundprofils-API:t i realtid. Den här slutpunkten kan också användas för att lista profildistributioner av både datauppsättningen och identitetsnamnutrymmet, samt för att generera en överlappande rapport för datauppsättningen och en rapport om identitetsöverlappning för att få synlighet i sammansättningen av organisationens profilarkiv. Den här guiden går igenom de steg som krävs för att visa dessa mått med API-slutpunkten `/previewsamplestatus`.

>[!NOTE]
>
>Det finns uppskattnings- och förhandsgranskningsslutpunkter som ingår i Adobe Experience Platform Segmentation Service API som gör att du kan visa information på sammanfattningsnivå om segmentdefinitioner så att du kan isolera den förväntade målgruppen. Om du vill hitta detaljerade steg för att arbeta med segmentförhandsgranskning och uppskattningar av slutpunkter kan du gå till [handboken för förhandsvisningar och uppskattningar av slutpunkter](../../segmentation/api/previews-and-estimates.md), som ingår i utvecklarhandboken för [!DNL Segmentation] API.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa valfritt [!DNL Experience Platform]-API.

## Profilfragment jämfört med sammanslagna profiler

Den här guiden refererar till både profilfragment och sammanfogade profiler. Det är viktigt att förstå skillnaden mellan dessa villkor innan du fortsätter.

Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med varumärket i flera kanaler har organisationen troligen flera profilfragment som är kopplade till den enskilda kunden i flera datauppsättningar.

När profilfragment hämtas till Platform sammanfogas de (baserat på en sammanfogningspolicy) för att skapa en enda profil för den kunden. Det totala antalet profilfragment är därför sannolikt alltid högre än det totala antalet sammanfogade profiler, eftersom varje profil består av flera fragment.

Om du vill veta mer om profiler och deras roll i Experience Platform börjar du med att läsa [Kundprofilöversikt i realtid](../home.md).

## Hur exempeljobbet utlöses

När data som har aktiverats för kundprofilen i realtid hämtas till [!DNL Platform] lagras de i profildatalagret. När inmatningen av poster i profilarkivet ökar eller minskar det totala antalet profiler med mer än 5 %, utlöses ett samplingsjobb för att uppdatera antalet. Hur provet utlöses beror på vilken typ av intag som används:

* För **arbetsflöden för strömmande data** görs en timkontroll för att avgöra om tröskelvärdet på 5 % ökning eller minskning har uppnåtts. Om den har det utlöses ett exempeljobb automatiskt för att uppdatera antalet.
* Om tröskelvärdet på 5 % ökning eller minskning uppnås körs ett jobb för att uppdatera antalet för **batchimport** inom 15 minuter efter att en batch har importerats till profilbutiken. Med hjälp av profil-API:t kan du förhandsgranska det senaste framgångsrika exempeljobbet samt lista profildistributionen per datauppsättning och per identitetsnamnområde.

Profilantalet och profilerna efter namnutrymmesmått är också tillgängliga i [!UICONTROL Profiles]-avsnittet i användargränssnittet för Experience Platform. Mer information om hur du får åtkomst till profildata via användargränssnittet finns i [[!DNL Profile] användargränssnittsguiden](../ui/user-guide.md).

## Visa senaste exempelstatus {#view-last-sample-status}

Du kan utföra en GET-förfrågan till `/previewsamplestatus`-slutpunkten för att visa information om det senaste slutförda samplingsjobbet som kördes för din IMS-organisation. Detta inkluderar det totala antalet profiler i exemplet, liksom antalet profiler eller det totala antalet profiler som din organisation har i Experience Platform.

Profilantalet genereras efter sammanfogning av profilfragment till en enda profil för varje enskild kund. När profilfragment sammanfogas returnerar de med andra ord antalet &quot;1&quot;-profiler eftersom de alla är relaterade till samma individ.

Profilantalet omfattar även både profiler med attribut (postdata) och profiler som endast innehåller tidsseriedata (händelsedata), t.ex. Adobe Analytics-profiler. Exempeljobbet uppdateras regelbundet när profildata importeras för att ge ett aktuellt totalt antal profiler inom plattformen.

**API-format**

```http
GET /previewsamplestatus
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller information om det senaste slutförda exempeljobbet som kördes för organisationen.

>[!NOTE]
>
>I det här exemplet är `numRowsToRead` och `totalRows` lika med varandra. Beroende på hur många profiler din organisation har i Experience Platform kan detta vara fallet. Vanligtvis är dessa två tal olika, där `numRowsToRead` är det mindre talet eftersom det representerar exemplet som en delmängd av det totala antalet profiler (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| Egenskap | Beskrivning |
|---|---|
| `numRowsToRead` | Det totala antalet sammanfogade profiler i exemplet. |
| `sampleJobRunning` | Ett booleskt värde som returnerar `true` när ett provjobb pågår. Ger transparens i den fördröjning som uppstår när en gruppfil överförs till när den läggs till i profilarkivet. |
| `cosmosDocCount` | Totalt antal dokument i Cosmos. |
| `totalFragmentCount` | Totalt antal profilfragment i profilarkivet. |
| `lastSuccessfulBatchTimestamp` | Senaste lyckade tidsstämpel för batchimport. |
| `streamingDriven` | *Detta fält har tagits bort och innehåller ingen betydelse för svaret.* |
| `totalRows` | Totalt antal sammanfogade profiler i Experience Platform, även kallat &#39;antal profiler&#39;. |
| `lastBatchId` | ID för senaste batchförbrukning. |
| `status` | Status för det senaste exemplet. |
| `samplingRatio` | Förhållandet mellan de sammanslagna profiler som du har tagit prov på (`numRowsToRead`) och de totala sammanslagna profilerna (`totalRows`), uttryckt i procent i decimalformat. |
| `mergeStrategy` | Sammanfogningsstrategi som används i exemplet. |
| `lastSampledTimestamp` | Senaste lyckade exempeltidsstämpel. |

## Visa profildistribution efter datauppsättning

Om du vill visa profildistributionen per datauppsättning kan du utföra en GET-begäran till `/previewsamplestatus/report/dataset`-slutpunkten.

**API-format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅÅ-MM-DD Exempel: `date=2024-12-31` |

**Begäran**

Följande begäran använder parametern `date` för att returnera den senaste rapporten för det angivna datumet.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller en `data`-array som innehåller en lista med datauppsättningsobjekt. Svaret som visas har trunkerats så att tre datauppsättningar visas.

>[!NOTE]
>
>Om det finns flera rapporter för datumet returneras bara den senaste rapporten. Om det inte finns någon datauppsättningsrapport för det angivna datumet returneras HTTP-status 404 (Hittades inte).

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Egenskap | Beskrivning |
|---|---|
| `sampleCount` | Det totala antalet sammanfogade profiler i prov med detta datauppsättnings-ID. |
| `samplePercentage` | `sampleCount` som en procentandel av det totala antalet sammanfogade profiler i prov (värdet `numRowsToRead` som returnerades i [den senaste samplingsstatusen](#view-last-sample-status)), uttryckt i decimalformat. |
| `fullIDsCount` | Det totala antalet sammanfogade profiler med det här datauppsättnings-ID:t. |
| `fullIDsPercentage` | `fullIDsCount` som en procentandel av det totala antalet sammanfogade profiler (värdet `totalRows` som returnerades i [den senaste samplingsstatusen](#view-last-sample-status)), uttryckt i decimalformat. |
| `name` | Namnet på datauppsättningen, som angavs när datauppsättningen skapades. |
| `description` | Beskrivningen av datauppsättningen, som den angavs när datauppsättningen skapades. |
| `value` | Datauppsättningens ID. |
| `streamingIngestionEnabled` | Anger om datauppsättningen är aktiverad för direktuppspelningsinmatning. |
| `createdUser` | Användar-ID för den användare som skapade datauppsättningen. |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date`-parameter angavs under begäran, returneras rapporten för det angivna datumet. Om ingen `date`-parameter anges returneras den senaste rapporten. |

## Visa profildistribution efter ID-namnområde

Du kan utföra en GET-begäran till `/previewsamplestatus/report/namespace`-slutpunkten för att visa uppdelningen efter identitetsnamnområde för alla sammanfogade profiler i profilarkivet. Detta omfattar både standardidentiteter från Adobe och anpassade identiteter som definieras av organisationen.

Identitetsnamnutrymmen är en viktig komponent i Adobe Experience Platform Identity Service som fungerar som indikatorer för det sammanhang som kunddata hör till. Börja med att läsa [översikten över identitetsnamnrymden](../../identity-service/namespaces.md) om du vill veta mer.

>[!NOTE]
>
>Det totala antalet profiler per namnutrymme (genom att lägga ihop värdena som visas för varje namnutrymme) kan vara högre än antalet profiler eftersom en profil kan kopplas till flera namnutrymmen. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

**API-format**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅÅ-MM-DD Exempel: `date=2024-12-31` |

**Begäran**

Följande begäran anger ingen `date`-parameter och returnerar därför den senaste rapporten.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller en `data`-array, med enskilda objekt som innehåller informationen för varje namnutrymme. Svaret som visas har trunkerats så att fyra namnutrymmen visas.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Egenskap | Beskrivning |
|---|---|
| `sampleCount` | Det totala antalet samkörda profiler i namnutrymmet. |
| `samplePercentage` | `sampleCount` som en procentandel av de sammanfogade profilerna (värdet `numRowsToRead` som returnerades i [den senaste samplingsstatusen](#view-last-sample-status)), uttryckt i decimalformat. |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date`-parameter angavs under begäran, returneras rapporten för det angivna datumet. Om ingen `date`-parameter anges returneras den senaste rapporten. |
| `fullIDsFragmentCount` | Det totala antalet profilfragment i namnutrymmet. |
| `fullIDsCount` | Det totala antalet sammanfogade profiler i namnutrymmet. |
| `fullIDsPercentage` | `fullIDsCount` som en procentandel av det totala sammanslagna profilerna (värdet `totalRows` som returnerades i [den senaste samplingsstatusen](#view-last-sample-status)), uttryckt i decimalformat. |
| `code` | Namnutrymmets `code`. Detta kan du hitta när du arbetar med namnutrymmen med hjälp av API:t [Adobe Experience Platform Identity Service](../../identity-service/api/list-namespaces.md) och kallas även [!UICONTROL Identity symbol] i användargränssnittet för Experience Platform. Mer information finns i [översikten över identitetsnamnet](../../identity-service/namespaces.md). |
| `value` | Värdet `id` för namnutrymmet. Detta kan du hitta när du arbetar med namnutrymmen med hjälp av [ID-tjänstens API](../../identity-service/api/list-namespaces.md). |

## Generera överlappningsrapport för datauppsättning

Rapporten om överlappning av datauppsättningar ger synlighet i sammansättningen av organisationens profilbutik genom att visa de datauppsättningar som bidrar mest till den adresserbara målgruppen (sammanslagna profiler). Förutom att ge insikter om era data kan den här rapporten hjälpa er att vidta åtgärder för att optimera licensanvändningen, till exempel att ställa in en TTL för vissa datauppsättningar.

Du kan generera överlappningsrapporten för datauppsättningen genom att utföra en GET-begäran till `/previewsamplestatus/report/dataset/overlap`-slutpunkten.

Stegvisa instruktioner om hur du genererar överlappningsrapporten för datauppsättningar med kommandoraden eller Postman-gränssnittet finns i [självstudiekursen om att generera överlappningsrapporten för datauppsättningar](../tutorials/dataset-overlap-report.md).

**API-format**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på samma datum returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅÅ-MM-DD Exempel: `date=2024-12-31` |

**Begäran**

Följande begäran använder parametern `date` för att returnera den senaste rapporten för det angivna datumet.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

En lyckad begäran returnerar HTTP-status 200 (OK) och datasetet överlappar rapporten.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| Egenskap | Beskrivning |
|---|---|
| `data` | Objektet `data` innehåller kommaavgränsade listor med datauppsättningar och deras respektive profilantal. |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date`-parameter angavs under begäran, returneras rapporten för det angivna datumet. Om ingen `date`-parameter anges returneras den senaste rapporten. |

### Tolka överlappningsrapporten för datauppsättningen

Resultatet av rapporten kan tolkas utifrån datauppsättningar och antal profiler i svaret. Titta på följande exempelrapportobjekt:`data`

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Den här rapporten innehåller följande information:
* Det finns 123 profiler med data från följande datauppsättningar: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Det finns 454 412 profiler som består av data från dessa två datauppsättningar: `5d92921872831c163452edc8` och `5eb2cdc6fa3f9a18a7592a98`.
* Det finns 107 profiler som endast består av data från datauppsättningen `5eeda0032af7bb19162172a7`.
* Det finns totalt 454 642 profiler i organisationen.

## Generera rapport över identitetsöverlappning

Rapporten om identitetsöverlappning ger synlighet i kompositionen för din organisations profilbutik genom att visa de identiteter som bidrar mest till den adresserbara målgruppen (sammanslagna profiler). Detta omfattar både standardidentiteter från Adobe och anpassade identiteter som definieras av organisationen.

Du kan generera rapporten om identitetsöverlappning genom att utföra en GET-begäran till `/previewsamplestatus/report/identity/overlap`-slutpunkten.

**API-format**

```http
GET /previewsamplestatus/report/identity/overlap
GET /previewsamplestatus/report/identity/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på samma datum returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅÅ-MM-DD Exempel: `date=2024-12-31` |

**Begäran**

Följande begäran använder parametern `date` för att returnera den senaste rapporten för det angivna datumet.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/identity/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

En lyckad begäran returnerar HTTP-status 200 (OK) och identitetsöverlappningsrapporten.

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| Egenskap | Beskrivning |
|---|---|
| `data` | Objektet `data` innehåller kommaavgränsade listor med unika kombinationer av ID-namnområdeskoder och deras respektive profilantal. |
| Namnområdeskoder | `code` är ett kort formulär för varje namn på identitetsnamn. Det går att hitta en mappning av varje `code` till `name` med hjälp av API:t [Adobe Experience Platform Identity Service](../../identity-service/api/list-namespaces.md). `code` kallas också [!UICONTROL Identity symbol] i användargränssnittet för Experience Platform. Mer information finns i [översikten över identitetsnamnet](../../identity-service/namespaces.md). |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date`-parameter angavs under begäran, returneras rapporten för det angivna datumet. Om ingen `date`-parameter anges returneras den senaste rapporten. |

### Tolka rapporten om identitetsöverlappning

Resultatet av rapporten kan tolkas utifrån identiteten och antalet profiler i svaret. Det numeriska värdet för varje rad visar hur många profiler som består av den exakta kombinationen av standard- och anpassade identitetsnamnutrymmen.

Ta följande utdrag från objektet `data`:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Den här rapporten innehåller följande information:
* Det finns 142 profiler som består av `AAID`, `ECID` och `Email` standardidentiteter samt av ett anpassat `crmid`-identitetsnamnutrymme.
* Det finns 24 profiler som består av `AAID` och `ECID` identitetsnamnutrymmen.
* Det finns 6 565 profiler som bara innehåller en `ECID`-identitet.

## Nästa steg

Nu när du vet hur du förhandsgranskar exempeldata i profilarkivet och kör flera överlappningsrapporter kan du även använda uppskattnings- och förhandsgranskningsslutpunkterna i segmenteringstjänstens API för att visa sammanfattningsnivåinformation om segmentdefinitionerna. Denna information hjälper er att isolera den förväntade målgruppen i ert segment. Om du vill veta mer om hur du arbetar med förhandsvisningar och uppskattningar av segment med hjälp av segmenterings-API:t kan du gå till guiden [för förhandsgranskning och uppskattning av slutpunkter](../../segmentation/api/previews-and-estimates.md).

