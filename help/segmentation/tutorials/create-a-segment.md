---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa ett segment
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 0%

---


# Skapa ett segment

Det här dokumentet innehåller en självstudiekurs för att utveckla, testa, förhandsgranska och spara en segmentdefinition med hjälp av [Segmenterings-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

Mer information om hur du skapar segment med användargränssnittet finns i guiden [](../ui/overview.md)Skapa segment.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika Adobe Experience Platform-tjänster som används för att skapa målgruppssegment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Segmenteringstjänsten](../home.md)Adobe Experience Platform: Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att ordna kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa Platform API:er.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla förfrågningar till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Utveckla en segmentdefinition

Det första steget i segmenteringen är att definiera ett segment, som representeras i en konstruktion som kallas **segmentdefinition**. En segmentdefinition är ett objekt som kapslar in en fråga skriven i PQL (Profile Query Language). Det här objektet kallas även för ett **PQL-predikat**. PQL beräknar regler för segmentet utifrån villkor som relaterar till data från poster eller tidsserier som du skickar till kundprofilen i realtid. Mer information om hur du skriver PQL-frågor finns i [PQL-guiden](../pql/overview.md) .

Du kan skapa en ny segmentdefinition genom att göra en POST-begäran till `/segment/definitions` slutpunkten i kundprofils-API:t i realtid. Följande exempel visar hur du formaterar en definitionsbegäran, inklusive vilken information som krävs för att ett segment ska kunna definieras korrekt.

Segmentdefinitioner kan utvärderas på två sätt - gruppsegmentering och direktuppspelningssegmentering. Gruppsegmentering utvärderar segment baserat på ett förinställt schema eller när utvärderingen aktiveras manuellt, medan direktuppspelningssegmentering utvärderar segment så snart data hämtas in i Platform. I den här självstudiekursen används **gruppsegmentering**. Mer information om direktuppspelningssegmentering finns i [översikten över direktuppspelningssegmentering](../api/streaming-segmentation.md).

**API-format**

```http
POST /segment/definitions
```

**Begäran**

Följande begäran skapar en ny segmentdefinition för ett schema med namnet&quot;MyProfile&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| Egenskap | Beskrivning |
| --------- | ------------ | 
| `name` | **Obligatoriskt.** Ett unikt namn som ska referera till segmentet. |
| `schema` | **Obligatoriskt.** Det schema som är associerat med entiteterna i segmentet. Består av antingen ett `id` eller `name` fält. |
| `expression` | **Obligatoriskt.** En entitet som innehåller fältinformation om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara PQL. |
| `expression.format` | Anger strukturen för uttrycket i värdet. Följande format stöds för närvarande: <ul><li>`pql/text`: En textbeteckning för en segmentdefinition enligt den publicerade PQL-grammatiken.  Exempel, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ett uttryck som överensstämmer med den typ som anges i `expression.format`. |
| `mergePolicyId` | Identifieraren för den sammanfogningsprincip som ska användas för exporterade data. Mer information finns i konfigurationsdokumentet för [sammanfogningsprinciper](../../profile/api/merge-policies.md). |
| `description` | En läsbar beskrivning av definitionen. |

**Svar**

Ett godkänt svar returnerar information om den nyligen skapade segmentdefinitionen, inklusive systemgenererad, skrivskyddad `id` som kommer att användas senare i kursen.

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## Beräkna och förhandsgranska en målgrupp {#estimate-and-preview-an-audience}

När ni utvecklar er segmentdefinition kan ni använda skattnings- och förhandsgranskningsverktygen i kundprofilen i realtid för att se information på sammanfattningsnivå för att säkerställa att ni isolerar den förväntade målgruppen. Uppskattningar ger statistisk information om en segmentdefinition, t.ex. förväntad målgruppsstorlek och konfidensintervall. Förhandsvisningar innehåller sidnumrerade listor med kvalificeringsprofiler för en segmentdefinition, så att du kan jämföra resultaten med vad du förväntar dig.

Genom att uppskatta och förhandsgranska målgruppen kan ni testa och optimera PQL-predikaten tills de ger önskat resultat, där de sedan kan användas i en uppdaterad segmentdefinition.

Du måste utföra två steg för att förhandsgranska eller få en uppskattning av ditt segment:

