---
solution: Experience Platform
title: Översikt över segmenteringstjänsten
description: Läs om Adobe Experience Platform segmenteringstjänst och vilken roll den spelar i Experience Platform ekosystem.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 1%

---

# [!DNL Segmentation Service] översikt

Adobe Experience Platform [!DNL Segmentation Service] innehåller ett användargränssnitt och RESTful API som gör att du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Experience Platform] och är tillgängliga för alla Adobe-lösningar.

Det här dokumentet innehåller en översikt över [!DNL Segmentation Service] och vilken roll det spelar i Adobe Experience Platform.

## Kom igång med [!DNL Segmentation Service]

Du bör förstå följande nyckeltermer som används i det här dokumentet:

- **Målgrupp**: En samling personer som delar liknande beteenden och/eller egenskaper. Den här mängden personer kan antingen genereras av Adobe Experience Platform med hjälp av segmentdefinitioner (en upplevelseplattformsgenererad publik) eller från externa källor (externt genererad publik).
- **Segmentdefinition**: Regeluppsättningen Adobe Experience Platform använder för att beskriva nyckelegenskaper eller beteenden för en målpublik.
- **Segment**: Åtgärden att dela upp profiler i målgrupper.

## Så här fungerar segmentering

Segmentering är processen att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från din kundbas. I en e-postkampanj som heter&quot;Har du glömt att köpa dina smygtittare?&quot; kanske du vill ha en målgrupp med alla användare som sökte efter skor de senaste 30 dagarna, men som inte slutförde ett köp.

När en målgrupp har definierats begreppsmässigt är den inbyggd i [!DNL Experience Platform]. Målgrupperna är oftast byggda av marknadsföraren eller målgruppsspecialisten, även om vissa organisationer föredrar att skapa dem av sin marknadsföringsavdelning, i samarbete med sina dataanalytiker. När data som skickas till [!DNL Experience Platform] granskas kan dataanalytikern skapa målgruppen på två sätt, antingen genom att skapa en segmentdefinition genom att välja vilka fält och värden som ska användas för att skapa regler eller villkor för målgruppen, eller genom att komponera en målgrupp med hjälp av målgruppsdispositionen.

## Skapa målgrupper

Du kan skapa målgrupper på flera sätt i Adobe Experience Platform, bland annat genom kompositioner, segmentdefinitioner, federerade data och Data Distiller.

### Målgruppskomposition

När du komponerar en målgrupp direkt på Experience Platform kan du använda Audience Composition. Mer information om hur du använder Audience Composition för att skapa en målgrupp finns i [guiden för målgruppssammansättning](./ui/audience-composition.md).

### Segmentdefinitioner

Oavsett om du skapar med API:t eller med [!DNL Segment Builder] definieras segmentdefinitionerna slutligen med [!DNL Profile Query Language] (PQL). Här beskrivs definitionen av konceptuellt segment i det språk som har byggts för att hämta profiler som uppfyller kriterierna. Mer information finns i [PQL - översikt](./pql/overview.md).

