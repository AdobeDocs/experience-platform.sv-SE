---
solution: Experience Platform
title: Översikt över segmenteringstjänsten
description: Läs om Adobe Experience Platform segmenteringstjänst och vilken roll den spelar i plattformens ekosystem.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# [!DNL Segmentation Service] översikt

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa målgrupper genom segmentdefinitioner eller andra källor från ditt [!DNL Real-Time Customer Profile] data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform]och är lätt tillgängliga för alla Adobe-lösningar.

Dokumentet innehåller en översikt över [!DNL Segmentation Service] och den roll den spelar i Adobe Experience Platform.

## Kom igång med [!DNL Segmentation Service]

Du bör förstå följande nyckeltermer som används i det här dokumentet:

- **Målgrupp**: En samling personer som delar liknande beteenden och/eller egenskaper. Den här mängden personer kan antingen genereras av Adobe Experience Platform med hjälp av segmentdefinitioner (plattformsgenererad publik) eller från externa källor (externt genererad publik).
- **Segmentdefinition**: Den regeluppsättning som Adobe Experience Platform använder för att beskriva nyckelegenskaper eller beteenden hos en målgrupp.
- **Segment**: Att separera profiler i målgrupper.

## Så här fungerar segmentering

Segmentering är processen att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från din kundbas. I en e-postkampanj som heter&quot;Har du glömt att köpa dina smygtittare?&quot; kanske du vill ha en målgrupp med alla användare som sökte efter skor de senaste 30 dagarna, men som inte slutförde ett köp.

När en målgrupp väl har definierats begreppsmässigt är den inbyggd [!DNL Experience Platform]. Målgrupperna är oftast byggda av marknadsföraren eller målgruppsspecialisten, även om vissa organisationer föredrar att skapa dem av sin marknadsföringsavdelning, i samarbete med sina dataanalytiker. Vid granskning av data som skickas till [!DNL Platform]kan dataanalytikerna skapa målgruppen på två sätt - antingen genom att skapa en segmentdefinition genom att välja vilka fält och värden som ska användas för att skapa regler eller villkor för målgruppen, eller genom att sätta samman en målgrupp med hjälp av Audience Composition.

## Skapa målgrupper

Målgrupper kan skapas på två olika sätt i Adobe Experience Platform - antingen direkt sammansatta som målgrupper eller med plattformsbaserade segmentdefinitioner.

### Målgruppskomposition

När du skapar en målgrupp direkt på en plattform kan du använda Audience Composition. Läs mer om hur du använder Audience Composition för att skapa en målgrupp i [Guide för målgruppssammansättning](./ui/audience-composition.md) för mer information.

### Segmentdefinitioner

Om det skapas med API:t eller med [!DNL Segment Builder], definieras segmentdefinitioner i slutändan med [!DNL Profile Query Language] (PQL) Här beskrivs definitionen av konceptuellt segment i det språk som har byggts för att hämta profiler som uppfyller kriterierna. Mer information finns i [PQL - översikt](./pql/overview.md).