1. [Skapa ett förhandsgranskningsjobb](#create-a-preview-job)
2. [Visa uppskattning eller förhandsgranskning](#view-an-estimate-or-preview) med ID:t för förhandsgranskningsjobbet

### Hur uppskattningar genereras

Dataprover används för att utvärdera segment och uppskatta antalet kvalificerade profiler. Nya data läses in i minnet varje morgon (mellan 12AM-2AM PT, som är 7-9AM UTC), och alla segmenteringsfrågor beräknas med hjälp av den dagens exempeldata. Alla nya fält som läggs till eller ytterligare uppgifter som samlas in kommer därför att återspeglas i beräkningarna följande dag.

Samplingsstorleken beror på det totala antalet enheter i din profilbutik. De här exempelstorlekarna visas i följande tabell:

| Enheter i profilarkivet | Samplingsstorlek |
| ------------------------- | ----------- |
| Mindre än 1 miljon | Fullständig datauppsättning |
| 1 till 20 miljoner | 1 miljon |
| Över 20 miljoner | 5 % av det totala |

Uppskattningar körs i allmänhet över 10-15 sekunder, med början med en grov uppskattning och förfining när fler poster läses.

### Skapa ett förhandsgranskningsjobb

Du kan skapa ett nytt förhandsgranskningsjobb genom att göra en POST-begäran till `/preview` slutpunkten.

**API-format**

```http
POST /preview
```

**Begäran**

Följande begäran skapar ett nytt förhandsgranskningsjobb. Begärandetexten innehåller den frågeinformation som är relaterad till segmentet.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `predicateExpression` | PQL-uttrycket som data ska frågas efter. |
| `predicateModel` | Namnet på XDM-schemat som profildata baseras på. |

**Svar**

Ett godkänt svar returnerar information om det nya förhandsgranskningsjobbet, inklusive dess ID och det aktuella bearbetningstillståndet.

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `state` | Det aktuella läget för förhandsgranskningsjobbet. Den kommer att vara i tillståndet &quot;RUNNING&quot; tills bearbetningen är klar, och då blir den &quot;RESULT_READY&quot; eller &quot;FAILED&quot;. |
| `previewId` | ID:t för förhandsgranskningsjobbet, som ska användas för uppslagssyften när du visar en uppskattning eller förhandsgranskning, enligt beskrivningen i följande avsnitt. |

### Visa en uppskattning eller förhandsgranskning

Uppskattnings- och förhandsgranskningsprocesserna körs asynkront eftersom olika frågor kan ta olika lång tid att slutföra. När en fråga har initierats kan du använda API-anrop för att hämta (GET) det aktuella läget för uppskattningen eller förhandsgranskningen medan den fortlöper.

Med hjälp av kundprofils-API:t i realtid kan du söka efter ett förhandsgranskningsjobbs aktuella tillstånd med hjälp av dess ID. Om läget är &quot;RESULT_READY&quot; kan du visa resultatet. Beroende på om du vill visa en uppskattning eller en förhandsgranskning har varje slutpunkt sin egen i API:t. Exempel på båda finns nedan.

### Visa en uppskattning

**API-format**

```http
GET /estimate/{PREVIEW_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID:t för det förhandsgranskningsjobb som du vill visa. |

**Begäran**

Följande begäran hämtar en uppskattning med hjälp av det som `previewId` skapades i föregående steg.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om uppskattningen.

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `state` | Det aktuella läget för förhandsgranskningsjobbet. KÖRS tills bearbetningen är slutförd och blir då RESULT_READY eller FAILED. |
| `_links.preview` | När förhandsgranskningsjobbets aktuella tillstånd är &quot;RESULT_READY&quot;, ger det här attributet en URL för att visa uppskattningen. |

### Visa en förhandsgranskning

**API-format**

```http
GET /preview/{PREVIEW_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID:t för det förhandsgranskningsjobb som du vill visa. |

**Begäran**

Följande begäran hämtar en förhandsgranskning med hjälp av den som `previewId` skapades i föregående steg.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar information om förhandsgranskningen.

```json
{
   "results": [{
         "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
               "XID_COOKIE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
               },
               "XID_PROFILE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
               }
            }
         }
      },
      {
         "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
               "XID_COOKIE_ID_2-1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

               },
               "XID_PROFILE_ID_2": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
               }
            }
         },
         "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
         },
         "state": "RESULT_READY",
         "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
         }
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## Nästa steg

När du har utvecklat, testat och sparat segmentdefinitionen kan du skapa ett segmentjobb för att bygga en målgrupp med hjälp av kundprofils-API:t i realtid. I självstudiekursen om [utvärdering och åtkomst av segmentresultat](./evaluate-a-segment.md) finns detaljerade anvisningar om hur du gör detta.