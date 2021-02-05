---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;förhandsvisning;exempel
title: API-slutpunkt för profilexempelstatus
description: Med hjälp av API-slutpunkter för kundprofiler i realtid kan du förhandsgranska det senaste framgångsrika exemplet av dina profildata samt lista profildistribution per datauppsättning och per ID-namnområde i Adobe Experience Platform.
topic: guide
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 0%

---


# Förhandsgranska exempelstatusslutpunkt (förhandsgranskning av profil)

Med Adobe Experience Platform kan ni importera kunddata från flera olika källor och skapa stabila, enhetliga profiler för enskilda kunder. När data som har aktiverats för kundprofilen i realtid hämtas till [!DNL Platform] lagras de i profildatalagret.

När inmatningen av poster i profilarkivet ökar eller minskar det totala antalet profiler med mer än 5 %, utlöses ett jobb för att uppdatera antalet. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet. Om tröskelvärdet på 5 % ökning eller minskning uppnås, körs ett jobb för att uppdatera antalet vid batchintag inom 15 minuter efter att en batch har importerats till profilbutiken. Med hjälp av profil-API:t kan du förhandsgranska det senaste framgångsrika exempeljobbet samt lista profildistributionen per datauppsättning och per identitetsnamnområde.

Dessa mått är också tillgängliga i [!UICONTROL Profiles]-avsnittet i användargränssnittet för Experience Platform. Mer information om hur du får åtkomst till profildata via användargränssnittet finns i [[!DNL Profile] användarhandboken](../ui/user-guide.md).

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Real-time Customer Profile] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa valfritt [!DNL Experience Platform]-API.

## Profilfragment jämfört med sammanslagna profiler

Den här guiden refererar till både profilfragment och sammanfogade profiler. Det är viktigt att förstå skillnaden mellan dessa villkor innan du fortsätter.

Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de (baserat på sammanfogningspolicyn) för att skapa en enda profil för kunden. Det totala antalet profilfragment är därför sannolikt alltid högre än det totala antalet sammanfogade profiler, eftersom varje profil består av flera fragment.

## Visa senaste exempelstatus {#view-last-sample-status}

Du kan utföra en GET-förfrågan till `/previewsamplestatus`-slutpunkten för att visa information om det senaste slutförda samplingsjobbet som kördes för din IMS-organisation. Detta inkluderar det totala antalet profiler i exemplet, liksom antalet profiler eller det totala antalet profiler som din organisation har i Experience Platform. Profilantalet genereras efter sammanfogning av profilfragment till en enda profil för varje enskild kund. Med andra ord kan din organisation ha flera profilfragment kopplade till en enskild kund som interagerar med ert varumärke i olika kanaler, men dessa fragment skulle slås samman (enligt standardprincipen för sammanslagning) och skulle returnera antalet&quot;1&quot;-profil eftersom de alla är kopplade till samma individ.

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

Svaret innehåller information om det senaste exempeljobbet som kördes för IMS-organisationen.

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
| `totalRows` | Totalt antal sammanfogade profiler i Experience-plattformen, även kallat &#39;antal profiler&#39;. |
| `lastBatchId` | ID för senaste batchförbrukning. |
| `status` | Status för det senaste exemplet. |
| `samplingRatio` | Förhållandet mellan de sammanslagna profiler som du har tagit prov på (`numRowsToRead`) och de totala sammanslagna profilerna (`totalRows`), uttryckt i procent i decimalformat. |
| `mergeStrategy` | Sammanfogningsstrategi som används i exemplet. |
| `lastSampledTimestamp` | Senaste lyckade exempeltidsstämpel. |

## Visa profildistribution efter datauppsättning

Om du vill visa profildistributionen efter datauppsättning kan du utföra en GET-begäran till `/previewsamplestatus/report/dataset`-slutpunkten.

**API-format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel. Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅÅ-MM-DD Exempel: `date=2024-12-31` |

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
>Om det fanns flera rapporter för datumet returneras bara det senaste. Om det inte finns någon datauppsättningsrapport för det angivna datumet returneras HTTP-status 404 (Hittades inte).

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



## Visa profildistribution efter namnområde

Du kan utföra en GET-begäran till `/previewsamplestatus/report/namespace`-slutpunkten för att visa uppdelningen efter identitetsnamnområde för alla sammanfogade profiler i profilarkivet. Identitetsnamnutrymmen är en viktig komponent i Adobe Experience Platform Identity Service som fungerar som indikatorer för det sammanhang som kunddata hör till. Mer information finns i [översikten över identitetsnamnet](../../identity-service/namespaces.md).

>[!NOTE]
>
>Det totala antalet profiler per namnutrymme (genom att lägga ihop värdena som visas för varje namnutrymme) kommer alltid att vara högre än antalet profiler eftersom en profil kan kopplas till flera namnutrymmen. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

**API-format**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel. Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅÅ-MM-DD Exempel: `date=2024-12-31` |

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

## Nästa steg

Du kan också använda liknande uppskattningar och förhandsgranskningar för att visa information på sammanfattningsnivå om segmentdefinitionerna för att säkerställa att du isolerar den förväntade målgruppen. Om du vill hitta detaljerade steg för att arbeta med förhandsgranskningar och uppskattningar av segment med hjälp av API:t [!DNL Adobe Experience Platform Segmentation Service] kan du gå till guiden [för förhandsgranskningar och uppskattningar av slutpunkter](../../segmentation/api/previews-and-estimates.md), som ingår i utvecklarhandboken för [!DNL Segmentation] API.

