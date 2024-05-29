---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;förhandsvisning;exempel
title: API-slutpunkt för exempelstatus för förhandsgranskning (förhandsgranskning av profil)
description: Med slutpunkten för förhandsgranskning av exempelstatus i API:t för kundprofiler i realtid kan du förhandsgranska det senaste framgångsrika exemplet av dina profildata, lista profildistribution per datauppsättning och identitet och generera rapporter som visar dataset överlappning, identitetsöverlappning och icke sammansatta profiler.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2901'
ht-degree: 0%

---

# Förhandsgranska exempelstatusslutpunkt (förhandsgranskning av profil)

Med Adobe Experience Platform kan ni importera kunddata från flera olika källor för att skapa en robust, enhetlig profil för varje enskild kund. När data hämtas till Platform körs ett exempeljobb för att uppdatera profilantalet och andra datarelaterade mått för kundprofiler i realtid.

Resultaten av det här exempeljobbet kan visas med `/previewsamplestatus` slutpunkt, som ingår i Real-Time Customer Profile API. Den här slutpunkten kan också användas för att lista profildistributioner av både datauppsättningen och identitetsnamnutrymmet, samt för att generera flera rapporter för att få synlighet i kompositionen för organisationens profilarkiv. Den här guiden går igenom de steg som krävs för att visa måtten med hjälp av `/previewsamplestatus` API-slutpunkt.

>[!NOTE]
>
>Det finns uppskattnings- och förhandsgranskningsslutpunkter som ingår i Adobe Experience Platform Segmentation Service API som gör att du kan visa information på sammanfattningsnivå om segmentdefinitioner så att du kan isolera den förväntade målgruppen. Om du vill ha mer information om hur du arbetar med förhandsgranskning och beräkning av slutpunkter kan du gå till [guide för förhandsgranskningar och uppskattningar av slutpunkter](../../segmentation/api/previews-and-estimates.md), en del av [!DNL Segmentation] Utvecklarhandbok för API.

## Komma igång

