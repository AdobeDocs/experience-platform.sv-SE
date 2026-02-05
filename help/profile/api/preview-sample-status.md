---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;förhandsvisning;exempel
title: API-slutpunkt för exempelstatus för förhandsgranskning (förhandsgranskning av profil)
description: Med slutpunkten för förhandsgranskning av exempelstatus i API:t för kundprofiler i realtid kan du förhandsgranska det senaste framgångsrika exemplet av dina profildata, lista profildistribution per datauppsättning och identitet och generera rapporter som visar dataset överlappning, identitetsöverlappning och icke sammansatta profiler.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 399b76f260732015f691fd199c977d6f7e772b01
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# Förhandsgranska exempelstatusslutpunkt (förhandsgranskning av profil)

Med Adobe Experience Platform kan ni importera kunddata från flera olika källor för att skapa en robust, enhetlig profil för varje enskild kund. När data hämtas till Experience Platform körs ett exempeljobb för att uppdatera profilantalet och andra datarelaterade mått för kundprofiler i realtid.

Resultaten av det här exempeljobbet kan visas med slutpunkten `/previewsamplestatus`, som ingår i kundprofils-API:t i realtid. Den här slutpunkten kan också användas för att lista profildistributioner av både datauppsättningen och identitetsnamnutrymmet, samt för att generera flera rapporter för att få synlighet i kompositionen för organisationens profilarkiv. Den här guiden går igenom de steg som krävs för att visa dessa mått med API-slutpunkten `/previewsamplestatus`.

>[!NOTE]
>
>Det finns uppskattnings- och förhandsgranskningsslutpunkter som ingår i Adobe Experience Platform Segmentation Service API som gör att du kan visa information på sammanfattningsnivå om segmentdefinitioner så att du kan isolera den förväntade målgruppen. Detaljerade steg för hur du arbetar med förhandsgransknings- och uppskattningsslutpunkter finns i [förhandsgransknings- och uppskattningsguiden](../../segmentation/api/previews-and-estimates.md), som ingår i [!DNL Segmentation] API-utvecklarhandboken.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett [!DNL Experience Platform] -API.

## Profilfragment jämfört med sammanslagna profiler

Den här guiden refererar till både profilfragment och sammanfogade profiler. Det är viktigt att förstå skillnaden mellan dessa villkor innan du fortsätter.

Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med varumärket i flera kanaler har organisationen troligen flera profilfragment som är kopplade till den enskilda kunden i flera datauppsättningar.

När profilfragment importeras till Experience Platform sammanfogas de (baserat på en sammanfogningspolicy) för att skapa en enda profil för den kunden. Det totala antalet profilfragment är därför sannolikt alltid högre än det totala antalet sammanfogade profiler, eftersom varje profil består av flera fragment.

Om du vill veta mer om profiler och deras roll i Experience Platform börjar du med att läsa [Översikt över kundprofiler i realtid](../home.md).

## Hur exempeljobbet utlöses

När data som har aktiverats för kundprofilen i realtid hämtas till [!DNL Experience Platform] lagras de i profildatalagret. När inmatningen av poster i profilarkivet ökar eller minskar det totala antalet profiler med mer än 3 %, utlöses ett samplingsjobb för att uppdatera antalet. Hur provet utlöses beror på vilken typ av intag som används:

* För **direktuppspelningsarbetsflöden** görs en timkontroll för att avgöra om tröskelvärdet på 3 % har uppnåtts eller inte. Om den har det utlöses ett exempeljobb automatiskt för att uppdatera antalet.
* Om tröskelvärdet på 3 % ökning eller minskning är uppfyllt, körs ett jobb för att uppdatera antalet för **batchinmatning** inom 15 minuter efter att en batch har importerats till profilbutiken. Med hjälp av profil-API:t kan du förhandsgranska det senaste framgångsrika exempeljobbet samt lista profildistributionen per datauppsättning och per identitetsnamnområde.

Profilantal och profiler efter namnområdesmått är också tillgängliga i avsnittet [!UICONTROL Profiles] i Experience Platform-gränssnittet. Mer information om hur du får åtkomst till profildata via användargränssnittet finns i [[!DNL Profile] gränssnittshandboken](../ui/user-guide.md).

## Visa senaste exempelstatus {#view-last-sample-status}

Du kan visa information om det senaste slutförda exempeljobbet som kördes för din organisation genom att göra en GET-begäran till slutpunkten `/previewsamplestatus`. Den här rapporten innehåller det totala antalet profiler i exemplet, liksom antalet profiler, eller det totala antalet profiler som din organisation har inom Experience Platform.

Profilantalet genereras efter sammanfogning av profilfragment för att skapa en enda profil för varje enskild kund. När profilfragment sammanfogas returnerar de med andra ord antalet &quot;1&quot;-profiler eftersom de alla är relaterade till samma individ.

Profilantalet omfattar även både profiler med attribut (postdata) och profiler som endast innehåller tidsseriedata (händelsedata), t.ex. Adobe Analytics-profiler. Exempeljobbet uppdateras regelbundet när profildata importeras för att ge ett aktuellt totalt antal profiler inom Experience Platform.

