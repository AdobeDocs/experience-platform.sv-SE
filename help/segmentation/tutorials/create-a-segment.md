---
keywords: Experience Platform;hemmabruk;populära ämnen;segment;skapa segment;segmentering;skapa ett segment;segmenteringstjänst;
solution: Experience Platform
title: Skapa ett segment
topic: tutorial
type: Tutorial
description: Det här dokumentet innehåller en självstudiekurs för att utveckla, testa, förhandsgranska och spara en segmentdefinition med Adobe Experience Platform Segmentation Service API.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---


# Skapa ett segment

Det här dokumentet innehåller en självstudiekurs för att utveckla, testa, förhandsgranska och spara en segmentdefinition med [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Mer information om hur du skapar segment med användargränssnittet finns i [guiden Skapa segment](../ui/overview.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform]-tjänsterna som används för att skapa målgruppssegment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Platform] organiserar kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:erna för [!DNL Platform].

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Utveckla en segmentdefinition

Det första steget i segmenteringen är att definiera ett segment, som representeras i en konstruktion som kallas segmentdefinition. En segmentdefinition är ett objekt som kapslar in en fråga skriven i [!DNL Profile Query Language] (PQL). Det här objektet kallas även för ett PQL-predikat. PQL förutsäger regler för segmentet baserat på villkor som relaterar till data från post- eller tidsserier som du skickar till [!DNL Real-time Customer Profile]. Mer information om hur du skriver PQL-frågor finns i [PQL-guiden](../pql/overview.md).

Du kan skapa en ny segmentdefinition genom att göra en POST-förfrågan till `/segment/definitions`-slutpunkten i [!DNL Segmentation]-API:t. Följande exempel visar hur du formaterar en definitionsbegäran, inklusive vilken information som krävs för att ett segment ska kunna definieras korrekt.

En detaljerad förklaring om hur du definierar ett segment finns i [utvecklarhandboken för segmentdefinitioner](../api/segment-definitions.md#create).

## Beräkna och förhandsgranska en målgrupp {#estimate-and-preview-an-audience}

När du utvecklar segmentdefinitionen kan du använda verktygen för uppskattning och förhandsgranskning i [!DNL Real-time Customer Profile] för att se information på sammanfattningsnivå för att säkerställa att du isolerar den förväntade målgruppen. Uppskattningar ger statistisk information om en segmentdefinition, t.ex. förväntad målgruppsstorlek och konfidensintervall. Förhandsvisningar innehåller sidnumrerade listor med kvalificeringsprofiler för en segmentdefinition, så att du kan jämföra resultaten med vad du förväntar dig.

Genom att uppskatta och förhandsgranska målgruppen kan ni testa och optimera PQL-predikaten tills de ger önskat resultat, där de sedan kan användas i en uppdaterad segmentdefinition.

Du måste utföra två steg för att förhandsgranska eller få en uppskattning av ditt segment:

1. [Skapa ett förhandsgranskningsjobb](#create-a-preview-job)
2. [Visa uppskattning eller ](#view-an-estimate-or-preview) förhandsgranskning med ID:t för förhandsgranskningsjobbet

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

Du kan skapa ett nytt förhandsgranskningsjobb genom att göra en POST-förfrågan till `/preview`-slutpunkten.

Detaljerade instruktioner om hur du skapar ett förhandsgranskningsjobb finns i [guiden för förhandsvisningar och uppskattningar av slutpunkter](../api/previews-and-estimates.md#create-preview).

### Visa en uppskattning eller förhandsgranskning

Uppskattnings- och förhandsgranskningsprocesserna körs asynkront eftersom olika frågor kan ta olika lång tid att slutföra. När en fråga har initierats kan du använda API-anrop för att hämta (GET) det aktuella läget för uppskattningen eller förhandsgranskningen medan den fortlöper.

Med hjälp av API:t [!DNL Segmentation Service] kan du slå upp ett förhandsgranskningsjobbs aktuella läge med dess ID. Om läget är &quot;RESULT_READY&quot; kan du visa resultatet. Om du vill söka efter ett förhandsgranskningsjobbs aktuella tillstånd läser du avsnittet [hämta ett förhandsgranskningsjobbavsnitt](../api/previews-and-estimates.md#get-preview) i guiden för förhandsgranskningar och uppskattningar av slutpunkter. Läs avsnittet [Hämta ett uppskattningsjobb](../api/previews-and-estimates.md#get-estimate) i guiden för förhandsvisningar och uppskattningar av slutpunkter om du vill söka efter ett uppskattningsjobb.


## Nästa steg

När du har utvecklat, testat och sparat segmentdefinitionen kan du skapa ett segmentjobb för att bygga en målgrupp med hjälp av API:t [!DNL Segmentation Service]. I självstudiekursen [utvärdering och åtkomst av segmentresultat](./evaluate-a-segment.md) finns detaljerade anvisningar om hur du gör detta.