API-slutpunkten som används i den här guiden är en del av [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Innan du fortsätter bör du granska [komma igång-guide](getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anrop i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna ringa anrop till [!DNL Experience Platform] API.

## Profilfragment jämfört med sammanslagna profiler

Den här guiden refererar till både profilfragment och sammanfogade profiler. Det är viktigt att förstå skillnaden mellan dessa villkor innan du fortsätter.

Varje enskild kundprofil består av flera profilfragment som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med varumärket i flera kanaler har organisationen troligen flera profilfragment som är kopplade till den enskilda kunden i flera datauppsättningar.

När profilfragment hämtas till Platform sammanfogas de (baserat på en sammanfogningspolicy) för att skapa en enda profil för den kunden. Det totala antalet profilfragment är därför sannolikt alltid högre än det totala antalet sammanfogade profiler, eftersom varje profil består av flera fragment.

Om du vill veta mer om profiler och deras roll i Experience Platform börjar du med att läsa [Översikt över kundprofiler i realtid](../home.md).

## Hur exempeljobbet utlöses

Som data som är aktiverade för kundprofilen i realtid hämtas till [!DNL Platform]lagras den i datalagret Profil. När inmatningen av poster i profilarkivet ökar eller minskar det totala antalet profiler med mer än 5 %, utlöses ett samplingsjobb för att uppdatera antalet. Hur provet utlöses beror på vilken typ av intag som används:

* För **arbetsflöden för strömmande data** kontrolleras dock timvis för att avgöra om tröskelvärdet på 5 % har uppnåtts. Om den har det utlöses ett exempeljobb automatiskt för att uppdatera antalet.
* För **batchintag**, inom 15 minuter efter att en batch har importerats till profilbutiken, körs ett jobb för att uppdatera antalet om tröskelvärdet på 5 % har uppnåtts. Med hjälp av profil-API:t kan du förhandsgranska det senaste framgångsrika exempeljobbet samt lista profildistributionen per datauppsättning och per identitetsnamnområde.

Profilantal och profiler efter namnutrymmesmått är också tillgängliga i [!UICONTROL Profiles] i användargränssnittet i Experience Platform. Mer information om hur du får åtkomst till profildata via användargränssnittet finns på [[!DNL Profile] Användargränssnittsguide](../ui/user-guide.md).

## Visa senaste exempelstatus {#view-last-sample-status}

Du kan göra en GET-förfrågan till `/previewsamplestatus` slutpunkt för att visa information om det senaste slutförda exempeljobbet som kördes för din organisation. Detta inkluderar det totala antalet profiler i exemplet, liksom antalet profiler eller det totala antalet profiler som din organisation har i Experience Platform.

Profilantalet genereras efter sammanfogning av profilfragment för att skapa en enda profil för varje enskild kund. När profilfragment sammanfogas returnerar de med andra ord antalet &quot;1&quot;-profiler eftersom de alla är relaterade till samma individ.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller information om det senaste slutförda exempeljobbet som kördes för organisationen.

>[!NOTE]
>
>I det här exemplet är svaret `numRowsToRead` och `totalRows` är lika med varandra. Beroende på hur många profiler din organisation har i Experience Platform kan detta vara fallet. Vanligtvis är dessa två tal olika, med `numRowsToRead` är det mindre talet eftersom det representerar exemplet som en delmängd av det totala antalet profiler (`totalRows`).

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
| `sampleJobRunning` | Ett booleskt värde som returnerar `true` när ett exempeljobb pågår. Ger transparens i den fördröjning som uppstår när en gruppfil överförs till när den läggs till i profilarkivet. |
| `cosmosDocCount` | Totalt antal dokument i Cosmos. |
| `totalFragmentCount` | Totalt antal profilfragment i profilarkivet. |
| `lastSuccessfulBatchTimestamp` | Senaste lyckade tidsstämpel för batchimport. |
| `streamingDriven` | *Detta fält har tagits bort och innehåller ingen betydelse för svaret.* |
| `totalRows` | Totalt antal sammanfogade profiler i Experience Platform, även kallat &#39;antal profiler&#39;. |
| `lastBatchId` | ID för senaste batchförbrukning. |
| `status` | Status för senaste prov. |
| `samplingRatio` | Proportionerna för de sammanslagna profilerna (`numRowsToRead`) till totalt antal sammanfogade profiler (`totalRows`), uttryckt i procent i decimalformat. |
| `mergeStrategy` | Sammanfogningsstrategi som används i exemplet. |
| `lastSampledTimestamp` | Senaste lyckade exempeltidsstämpel. |

## Visa profildistribution efter datauppsättning

Om du vill se profildistributionen per datauppsättning kan du utföra en GET-förfrågan till `/previewsamplestatus/report/dataset` slutpunkt.

**API-format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅ-MM-DD. Exempel: `date=2024-12-31` |

**Begäran**

Följande begäran använder `date` parameter för att returnera den senaste rapporten för det angivna datumet.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller en `data` -array, som innehåller en lista med datauppsättningsobjekt. Svaret som visas har trunkerats så att tre datauppsättningar visas.

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
| `samplePercentage` | The `sampleCount` som en procentandel av det totala antalet sammanfogade profiler i prov ( `numRowsToRead` det returnerade värdet i [senaste exempelstatus](#view-last-sample-status)), uttryckt i decimalformat. |
| `fullIDsCount` | Det totala antalet sammanfogade profiler med det här datauppsättnings-ID:t. |
| `fullIDsPercentage` | The `fullIDsCount` som en procentandel av det totala antalet sammanfogade profiler ( `totalRows` det returnerade värdet i [senaste exempelstatus](#view-last-sample-status)), uttryckt i decimalformat. |
| `name` | Namnet på datauppsättningen, som angavs när datauppsättningen skapades. |
| `description` | Beskrivningen av datauppsättningen, som den angavs när datauppsättningen skapades. |
| `value` | Datauppsättningens ID. |
| `streamingIngestionEnabled` | Anger om datauppsättningen är aktiverad för direktuppspelningsinmatning. |
| `createdUser` | Användar-ID för den användare som skapade datauppsättningen. |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date` parametern angavs under begäran, rapporten returneras för angivet datum. Om nej `date` parametern anges, den senaste rapporten returneras. |

## Visa profildistribution efter ID-namnområde

Du kan göra en GET-förfrågan till `/previewsamplestatus/report/namespace` slutpunkt för att visa uppdelningen efter ID-namnutrymme för alla sammanfogade profiler i din profilbutik. Detta omfattar både standardidentiteter från Adobe och anpassade identiteter som definieras av organisationen.

Identitetsnamnutrymmen är en viktig komponent i Adobe Experience Platform Identity Service som fungerar som indikatorer för det sammanhang som kunddata hör till. Om du vill veta mer börjar du med att läsa [Översikt över namnutrymmet identity](../../identity-service/features/namespaces.md).

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
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på datumet returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅ-MM-DD. Exempel: `date=2024-12-31` |

**Begäran**

Följande begäran anger inte en `date` parametern och returnerar därför den senaste rapporten.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller en `data` array, med enskilda objekt som innehåller information för varje namnutrymme. Svaret som visas har trunkerats så att fyra namnutrymmen visas.

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
| `samplePercentage` | The `sampleCount` som en procentandel av de sammanfogade profilerna ( `numRowsToRead` det returnerade värdet i [senaste exempelstatus](#view-last-sample-status)), uttryckt i decimalformat. |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date` parametern angavs under begäran, rapporten returneras för angivet datum. Om nej `date` parametern anges, den senaste rapporten returneras. |
| `fullIDsFragmentCount` | Det totala antalet profilfragment i namnutrymmet. |
| `fullIDsCount` | Det totala antalet sammanfogade profiler i namnutrymmet. |
| `fullIDsPercentage` | The `fullIDsCount` som en procentandel av det totala antalet sammanfogade profiler ( `totalRows` det returnerade värdet i [senaste exempelstatus](#view-last-sample-status)), uttryckt i decimalformat. |
| `code` | The `code` för namnutrymmet. Detta kan du hitta när du arbetar med namnutrymmen med [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md) och kallas även [!UICONTROL Identity symbol] i användargränssnittet i Experience Platform. Mer information finns på [Översikt över namnutrymmet identity](../../identity-service/features/namespaces.md). |
| `value` | The `id` namnutrymmets värde. Detta kan du hitta när du arbetar med namnutrymmen med [Identitetstjänstens API](../../identity-service/api/list-namespaces.md). |

## Generera överlappningsrapport för datauppsättning

Rapporten om överlappning av datauppsättningar ger synlighet i kompositionen för organisationens profilbutik genom att visa de datauppsättningar som bidrar mest till den adresserbara målgruppen (sammanslagna profiler). Förutom att ge insikter om era data kan den här rapporten hjälpa er att vidta åtgärder för att optimera licensanvändningen, som att ange förfallodatum för vissa datauppsättningar.

Du kan generera en överlappningsrapport för datauppsättningen genom att utföra en GET-förfrågan till `/previewsamplestatus/report/dataset/overlap` slutpunkt.

Stegvisa instruktioner om hur man skapar en överlappande rapport för datauppsättningen med kommandoraden eller användargränssnittet i Postman finns i [generera rapporten om datauppöverlappning](../tutorials/dataset-overlap-report.md).

**API-format**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på samma datum returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅ-MM-DD. Exempel: `date=2024-12-31` |

**Begäran**

Följande begäran använder `date` parameter för att returnera den senaste rapporten för det angivna datumet.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `data` | The `data` -objektet innehåller kommaavgränsade listor med datauppsättningar och deras respektive profilantal. |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date` parametern angavs under begäran, rapporten returneras för angivet datum. Om nej `date` parametern anges, den senaste rapporten returneras. |

### Tolka överlappningsrapporten för datauppsättningen

Resultatet av rapporten kan tolkas utifrån datauppsättningar och antal profiler i svaret. Titta på följande exempelrapport `data` objekt:

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

## Generera rapport över namnutrymmesöverlappning {#identity-overlap-report}

Rapporten om överlappning av identitetsnamn ger synlighet i sammansättningen av organisationens profilarkiv genom att visa de identitetsnamnutrymmen som bidrar mest till den adresserbara målgruppen (sammanslagna profiler). Detta omfattar både de vanliga identitetsnamnutrymmena från Adobe och de anpassade identitetsnamnutrymmen som definieras av din organisation.

Du kan generera en rapport om namnutrymmesöverlappning genom att utföra en GET-begäran till `/previewsamplestatus/report/namespace/overlap` slutpunkt.

**API-format**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `date` | Ange datumet för rapporten som ska returneras. Om flera rapporter kördes på samma datum returneras den senaste rapporten för det datumet. Om det inte finns någon rapport för det angivna datumet returneras ett 404-fel (Hittades inte). Om inget datum anges returneras den senaste rapporten. Format: ÅÅÅ-MM-DD. Exempel: `date=2024-12-31` |

**Begäran**

Följande begäran använder `date` parameter för att returnera den senaste rapporten för det angivna datumet.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Svar**

En lyckad begäran returnerar HTTP-status 200 (OK) och identitetsnamnutrymmets överlappningsrapport.

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
| `data` | The `data` -objektet innehåller kommaavgränsade listor med unika kombinationer av ID-namnområdeskoder och deras respektive profilantal. |
| Namnområdeskoder | The `code` är ett kort formulär för varje namn på identitetsnamn. En mappning av varje `code` till `name` kan hittas med [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md). The `code` kallas även [!UICONTROL Identity symbol] i användargränssnittet i Experience Platform. Mer information finns på [Översikt över namnutrymmet identity](../../identity-service/features/namespaces.md). |
| `reportTimestamp` | Rapportens tidsstämpel. Om en `date` parametern angavs under begäran, rapporten returneras för angivet datum. Om nej `date` parametern anges, den senaste rapporten returneras. |

### Tolka rapporten om namnutrymmesöverlappning

Resultatet av rapporten kan tolkas utifrån identiteten och antalet profiler i svaret. Det numeriska värdet för varje rad visar hur många profiler som består av den exakta kombinationen av standard- och anpassade identitetsnamnutrymmen.

Titta på följande utdrag från `data` objekt:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Den här rapporten innehåller följande information:

* Det finns 142 profiler som består av `AAID`, `ECID`och `Email` standardidentiteter, liksom från en anpassad `crmid` identity namespace.
* Det finns 24 profiler som består av `AAID` och `ECID` ID-namnutrymmen.
* Det finns 6 565 profiler som bara innehåller en `ECID` identitet.

## Generera rapport över profiler som inte sammanställts

Du kan få mer insyn i hur din organisations profilbutik är uppbyggd genom rapporten för icke sammansatta profiler. En &quot;sammanfogad&quot; profil är en profil som bara innehåller ett profilfragment. En&quot;okänd&quot; profil är en profil som associeras med pseudonyma identitetsnamnutrymmen som `ECID` och `AAID`. Okända profiler är inaktiva, vilket innebär att de inte har lagt till nya händelser under den angivna tidsperioden. I rapporten för icke sammansatta profiler finns en beskrivning av profilerna för en period på 7, 30, 60, 90 och 120 dagar.

Du kan generera rapporten för icke sammansatta profiler genom att göra en GET-förfrågan till `/previewsamplestatus/report/unstitchedProfiles` slutpunkt.

**API-format**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**Begäran**

Följande begäran returnerar rapporten för profiler utan sammanfogning.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Svar**

En slutförd begäran returnerar HTTP-status 200 (OK) och rapporten för icke-sammansatta profiler.

>[!NOTE]
>
>I den här guiden har rapporten trunkerats till att endast innehålla `"120days"` och &quot;`7days`&quot; tidsperioder. Den fullständiga rapporten över icke sammansatta profiler innehåller en beskrivning av profilerna för en period på 7, 30, 60, 90 och 120 dagar.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| Egenskap | Beskrivning |
|---|---|
| `data` | The `data` -objektet innehåller den information som returneras för rapporten för icke-sammansatta profiler. |
| `totalNumberOfProfiles` | Det totala antalet unika profiler i profilarkivet. Detta motsvarar antalet adresserbara målgrupper. Den innehåller både kända och osydda profiler. |
| `totalNumberOfEvents` | Det totala antalet ExperienceEvents i profilarkivet. |
| `unstitchedProfiles` | Ett objekt som innehåller en uppdelning av icke sammanfogade profiler efter tidsperiod. I rapporten för icke sammansatta profiler finns en beskrivning av profiler för tidsperioderna 7, 30, 60, 90 och 120 dagar. |
| `countOfProfiles` | Antalet profiler som inte sammanfogats för tidsperioden eller antalet profiler som inte sammanfogats för namnutrymmet. |
| `eventsAssociated` | Antalet ExperienceEvents för tidsintervallet eller antalet händelser för namnutrymmet. |
| `nsDistribution` | Ett objekt som innehåller enskilda identitetsnamnutrymmen med distributionen av osydda profiler och händelser för varje namnutrymme. Obs! Lägg samman summan `countOfProfiles` för varje identitetsnamnutrymme i `nsDistribution` är lika med `countOfProfiles` för tidsperioden. Detsamma gäller `eventsAssociated` per namnutrymme och totalt `eventsAssociated` per tidsperiod. |
| `reportTimestamp` | Rapportens tidsstämpel. |

### Tolka rapporten över icke sammansatta profiler

Resultaten av rapporten ger insikt i hur många icke-sammansatta och inaktiva profiler din organisation har i sin profilbutik.

Titta på följande utdrag från `data` objekt:

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

Den här rapporten innehåller följande information:

* Det finns 1 782 profiler som bara innehåller ett profilfragment och som inte har några nya händelser de senaste sju dagarna.
* Det finns 29 151 ExperienceEvents associerade med de 1 782 icke-sammansatta profilerna.
* Det finns 1 734 osydda profiler som innehåller ett enda profilfragment från ECID-identitetsnamnområdet.
* Det finns 28 591 händelser som är associerade med de 1 734 icke-sammansatta profilerna som innehåller ett enda profilfragment från ECID-identitetsnamnområdet.

## Nästa steg

Nu när du vet hur du förhandsgranskar exempeldata i profilarkivet och kör flera rapporter på data kan du även använda uppskattnings- och förhandsgranskningsslutpunkterna i segmenteringstjänstens API för att visa sammanfattningsnivåinformation om segmentdefinitionerna. Denna information hjälper er att isolera den förväntade målgruppen. Läs mer om hur du arbetar med förhandsgranskningar och uppskattningar med segmenterings-API:t på [guide för att förhandsgranska och beräkna slutpunkter](../../segmentation/api/previews-and-estimates.md).