**API-format**

```http
GET /previewsamplestatus
```

**Begäran**

+++ Ett exempel på en begäran om att visa den senaste samplingsstatusen.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 och innehåller information om det senaste slutförda samplingsjobbet som kördes för organisationen.

+++ Ett exempelsvar som innehåller den senaste samplingsstatusen.

>[!NOTE]
>
>I det här exempelsvaret är `numRowsToRead` och `totalRows` lika. Beroende på hur många profiler din organisation har i Experience Platform kan detta vara fallet. Vanligtvis är dessa två tal olika, och `numRowsToRead` är det mindre talet eftersom det representerar exemplet som en delmängd av det totala antalet profiler (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
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
| -------- | ----------- |
| `numRowsToRead` | Det totala antalet sammanfogade profiler i exemplet. |
| `sampleJobRunning` | Ett booleskt värde som returnerar `true` när ett provjobb pågår. Ger transparens i den fördröjning som uppstår när en gruppfil överförs till när den läggs till i profilarkivet. |
| `docCount` | Totalt antal dokument i databasen. |
| `totalFragmentCount` | Totalt antal profilfragment i profilarkivet. |
| `lastSuccessfulBatchTimestamp` | Senaste lyckade tidsstämpel för batchimport. |
| `streamingDriven` | *Det här fältet har tagits bort och innehåller ingen betydelse för svaret.* |
| `totalRows` | Totalt antal sammanfogade profiler i Experience Platform, även kallat profilantal. |
| `lastBatchId` | ID för senaste batchförbrukning. |
| `status` | Status för senaste prov. |
| `samplingRatio` | Förhållandet mellan de sammanfogade profiler som du har tagit prov på (`numRowsToRead`) och det totala antalet sammanfogade profiler (`totalRows`), uttryckt i procent i decimalformat. |
| `mergeStrategy` | Sammanfogningsstrategi som används i exemplet. |
| `lastSampledTimestamp` | Senaste lyckade exempeltidsstämpel. |

+++

## Visa profildistribution efter datauppsättning

Du kan se hur profiler distribueras per datauppsättning genom att göra en GET-begäran till slutpunkten `/previewsamplestatus/report/dataset`.

**API-format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Frågeparameter | Beskrivning | Exempel |
| --------------- | ----------- | ------- |
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅ-MM-DD. | `date=2024-12-31` |

**Begäran**

I följande begäran används parametern `date` för att returnera den senaste rapporten för det angivna datumet.

+++ En exempelbegäran om att hämta profildistributionen efter datauppsättning.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Svar**

>[!NOTE]
>
>Om det finns flera rapporter för datumet returneras bara den senaste rapporten. Om det inte finns någon datauppsättningsrapport för det angivna datumet returneras HTTP-status 404 (Hittades inte).

Ett lyckat svar returnerar HTTP-status 200 och innehåller en `data`-array som innehåller en lista med datauppsättningsobjekt.

+++ Ett exempelsvar som innehåller de senaste datauppsättningsobjekten.

>[!NOTE]
>
>Följande svar har trunkerats så att tre datauppsättningar visas.

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
| -------- | ----------- |
| `sampleCount` | Det totala antalet sammanfogade profiler i prov med detta datauppsättnings-ID. |
| `samplePercentage` | `sampleCount` som en procentandel av det totala antalet sammanfogade profiler i prov (värdet `numRowsToRead` som returneras i den [senaste exempelstatusen](#view-last-sample-status)), uttryckt i decimalformat. |
| `fullIDsCount` | Det totala antalet sammanfogade profiler med det här datauppsättnings-ID:t. |
| `fullIDsPercentage` | `fullIDsCount` som en procentandel av det totala antalet sammanfogade profiler (värdet `totalRows` som returnerades i den [senaste exempelstatusen](#view-last-sample-status)), uttryckt i decimalformat. |
| `name` | Namnet på datauppsättningen, som angavs när datauppsättningen skapades. |
| `description` | Beskrivningen av datauppsättningen, som den angavs när datauppsättningen skapades. |
| `value` | Datauppsättningens ID. |
| `streamingIngestionEnabled` | Anger om datauppsättningen är aktiverad för direktuppspelningsinmatning. |
| `createdUser` | Användar-ID för den användare som skapade datauppsättningen. |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date`-parameter angavs under begäran är den returnerade rapporten för det angivna datumet. Om ingen `date`-parameter anges returneras den senaste rapporten. |

+++

## Visa profildistribution efter ID-namnområde

Du kan utföra en GET-begäran till slutpunkten `/previewsamplestatus/report/namespace` om du vill visa uppdelningen efter identitetsnamnområde för alla sammanfogade profiler i din profilbutik. Detta omfattar både de standardidentiteter som tillhandahålls av Adobe och de anpassade identiteter som definieras av din organisation.

Identitetsnamnutrymmen är en viktig komponent i Adobe Experience Platform Identity Service som fungerar som indikatorer för det sammanhang som kunddata hör till. Om du vill veta mer börjar du med att läsa översikten över [identitetsnamnområdet](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>Det totala antalet profiler per namnutrymme (genom att lägga ihop värdena som visas för varje namnutrymme) kan vara högre än antalet profiler eftersom en profil kan kopplas till flera namnutrymmen. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

**API-format**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Frågeparameter | Beskrivning | Exempel |
| --------------- | ----------- | ------- |
| `date` | Anger datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: `YYYY-MM-DD`. | `date=2025-6-20` |

**Begäran**

Följande begäran anger ingen `date`-parameter och returnerar den senaste rapporten.

+++ Ett exempel på en begäran om att returnera den senaste rapporten för profildistribution efter namnutrymme. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 och innehåller en `data`-array, där individuella objekt innehåller information för varje namnområde. Svaret som visas har trunkerats så att fyra namnutrymmen visas.

+++ Ett exempelsvar innehåller information om profilfördelningen per namnutrymme.

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
| -------- | ----------- |
| `sampleCount` | Det totala antalet samkörda profiler i namnutrymmet. |
| `samplePercentage` | `sampleCount` som en procentandel av de sammanfogade profilerna (värdet `numRowsToRead` som returnerades i den [senaste exempelstatusen](#view-last-sample-status)), uttryckt i decimalformat. |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date`-parameter angavs under begäran är den returnerade rapporten för det angivna datumet. Om ingen `date`-parameter anges returneras den senaste rapporten. |
| `fullIDsFragmentCount` | Det totala antalet profilfragment i namnutrymmet. |
| `fullIDsCount` | Det totala antalet sammanfogade profiler i namnutrymmet. |
| `fullIDsPercentage` | `fullIDsCount` som en procentandel av det totala sammanslagna profilerna (värdet `totalRows` som returnerades i den [senaste exempelstatusen](#view-last-sample-status)), uttryckt i decimalformat. |
| `code` | `code` för namnutrymmet. Detta kan du hitta när du arbetar med namnutrymmen med hjälp av [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md) och kallas även [!UICONTROL Identity symbol] i Experience Platform-gränssnittet. Mer information finns i [översikten över identitetsnamnet](../../identity-service/features/namespaces.md). |
| `value` | Värdet `id` för namnutrymmet. Detta kan du hitta när du arbetar med namnutrymmen med hjälp av [identitetstjänstens API](../../identity-service/api/list-namespaces.md). |

+++

## Lista datauppsättningsstatistik {#dataset-stats}

Du kan generera en rapport som ger statistik om datauppsättningen genom att göra en GET-begäran till slutpunkten `/previewsamplestatus/report/dataset_stats`.

**API-format**

```http
GET /previewsamplestatus/report/dataset_stats
```

**Begäran**

+++ En exempelbegäran för att generera rapporten för datauppsättningsstatistik.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om datauppsättningens statistik.

+++ Ett exempelsvar som innehåller information om datauppsättningens statistik.

>[!NOTE]
>
>Följande svar har trunkerats så att tre datauppsättningar visas.

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `120days` | Antalet poster som kommer att finnas kvar i datauppsättningen efter att data har upphört att gälla i 120 dagar. |
| `14days` | Antalet poster som kommer att finnas kvar i datauppsättningen efter att data har gått ut i 14 dagar. |
| `30days` | Antalet poster som kommer att finnas kvar i datauppsättningen efter att data har upphört att gälla i 30 dagar. |
| `365days` | Antalet poster som kommer att finnas kvar i datauppsättningen efter att data har upphört att gälla i 365 dagar. |
| `60days` | Antalet poster som kommer att finnas kvar i datauppsättningen efter att data har upphört att gälla i 60 dagar. |
| `7days` | Antalet poster som kommer att finnas kvar i datauppsättningen efter en dataförfallotid på 7 dagar. |
| `90days` | Antalet poster som kommer att finnas kvar i datauppsättningen efter att data har upphört att gälla i 90 dagar. |
| `datasetId` | Datauppsättningens ID. |
| `datasetType` | Datamängdstypen. Värdet kan vara antingen `Profiles` eller `ExperienceEvents`. |
| `percentEvents` | Procentandel av Experience Events-poster som finns i datauppsättningen. |
| `percentProfiles` | Profilposter i procent som finns i datauppsättningen. |
| `profileFragments` | Det totala antalet profilfragment som finns i datauppsättningen. |
| `records` | Det totala antalet profilposter som har importerats till datauppsättningen. |
| `totalProfiles` | Det totala antalet profiler som har importerats till datauppsättningen. |

+++

## Nästa steg

Nu när du vet hur du förhandsgranskar exempeldata i profilarkivet och kör flera rapporter på data kan du även använda uppskattnings- och förhandsgranskningsslutpunkterna i segmenteringstjänstens API för att visa sammanfattningsnivåinformation om segmentdefinitionerna. Denna information hjälper er att isolera den förväntade målgruppen. Mer information om hur du arbetar med förhandsvisningar och uppskattningar med segmenterings-API:t finns i [förhandsgransknings- och uppskattningsguiden](../../segmentation/api/previews-and-estimates.md).

