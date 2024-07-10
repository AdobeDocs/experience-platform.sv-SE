---
solution: Experience Platform
title: Skapa en segmentdefinition med hjälp av segmenteringstjänstens API
type: Tutorial
description: Följ den här självstudiekursen för att lära dig hur du utvecklar, testar, förhandsgranskar och sparar en segmentdefinition med Adobe Experience Platform Segmentation Service API.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 0%

---

# Skapa en segmentdefinition med hjälp av segmenteringstjänstens API

Det här dokumentet innehåller en självstudiekurs för att utveckla, testa, förhandsgranska och spara en segmentdefinition med [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Mer information om hur du skapar segmentdefinitioner med användargränssnittet finns i [Segment Builder Guide](../ui/segment-builder.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika [!DNL Adobe Experience Platform] tjänster för att skapa segmentdefinitioner. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Används för att bygga målgrupper med segmentdefinitioner eller andra externa källor från kundprofildata i realtid.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ringa samtal till [!DNL Platform] API.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

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

- Content-Type: application/json

## Utveckla en segmentdefinition

Det första steget i segmenteringen är att definiera en segmentdefinition. En segmentdefinition är ett objekt som kapslar in en fråga skriven i [!DNL Profile Query Language] (PQL) Det här objektet kallas även för ett PQL-predikat. PQL förutser regler för segmentdefinitionen baserat på villkor som relaterar till data från post- eller tidsserier som du skickar till [!DNL Real-Time Customer Profile]. Se [PQL Guide](../pql/overview.md) för mer information om hur du skriver PQL-frågor.

Du kan skapa en ny segmentdefinition genom att göra en POST-förfrågan till `/segment/definitions` slutpunkt i [!DNL Segmentation] API. Följande exempel visar hur du formaterar en definitionsbegäran, inklusive vilken information som krävs för att en segmentdefinition ska kunna definieras korrekt.

En detaljerad förklaring om hur du definierar en segmentdefinition finns i [Utvecklarhandbok för segmentdefinition](../api/segment-definitions.md#create).

## Beräkna och förhandsgranska en målgrupp {#estimate-and-preview-an-audience}

När du utvecklar segmentdefinitionen kan du använda verktygen för uppskattning och förhandsgranskning i [!DNL Real-Time Customer Profile] för att se information på sammanfattningsnivå för att säkerställa att ni isolerar den förväntade målgruppen. Uppskattningar ger statistisk information om en segmentdefinition, t.ex. förväntad målgruppsstorlek och konfidensintervall. Förhandsvisningar innehåller sidnumrerade listor med kvalificeringsprofiler för en segmentdefinition, så att du kan jämföra resultaten med vad du förväntar dig.

Genom att uppskatta och förhandsgranska målgruppen kan ni testa och optimera era era PQL-predikat tills de ger önskat resultat, där de sedan kan användas i en uppdaterad segmentdefinition.

Det finns två nödvändiga steg för att förhandsgranska eller få en uppskattning av din segmentdefinition:

1. [Skapa ett förhandsgranskningsjobb](#create-a-preview-job)
2. [Visa uppskattning eller förhandsgranskning](#view-an-estimate-or-preview) med ID:t för förhandsgranskningsjobbet

### Hur uppskattningar genereras

När data som är aktiverade för kundprofilen i realtid hämtas till plattformen lagras de i profildatalagret. När inmatningen av poster i profilarkivet ökar eller minskar det totala antalet profiler med mer än 5 %, utlöses ett samplingsjobb för att uppdatera antalet. Om profilantalet inte ändras med mer än 5 % körs provtagningsjobbet automatiskt varje vecka.

Hur provet utlöses beror på vilken typ av intag som används:

- För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om detta tröskelvärde har uppnåtts aktiveras ett provjobb automatiskt för att uppdatera antalet.
- Om tröskelvärdet på 5 % ökning eller minskning uppnås, körs ett jobb för att uppdatera antalet vid batchintag inom 15 minuter efter att en batch har importerats till profilbutiken. Med hjälp av profil-API:t kan du förhandsgranska det senaste framgångsrika exempeljobbet samt lista profildistributionen per datauppsättning och per identitetsnamnområde.

Samplingsstorleken beror på det totala antalet enheter i din profilbutik. De här exempelstorlekarna visas i följande tabell:

| Enheter i profilarkivet | Samplingsstorlek |
| ------------------------- | ----------- |
| Mindre än 1 miljon | Fullständig datauppsättning |
| 1 till 20 miljoner | 1 miljon |
| Över 20 miljoner | 5 % av det totala |

Uppskattningar körs i allmänhet över 10-15 sekunder, med början med en grov uppskattning och förfining när fler poster läses.

### Skapa ett förhandsgranskningsjobb

Du kan skapa ett nytt förhandsgranskningsjobb genom att göra en POST-förfrågan till `/preview` slutpunkt.

Detaljerade anvisningar om hur du skapar ett förhandsgranskningsjobb finns i [guide för förhandsgranskningar och uppskattningar av slutpunkter](../api/previews-and-estimates.md#create-preview).

### Visa en uppskattning eller förhandsgranskning

Uppskattnings- och förhandsgranskningsprocesserna körs asynkront eftersom olika frågor kan ta olika lång tid att slutföra. När en fråga har initierats kan du använda API-anrop för att hämta (GET) det aktuella läget för uppskattningen eller förhandsgranskningen allt eftersom den fortskrider.

Använda [!DNL Segmentation Service] API, du kan söka efter ett förhandsgranskningsjobbs aktuella tillstånd med hjälp av dess ID. Om läget är &quot;RESULT_READY&quot; kan du visa resultatet. Om du vill söka efter ett förhandsgranskningsjobbs aktuella tillstånd kan du läsa avsnittet om [hämta ett förhandsgranskningsjobbavsnitt](../api/previews-and-estimates.md#get-preview) i förhandsgransknings- och uppskattningsguiden för slutpunkter. Om du vill söka efter ett uppskattningsjobbs aktuella tillstånd kan du läsa avsnittet om [hämta ett uppskattningsjobb](../api/previews-and-estimates.md#get-estimate) i förhandsgransknings- och uppskattningsguiden för slutpunkter.


## Nästa steg

När du har utvecklat, testat och sparat segmentdefinitionen kan du skapa ett segmentjobb för att skapa en målgrupp med [!DNL Segmentation Service] API. Se självstudiekursen om [utvärdera och komma åt segmentresultat](./evaluate-a-segment.md) för detaljerade steg om hur du uppnår detta.
