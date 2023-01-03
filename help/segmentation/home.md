---
keywords: Experience Platform;hemmabruk;populära ämnen;segmentering;segmentering;segmenttjänst;segment;segment;segment;segment;segment
solution: Experience Platform
title: Översikt över segmenteringstjänsten
topic-legacy: overview
description: Läs om Adobe Experience Platform segmenteringstjänst och vilken roll den spelar i plattformens ekosystem.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# [!DNL Segmentation Service] översikt

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper från [!DNL Real-Time Customer Profile] data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform]och är lätt tillgängliga för alla Adobe-lösningar.

Dokumentet innehåller en översikt över [!DNL Segmentation Service] och den roll den spelar i Adobe Experience Platform.

## Komma igång med [!DNL Segmentation Service]

Det är viktigt att förstå följande nyckeltermer som används i hela det här dokumentet:

- **Segmentering**: Att dela upp en stor grupp individer (t.ex. kunder, prospects, användare eller organisationer) i mindre grupper som delar liknande egenskaper och kommer att reagera på liknande sätt som marknadsföringsstrategier.
- **Segmentdefinition**: Den regeluppsättning som används för att beskriva nyckelegenskaper eller beteenden för en målgrupp. När reglerna i en segmentdefinition är färdiga används de för att avgöra vilka målgruppsmedlemmar som är kvalificerade för ett segment.
- **Målgrupp**: Den resulterande uppsättningen profiler som uppfyller villkoren för en segmentdefinition.

## Så här fungerar segmentering

Segmentering är processen att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från din kundbas. I en e-postkampanj som heter&quot;Har du glömt att köpa dina smygtittare?&quot; kanske du vill ha en målgrupp med alla användare som sökte efter skor de senaste 30 dagarna, men som inte slutförde ett köp.

När ett segment har definierats konceptuellt är det inbyggt [!DNL Experience Platform]. Vanligtvis är segment byggda av marknadsföraren eller målgruppsspecialisten, även om vissa organisationer föredrar att de skapas av deras marknadsföringsavdelning i samarbete med deras dataanalytiker. Vid granskning av data som skickas till [!DNL Platform]skapar dataanalytikern segmentdefinitionen genom att välja vilka fält och värden som ska användas för att skapa segmentets regler eller villkor. Detta görs med antingen användargränssnittet eller API:t.

## Skapa segment

Om det skapas med API:t eller med [!DNL Segment Builder], definieras segment slutligen med [!DNL Profile Query Language] (PQL). Här beskrivs definitionen av konceptuellt segment i det språk som har byggts för att hämta profiler som uppfyller kriterierna. Mer information finns i [PQL - översikt](./pql/overview.md).