Så här skapar och använder du segment i [!DNL Segment Builder] (användargränssnittets genomförande av [!DNL Segmentation Service]), se [Segment Builder Guide](./ui/segment-builder.md).

Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om [skapa segmentdefinitioner med API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Om ett schema utökas måste alla framtida överföringar uppdatera nya fält i enlighet med detta. Mer information om hur du anpassar [!DNL Experience Data Model] (XDM), gå till [Schemaredigeraren, genomgång](../xdm/tutorials/create-schema-ui.md).
>
>Om dessutom ett förfallovärde för Experience Event är aktiverat för datauppsättningen kan detta påverka medlemskapet för den segmentdefinition som skapas. Läs guiden på [Förfallodatum för upplevelsehändelser](../profile/event-expirations.md) om du vill ha mer information om hur den här funktionen kan påverka segmenteringen.

## Utvärdera målgrupper {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Utvärderingsmetoder"
>abstract="Plattformen har för närvarande stöd för tre metoder för att utvärdera målgrupper: direktuppspelningssegmentering, gruppsegmentering och kantsegmentering."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Utvärdering av strömning"
>abstract="Direktuppspelningssegmentering är en kontinuerlig process för datamarkering som uppdaterar era målgrupper som svar på användaraktivitet."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="Utvärdera händelser i nära realtid med strömmande segmentering"

Plattformen har för närvarande stöd för tre metoder för att utvärdera målgrupper: direktuppspelningssegmentering, gruppsegmentering och kantsegmentering.

### Direktuppspelningssegmentering {#streaming}

Direktuppspelningssegmentering är en kontinuerlig process för datamarkering som uppdaterar era målgrupper som svar på användaraktivitet. När en målgrupp har skapats och sparats tillämpas segmentdefinitionen på inkommande data på [!DNL Real-Time Customer Profile]. Tillägg och borttagningar till målgruppen behandlas regelbundet, vilket säkerställer att målgruppen förblir relevant.

Läs mer om direktuppspelningssegmentering i [dokumentation om direktuppspelningssegmentering](./api/streaming-segmentation.md).

### Gruppsegmentering {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batchutvärdering"
>abstract="Som ett alternativ till en pågående dataurvalsprocess flyttar gruppsegmentering alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När målgruppen har skapats sparas den och lagras så att du kan exportera den för användning."

Som ett alternativ till en pågående dataurvalsprocess flyttar gruppsegmentering alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När målgruppen har skapats sparas den och lagras så att du kan exportera den för användning.

Batchmålgrupper utvärderas automatiskt var 24:e timme. Om du vill utvärdera en batchmålgrupp på begäran kan du använda ett segmentjobb. Läs mer om segmentjobb i [dokumentation för segmentjobb](./api/segment-jobs.md).

### Edge segmentering {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Edge-utvärdering"
>abstract="Edge segmentering är möjligheten att omedelbart utvärdera segment i Platform på Edge Network, vilket möjliggör användning av samma sida och nästa sida."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Användargränssnittsguide för Edge-segmentering"

Edge segmentering är möjligheten att omedelbart utvärdera segment i plattformen [på Edge Network](../web-sdk/home.md), vilket möjliggör användning av personalisering på samma sida och nästa sida.

Läs antingen [API-dokumentation](./api/edge-segmentation.md) eller [Användargränssnittsdokumentation](./ui/edge-segmentation.md).

## Få tillgång till segmenteringsresultat

Om du vill veta hur du får åtkomst till en exporterad publik kan du läsa [självstudiekurs om utvärdering av segmentdefinition](./tutorials/evaluate-a-segment.md).

## Metadata för segmentdefinition

Metadata för segmentdefinitioner underlättar indexering om någon av era målgrupper ska återanvändas och/eller kombineras.

Disponera en segmentdefinition (antingen via API:t eller [!DNL Segment Builder]) kräver att du definierar ett namn och en sammanfogningsprincip.

### Segmentdefinitionsnamn

När du skapar en ny segmentdefinition måste du ange ett namn. Segmentdefinitionsnamnet används för att identifiera en viss segmentdefinition bland de samlingar som skapats av [!DNL Segmentation Service]. Segmentdefinitionsnamn ska därför vara beskrivande, koncisa och unika.

>[!NOTE]
>
>När du planerar en segmentdefinition måste du komma ihåg att det går att referera till segmentdefinitioner från och kombinera dem med andra segmentdefinitioner. När du väljer ett namn bör du tänka på att din segmentdefinition kan innehålla återanvändbara delar.

### Sammanfoga profiler

Sammanfogningsprinciper är regler som används av [!DNL Profile] fastställa hur data ska prioriteras och kombineras i en enhetlig vy under vissa förhållanden.

Om ingen sammanfogningsprincip är definierad är standardinställningen [!DNL Platform] sammanfogningsprincip används. Om du hellre vill använda en sammanfogningspolicy som är specifik för din organisation, kan du skapa en egen och markera den som din organisations standardpolicy.

Mer information om sammanfogningsprinciper finns i [guide för sammanslagningsprinciper](../profile/api/merge-policies.md).

>[!NOTE]
>
>Uppskattningen av målgruppsstorlekar baseras på organisationens standardpolicy för profilsammanslagning.

### Andra metadata för segmentdefinition

Förutom namn och sammanfogningsprincip [!DNL Segment Builder] I finns ytterligare ett beskrivningsmetadatafält där du kan sammanfatta segmentdefinitionens syfte.

## Avancerade segmenteringsfunktioner

Segmentdefinitioner kan konfigureras för att kontinuerligt generera en målgrupp genom att kombinera [inmatning av strömmande data](../ingestion/streaming-ingestion/overview.md) med någon av följande avancerade segmenteringsfunktioner:
- [Sekventiell segmentering](#sequential)
- [Dynamisk segmentering](#dynamic)
- [Segmentering för flera enheter](#multi-entity)

Dessa avancerade funktioner beskrivs närmare i följande avsnitt.

### Sekventiell segmentering {#sequential}

En vanlig användarresa är sekventiell till sin natur. Med Adobe Experience Platform kan ni definiera en ordnad serie målgrupper som speglar den här resan och därmed fånga upp händelsesekvenser när de inträffar. Du kan ordna händelser i önskad ordning med hjälp av tidslinjen för visuella händelser i dialogrutan [!DNL Segment Builder].

Ett exempel på en kundresa som skulle kräva sekventiell segmentering är produktvyn > produkttillägg > utcheckning > Inget inköp.

### Dynamisk segmentering {#dynamic}

Dynamisk segmentering löser de skalbarhetsproblem som marknadsförare traditionellt möter när de skapar målgrupper för marknadsföringskampanjer.

Till skillnad från statisk segmentering, som kräver att ni explicit och upprepade gånger hämtar in alla tänkbara användningsfall, använder dynamisk segmentering variabler för att bygga regellogiken och dynamiskt uttrycka relationer.

För att illustrera värdet av den här avancerade segmenteringsfunktionen bör du överväga en dataarkitekt som samarbetar med en marknadsförare för att identifiera kunder som har gjort inköp utanför sitt hemland.

Statisk segmentering kräver att du definierar enskilda segment med ett unikt attribut för hemläge innan du filtrerar efter inköpshändelser som inte är lika med hemläget. En uttrycklig segmentdefinition av den här typen skulle få texten&quot;Jag söker efter personer från Utah där köpet inte är Utah&quot;. Om du vill skapa en målgrupp med den här metoden måste du definiera en segmentdefinition för varje delstat i USA, vilket ger totalt 50 segment.

Som ett resultat av de olika segmentdefinitionskombinationerna som oundvikligen uppstår när du skalförändrar, blir den manuella process som krävs för statisk segmentering mer tidskrävande, vilket minskar den totala effektiviteten.

Genom att tilldela en variabel till inköpsattributet förenklar er definition av dynamiskt segment att&quot;hitta ett köp där läget för köpet inte är lika med kundens hemläge&quot;. Om du gör det kan du sedan konsolidera 50 statiska segment till en enda dynamisk segmentdefinition.

### Segmentering för flera enheter {#multi-entity}

Med den avancerade segmenteringsfunktionen för flera enheter kan du utöka [!DNL Real-Time Customer Profile] data med ytterligare data baserade på produkter, butiker eller andra icke-personella enheter, även kallade&quot;dimensionsenheter&quot;. Detta resulterar i [!DNL Segmentation Service] kan få åtkomst till ytterligare fält under segmentdefinitionen som om de var inbyggda i [!DNL Profile] datalager. Multientitetssegmentering ger flexibilitet när det gäller att identifiera målgrupper baserat på data som är relevanta för era unika affärsbehov. Mer information, inklusive användningsexempel och arbetsflöden, finns i [segmenteringshandbok för flera enheter](multi-entity-segmentation.md).

## [!DNL Segmentation Service] datatyper

[!DNL Segmentation Service] har stöd för flera olika primitiva och komplexa datatyper. Detaljerad information, inklusive en lista över vilka datatyper som stöds, finns i [guide för datatyper som stöds](./data-types.md).

## Nästa steg

[!DNL Segmentation Service] ger ett konsoliderat arbetsflöde för att bygga målgrupper utifrån [!DNL Real-Time Customer Profile] data.

Mer information om hur du använder gränssnittet för segmenteringstjänsten finns i [Översikt över användargränssnittet för segmenteringstjänsten](./ui/overview.md).

Läs mer om hur du skapar målgrupper i användargränssnittet i [Guide för målgruppssammansättning](./ui/audience-composition.md). Mer information om hur du definierar segmentdefinitioner i användargränssnittet finns i [Segment Builder Guide](./ui/overview.md). Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om [skapa segmentdefinitioner med API](./tutorials/create-a-segment.md).
