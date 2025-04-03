---
solution: Experience Platform
title: Skapa en segmentdefinition med hjälp av segmenteringstjänstens API
type: Tutorial
description: Följ den här självstudiekursen för att lära dig hur du utvecklar, testar, förhandsgranskar och sparar en segmentdefinition med Adobe Experience Platform Segmentation Service API.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 0%

---

# Skapa en segmentdefinition med hjälp av segmenteringstjänstens API

Det här dokumentet innehåller en självstudiekurs för att utveckla, testa, förhandsgranska och spara en segmentdefinition med [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Mer information om hur du skapar segmentdefinitioner med användargränssnittet finns i [guiden för segmentbyggaren](../ui/segment-builder.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform]-tjänster som används för att skapa segmentdefinitioner. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Gör att du kan skapa målgrupper med segmentdefinitioner eller andra externa källor från kundprofildata i realtid.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med. För att du ska kunna använda segmentering bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:erna för [!DNL Experience Platform].

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare ett huvud:

- Content-Type: application/json

## Utveckla en segmentdefinition

Det första steget i segmenteringen är att definiera en segmentdefinition. En segmentdefinition är ett objekt som kapslar in en fråga skriven i [!DNL Profile Query Language] (PQL). Det här objektet kallas även för ett PQL-predikat. PQL förutsäger regler för segmentdefinitionen baserat på villkor som relaterar till alla post- eller tidsseriedata som du skickar till [!DNL Real-Time Customer Profile]. Mer information om hur du skriver PQL-frågor finns i [PQL-handboken](../pql/overview.md).

Du kan skapa en ny segmentdefinition genom att göra en POST-begäran till `/segment/definitions`-slutpunkten i [!DNL Segmentation] API. Följande exempel visar hur du formaterar en definitionsbegäran, inklusive vilken information som krävs för att en segmentdefinition ska kunna definieras korrekt.

En detaljerad förklaring om hur du definierar en segmentdefinition finns i [utvecklarhandboken för segmentdefinitioner](../api/segment-definitions.md#create).

## Beräkna och förhandsgranska en målgrupp {#estimate-and-preview-an-audience}

När du utvecklar din segmentdefinition kan du använda verktygen för uppskattning och förhandsgranskning i [!DNL Real-Time Customer Profile] för att visa information på sammanfattningsnivå för att säkerställa att du isolerar den förväntade målgruppen. Uppskattningar ger statistisk information om en segmentdefinition, t.ex. förväntad målgruppsstorlek och konfidensintervall. Förhandsvisningar innehåller sidnumrerade listor med kvalificeringsprofiler för en segmentdefinition, så att du kan jämföra resultaten med vad du förväntar dig.

Genom att uppskatta och förhandsgranska målgruppen kan ni testa och optimera era era PQL-predikat tills de ger önskat resultat, där de sedan kan användas i en uppdaterad segmentdefinition.

Det finns två nödvändiga steg för att förhandsgranska eller få en uppskattning av din segmentdefinition:

1. [Skapa ett förhandsgranskningsjobb](#create-a-preview-job)
2. [Visa uppskattning eller förhandsgranskning](#view-an-estimate-or-preview) med ID:t för förhandsgranskningsjobbet

### Hur uppskattningar genereras

När data som har aktiverats för kundprofilen i realtid hämtas till Experience Platform lagras de i profildatalagret. När inmatningen av poster i profilarkivet ökar eller minskar det totala antalet profiler med mer än 5 %, utlöses ett samplingsjobb för att uppdatera antalet. Om profilantalet inte ändras med mer än 5 % körs provtagningsjobbet automatiskt varje vecka.

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

Du kan skapa ett nytt förhandsgranskningsjobb genom att göra en POST-begäran till slutpunkten `/preview`.

Detaljerade instruktioner om hur du skapar ett förhandsgranskningsjobb finns i guiden [för förhandsvisningar och uppskattningar av slutpunkter](../api/previews-and-estimates.md#create-preview).

### Visa en uppskattning eller förhandsgranskning

Uppskattnings- och förhandsgranskningsprocesserna körs asynkront eftersom olika frågor kan ta olika lång tid att slutföra. När en fråga har initierats kan du använda API-anrop för att hämta (GET) det aktuella läget för uppskattningen eller förhandsgranskningen allt eftersom den fortskrider.

Med API:t [!DNL Segmentation Service] kan du slå upp ett förhandsgranskningsjobbs aktuella tillstånd med dess ID. Om läget är &quot;RESULT_READY&quot; kan du visa resultatet. Läs avsnittet [Hämta ett förhandsgranskningsjobbavsnitt](../api/previews-and-estimates.md#get-preview) i guiden för förhandsgranskningar och uppskattningar om du vill söka efter ett förhandsgranskningsjobbs aktuella tillstånd. Läs avsnittet [Hämta ett uppskattningsjobb](../api/previews-and-estimates.md#get-estimate) i guiden för förhandsgranskningar och uppskattningar av slutpunkter om du vill söka efter ett uppskattningsjobbs aktuella tillstånd.


## Nästa steg

När du har utvecklat, testat och sparat segmentdefinitionen kan du skapa ett segmentjobb för att skapa en målgrupp med hjälp av [!DNL Segmentation Service]-API:t. I självstudiekursen [Utvärderar och får åtkomst till segmentresultat](./evaluate-a-segment.md) finns detaljerade anvisningar om hur du gör detta.