Så här skapar och använder du segment i [!DNL Segment Builder] (användargränssnittets genomförande av [!DNL Segmentation Service]), se [Segment Builder Guide](./ui/overview.md).

Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om [skapa målgruppssegment med API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Om ett schema utökas måste alla framtida överföringar uppdatera nya fält i enlighet med detta. Mer information om hur du anpassar [!DNL Experience Data Model] (XDM), gå till [Schemaredigeraren, genomgång](../xdm/tutorials/create-schema-ui.md).
>
>Om dessutom ett förfallovärde för Experience Event är aktiverat för datauppsättningen kan det påverka medlemskapet för det skapade segmentet. Läs guiden på [Förfallodatum för upplevelsehändelser](../profile/event-expirations.md) om du vill ha mer information om hur den här funktionen kan påverka segmenteringen.

## Utvärdera segment {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Utvärderingsmetoder"
>abstract="Plattformen har för närvarande stöd för tre metoder för att utvärdera segment: direktuppspelningssegmentering, gruppsegmentering och kantsegmentering."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Utvärdering av strömning"
>abstract="Direktuppspelningssegmentering är en kontinuerlig process för val av data som uppdaterar era segment som svar på användaraktivitet."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="Utvärdera händelser i nära realtid med strömmande segmentering"

Plattformen har för närvarande stöd för tre metoder för att utvärdera segment: direktuppspelningssegmentering, gruppsegmentering och kantsegmentering.

### Direktuppspelningssegmentering {#streaming}

Direktuppspelningssegmentering är en kontinuerlig process för val av data som uppdaterar era segment som svar på användaraktivitet. När ett segment har skapats och sparats tillämpas segmentdefinitionen på inkommande data på [!DNL Real-Time Customer Profile]. Tillägg och borttagningar av segment behandlas regelbundet, vilket säkerställer att målgruppen förblir relevant.

Läs mer om direktuppspelningssegmentering i [dokumentation om direktuppspelningssegmentering](./api/streaming-segmentation.md).

### Gruppsegmentering {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batchutvärdering"
>abstract="Som ett alternativ till en pågående dataurvalsprocess flyttar gruppsegmentering alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När segmentet har skapats sparas det och lagras så att du kan exportera det för användning."

Som ett alternativ till en pågående dataurvalsprocess flyttar gruppsegmentering alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När segmentet har skapats sparas det och lagras så att du kan exportera det för användning.

Batchsegment utvärderas automatiskt var 24:e timme. Om du vill utvärdera ett batchsegment vid behov kan du använda ett segmentjobb. Läs mer om segmentjobb i [dokumentation för segmentjobb](./api/segment-jobs.md).

### Kantsegmentering {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Kantutvärdering"
>abstract="Kantsegmentering är möjligheten att omedelbart utvärdera segment i plattformen på Experience Edge, vilket möjliggör användning av samma sida och nästa sida."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Användargränssnittsguide för kantsegmentering"

Kantsegmentering är möjligheten att omedelbart utvärdera segment i plattformen [på Experience Edge](../edge/home.md), vilket möjliggör användning av personalisering på samma sida och nästa sida.

Läs antingen [API-dokumentation](./api/edge-segmentation.md) eller [Användargränssnittsdokumentation](./ui/edge-segmentation.md).

## Få tillgång till segmenteringsresultat

Mer information om hur du kommer åt ett exporterat segment finns i [självstudiekurs om segmentutvärdering](./tutorials/evaluate-a-segment.md).

## Segmentmetadata

Metadata för segment underlättar indexering om något av segmenten ska återanvändas och/eller kombineras.

Skapa dina segment (antingen via API:t eller [!DNL Segment Builder]) kräver att du definierar ett segmentnamn och en sammanfogningsprincip.

### Segmentnamn

När du skapar ett nytt segment måste du ange ett segmentnamn. Segmentnamnet används för att identifiera ett visst segment i den samling som skapas av [!DNL Segmentation Service]. Segmentnamn ska därför vara beskrivande, koncisa och unika.

>[!NOTE]
>
>När du planerar ett segment måste du komma ihåg att det går att referera till segment från och kombinera dem med andra segment. När du väljer ett namn bör du tänka på att ditt segment kan innehålla återanvändbara delar.

### Sammanfoga profiler

Sammanfogningsprinciper är regler som används av [!DNL Profile] fastställa hur data ska prioriteras och kombineras i en enhetlig vy under vissa förhållanden.
Om ingen sammanfogningsprincip är definierad är standardinställningen [!DNL Platform] sammanfogningsprincip används. Om du hellre vill använda en sammanfogningspolicy som är specifik för din organisation, kan du skapa en egen och markera den som din organisations standardpolicy.

Mer information om kopplingsprofiler finns i [guide för sammanslagningsprinciper](../profile/api/merge-policies.md).

>[!NOTE]
>
>Uppskattningen av målgruppsstorlekar baseras på organisationens standardpolicy för profilsammanslagning.

### Andra segmentmetadata

Förutom segmentnamn och sammanfogningsprincip [!DNL Segment Builder] I finns ytterligare ett metadatafält för&quot;segmentbeskrivning&quot; där du kan sammanfatta syftet med segmentdefinitionen.

## Avancerade segmenteringsfunktioner

Segment kan konfigureras för att kontinuerligt generera en målgrupp genom att kombinera [inmatning av strömmande data](../ingestion/streaming-ingestion/overview.md) med någon av följande avancerade segmenteringsfunktioner:
- [Sekventiell segmentering](#sequential)
- [Dynamisk segmentering](#dynamic)
- [Segmentering för flera enheter](#multi-entity)

Dessa avancerade funktioner beskrivs närmare i följande avsnitt.

## Sekventiell segmentering {#sequential}

En vanlig användarresa är sekventiell till sin natur. Med Adobe Experience Platform kan ni definiera en ordnad serie segment för att återspegla resan och därmed fånga upp sekvenser av händelser när de inträffar. Du kan ordna händelser i önskad ordning med hjälp av tidslinjen för visuella händelser i dialogrutan [!DNL Segment Builder].

Ett exempel på en kundresa som skulle kräva sekventiell segmentering är produktvyn > produkttillägg > utcheckning > Inget inköp.

## Dynamisk segmentering {#dynamic}

Dynamisk segmentering löser de skalbarhetsproblem som marknadsförare traditionellt möter när de skapar segment för marknadsföringskampanjer.

Till skillnad från statisk segmentering, som kräver att ni explicit och upprepade gånger hämtar in alla tänkbara användningsfall, använder dynamisk segmentering variabler för att bygga regellogiken och dynamiskt uttrycka relationer.

### Användningsfall: Söker efter kunder som gör inköp utanför hemlandet

För att illustrera värdet av den här avancerade segmenteringsfunktionen bör du överväga en dataarkitekt som samarbetar med en marknadsförare för att identifiera kunder som har gjort inköp utanför sitt hemland.

**Problemet**

Statisk segmentering kräver att du definierar enskilda segment med ett unikt attribut för hemläge innan du filtrerar efter inköpshändelser som inte är lika med hemläget. Ett explicit segment av den här typen skulle ha texten&quot;Jag söker efter personer från Utah där köpläget inte är Utah&quot;. Om du vill skapa en målgrupp med den här metoden måste du definiera ett segment för varje delstat i USA, vilket ger totalt 50 segment.

Till följd av de olika segmentkombinationer som oundvikligen uppstår när du skalförändrar blir den manuella process som krävs för statisk segmentering mer tidskrävande, vilket minskar den totala effektiviteten.

**Lösningen**

Genom att tilldela en variabel till inköpsattributet förenklar ditt dynamiska segment att&quot;hitta ett köp där köpets status inte är densamma som kundens hemläge&quot;. Om du gör det kan du sedan konsolidera 50 statiska segment till ett enda dynamiskt segment.

## Segmentering för flera enheter {#multi-entity}

Med den avancerade segmenteringsfunktionen för flera enheter kan du utöka [!DNL Real-Time Customer Profile] data med ytterligare data baserade på produkter, butiker eller andra icke-personella enheter, även kallade&quot;dimensionsenheter&quot;. Som en följd av detta [!DNL Segmentation Service] kan få åtkomst till ytterligare fält under segmentdefinitionen som om de var inbyggda i [!DNL Profile] datalager. Multientitetssegmentering ger flexibilitet när det gäller att identifiera målgrupper baserat på data som är relevanta för era unika affärsbehov. Mer information, inklusive användningsexempel och arbetsflöden, finns i [segmenteringshandbok för flera enheter](multi-entity-segmentation.md).

## [!DNL Segmentation Service] datatyper

[!DNL Segmentation Service] har stöd för flera olika primitiva och komplexa datatyper. Detaljerad information, inklusive en lista över datatyper som stöds, finns i [guide för datatyper som stöds](./data-types.md).

## Nästa steg

[!DNL Segmentation Service] ger ett konsoliderat arbetsflöde för att skapa segment utifrån [!DNL Real-Time Customer Profile] data. Sammanfattning:

- [!DNL Segmentation] är processen att definiera en deluppsättning av profiler från din profilbutik, vilket gör att du kan karakterisera beteenden eller attribut för en önskad marknadsföringsbar grupp. [!DNL Segmentation Service] gör processen möjlig.
- När du planerar ett segment bör du tänka på att det går att referera till ett segment från och kombinera det med andra segment.
- Ett segment kan byggas utifrån regler baserade på profildata, relaterade tidsseriedata eller både och.
- Segment kan antingen utvärderas på begäran eller kontinuerligt. När alla profildata utvärderas vid behov skickas de via segmentdefinitionerna samtidigt. Vid kontinuerlig utvärdering strömmar data genom segmentdefinitioner allt eftersom de matas in [!DNL Platform].

Mer information om hur du definierar segment i användargränssnittet finns i [Segment Builder Guide](./ui/overview.md). Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om [skapa segment med API](./tutorials/create-a-segment.md).