Mer information om hur du skapar och använder segment i [!DNL Segment Builder] (gränssnittsimplementeringen av [!DNL Segmentation Service]) finns i [segmentbyggguiden](./ui/segment-builder.md).

Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om att [skapa segmentdefinitioner med API:t](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Om ett schema utökas måste alla framtida överföringar uppdatera nya fält i enlighet med detta. Mer information om hur du anpassar [!DNL Experience Data Model] (XDM) finns i [Schemaredigerarens självstudiekurs](../xdm/tutorials/create-schema-ui.md).
>
>Om dessutom ett förfallovärde för Experience Event är aktiverat för datauppsättningen kan detta påverka medlemskapet för den segmentdefinition som skapas. Mer information om hur den här funktionen kan påverka segmenteringen finns i guiden [Händelseförfallodatum](../profile/event-expirations.md).

### Federerad målgruppssammansättning {#fac}

Förutom målgruppskompositioner och segmentdefinitioner kan du använda Adobe Federated Audience Composition för att skapa nya målgrupper från företagsdatauppsättningar utan att kopiera underliggande data och lagra dessa målgrupper i Adobe Experience Platform Audience Portal. Ni kan också berika befintliga målgrupper i Adobe Experience Platform genom att använda sammansatta målgruppsdata som har federerats från företagets datalager. Läs guiden om [Federated Audience Composition](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/home).

## Utvärdera målgrupper {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Utvärderingsmetoder"
>abstract="Experience Platform stöder för närvarande tre metoder för att utvärdera målgrupper: direktuppspelningssegmentering, gruppsegmentering och kantsegmentering."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Utvärdering av strömning"
>abstract="Direktuppspelningssegmentering är en kontinuerlig process för datamarkering som uppdaterar era målgrupper som svar på användaraktivitet."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/streaming-segmentation.html?lang=sv-SE" text="Utvärdera händelser i nära realtid med strömmande segmentering"

Experience Platform stöder för närvarande tre metoder för att utvärdera målgrupper: direktuppspelningssegmentering, gruppsegmentering och kantsegmentering.

### Direktuppspelningssegmentering {#streaming}

Direktuppspelningssegmentering är en kontinuerlig process för datamarkering som uppdaterar era målgrupper som svar på användaraktivitet. När en målgrupp har skapats och sparats tillämpas segmentdefinitionen på inkommande data till [!DNL Real-Time Customer Profile]. Tillägg och borttagningar till målgruppen behandlas regelbundet, vilket säkerställer att målgruppen förblir relevant.

Läs [dokumentationen om direktuppspelningssegmentering](./methods/streaming-segmentation.md) om du vill veta mer om direktuppspelningssegmentering.

### Gruppsegmentering {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batchutvärdering"
>abstract="Som ett alternativ till en pågående dataurvalsprocess flyttar gruppsegmentering alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När målgruppen har skapats sparas den och lagras så att du kan exportera den för användning."

Som ett alternativ till en pågående dataurvalsprocess flyttar gruppsegmentering alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När målgruppen har skapats sparas den och lagras så att du kan exportera den för användning.

Batchmålgrupper utvärderas automatiskt var 24:e timme. Om du vill utvärdera en batchmålgrupp på begäran kan du använda ett segmentjobb. Mer information om segmentjobb finns i [segmentjobbdokumentationen](./api/segment-jobs.md).

### Edge segmentering {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Edge-utvärdering"
>abstract="Edge segmentering är möjligheten att omedelbart utvärdera segment i Experience Platform på Edge Network, vilket möjliggör användning av samma sida och nästa sida."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/edge-segmentation.html?lang=sv-SE" text="Edge segmenteringsguide"

Edge segmentering är möjligheten att omedelbart utvärdera segment i Experience Platform [på Edge Network](../landing/edge-and-hub-comparison.md), vilket möjliggör användning av samma sida och nästa sida.

Läs [Översikt över kantsegmentering](./methods/edge-segmentation.md) om du vill veta mer om kantsegmentering.

## Få tillgång till segmenteringsresultat

Mer information om hur du får åtkomst till en exporterad publik finns i [självstudiekursen för utvärdering av segmentdefinition](./tutorials/evaluate-a-segment.md).

## Metadata för segmentdefinition

Metadata för segmentdefinitioner underlättar indexering om någon av era målgrupper ska återanvändas och/eller kombineras.

När du komponerar en segmentdefinition (antingen via API eller [!DNL Segment Builder]) måste du definiera ett namn och en sammanfogningsprincip.

### Segmentdefinitionsnamn

När du skapar en ny segmentdefinition måste du ange ett namn. Segmentdefinitionsnamnet används för att identifiera en viss segmentdefinition bland den samling som skapats av [!DNL Segmentation Service]. Segmentdefinitionsnamn ska därför vara beskrivande, koncisa och unika.

>[!NOTE]
>
>När du planerar en segmentdefinition måste du komma ihåg att det går att referera till segmentdefinitioner från och kombinera dem med andra segmentdefinitioner. När du väljer ett namn bör du tänka på att din segmentdefinition kan innehålla återanvändbara delar.

### Sammanfoga profiler

Sammanslagningsprinciper är regler som används av [!DNL Profile] för att bestämma hur data ska prioriteras och kombineras till en enhetlig vy under vissa villkor.

Om ingen sammanfogningsprincip har definierats används standardprincipen [!DNL Experience Platform]. Om du hellre vill använda en sammanfogningspolicy som är specifik för din organisation, kan du skapa en egen och markera den som din organisations standardpolicy.

Mer information om sammanfogningsprinciper finns i [guiden för sammanfogningsprinciper](../profile/api/merge-policies.md).

>[!NOTE]
>
>Uppskattningen av målgruppsstorlekar baseras på organisationens standardpolicy för profilsammanslagning.

### Andra metadata för segmentdefinition

Förutom namn- och sammanfogningsprincipen erbjuder [!DNL Segment Builder] ytterligare ett beskrivningsmetadatafält där du kan sammanfatta syftet med segmentdefinitionen.

## Avancerade segmenteringsfunktioner

Segmentdefinitioner kan konfigureras så att de kontinuerligt genererar en målgrupp genom att kombinera [datainmatning](../ingestion/streaming-ingestion/overview.md) med någon av följande avancerade segmenteringsfunktioner:

- [Sekventiell segmentering](#sequential)
- [Dynamisk segmentering](#dynamic)
- [Segmentering för flera enheter](#multi-entity)

Dessa avancerade funktioner beskrivs närmare i följande avsnitt.

### Sekventiell segmentering {#sequential}

En vanlig användarresa är sekventiell till sin natur. Med Adobe Experience Platform kan ni definiera en ordnad serie målgrupper som speglar den här resan och därmed fånga upp händelsesekvenser när de inträffar. Du kan ordna händelser i önskad ordning med hjälp av tidslinjen för visuella händelser i [!DNL Segment Builder].

Ett exempel på en kundresa som skulle kräva sekventiell segmentering är produktvyn > produkttillägg > utcheckning > Inget inköp.

### Dynamisk segmentering {#dynamic}

Dynamisk segmentering löser de skalbarhetsproblem som marknadsförare traditionellt möter när de skapar målgrupper för marknadsföringskampanjer.

Till skillnad från statisk segmentering, som kräver att ni explicit och upprepade gånger hämtar in alla tänkbara användningsfall, använder dynamisk segmentering variabler för att bygga regellogiken och dynamiskt uttrycka relationer.

För att illustrera värdet av den här avancerade segmenteringsfunktionen bör du överväga en dataarkitekt som samarbetar med en marknadsförare för att identifiera kunder som har gjort inköp utanför sitt hemland.

Statisk segmentering kräver att du definierar enskilda segment med ett unikt attribut för hemläge innan du filtrerar efter inköpshändelser som inte är lika med hemläget. En uttrycklig segmentdefinition av den här typen skulle få texten&quot;Jag söker efter personer från Utah där köpet inte är Utah&quot;. Om du vill skapa en målgrupp med den här metoden måste du definiera en segmentdefinition för varje delstat i USA, vilket ger totalt 50 segment.

Som ett resultat av de olika segmentdefinitionskombinationerna som oundvikligen uppstår när du skalförändrar, blir den manuella process som krävs för statisk segmentering mer tidskrävande, vilket minskar den totala effektiviteten.

Genom att tilldela en variabel till inköpsattributet förenklar er definition av dynamiskt segment att&quot;hitta ett köp där läget för köpet inte är lika med kundens hemläge&quot;. Om du gör det kan du sedan konsolidera 50 statiska segment till en enda dynamisk segmentdefinition.

### Segmentering för flera enheter {#multi-entity}

Med den avancerade segmenteringsfunktionen för flera enheter kan du utöka [!DNL Real-Time Customer Profile]-data med ytterligare data baserade på produkter, butiker eller andra icke-personella enheter, även kallade dimensionsenheter. Därför kan [!DNL Segmentation Service] komma åt ytterligare fält under segmentdefinitionen som om de vore inbyggda i datalagret [!DNL Profile]. Multientitetssegmentering ger flexibilitet när det gäller att identifiera målgrupper baserat på data som är relevanta för era unika affärsbehov. Mer information, inklusive användningsexempel och arbetsflöden, finns i [segmenteringsguiden för flera enheter](./tutorials/multi-entity-segmentation.md).

## [!DNL Segmentation Service] datatyper

[!DNL Segmentation Service] har stöd för en mängd primitiva och komplexa datatyper. Detaljerad information, inklusive en lista över datatyper som stöds, finns i [guiden för datatyper som stöds](./data-types.md).

## Nästa steg

[!DNL Segmentation Service] tillhandahåller ett konsoliderat arbetsflöde för att skapa målgrupper från [!DNL Real-Time Customer Profile]-data.

Mer information om hur du använder gränssnittet för segmenteringstjänsten finns i [Översikt över användargränssnittet för segmenteringstjänsten](./ui/overview.md).

Läs [handboken om målgruppssammansättning](./ui/audience-composition.md) om du vill lära dig hur du skapar målgrupper i användargränssnittet. Mer information om hur du definierar segmentdefinitioner i användargränssnittet finns i [guiden Skapa segment](./ui/overview.md). Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om att [skapa segmentdefinitioner med API:t](./tutorials/create-a-segment.md).
