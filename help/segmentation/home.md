---
keywords: Experience Platform;hemmabruk;populära ämnen;segmentering;segmentering;segmenttjänst;segment;segment;segment;segment;segment
solution: Experience Platform
title: Översikt över segmenteringstjänsten
topic: overview
description: Läs om Adobe Experience Platform segmenteringstjänst och vilken roll den spelar i plattformens ekosystem.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---


# [!DNL Segmentation Service] översikt

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile]-data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform] och är tillgängliga för alla Adobe-lösningar.

Det här dokumentet innehåller en översikt över [!DNL Segmentation Service] och vilken roll det spelar i Adobe Experience Platform.

## Komma igång med [!DNL Segmentation Service]

Det är viktigt att förstå följande nyckeltermer som används i hela det här dokumentet:

- **Segmentering**: Att dela upp en stor grupp individer (t.ex. kunder, prospects, användare eller organisationer) i mindre grupper som delar liknande egenskaper och kommer att reagera på liknande sätt som marknadsföringsstrategier.
- **Segmentdefinition**: Den regeluppsättning som används för att beskriva nyckelegenskaper eller beteenden för en målgrupp. När reglerna i en segmentdefinition är färdiga används de för att avgöra vilka målgruppsmedlemmar som är kvalificerade för ett segment.
- **Målgrupp**: Den resulterande uppsättningen profiler som uppfyller villkoren för en segmentdefinition.

## Så här fungerar segmentering

Segmentering är processen att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från din kundbas. I en e-postkampanj som heter&quot;Har du glömt att köpa dina smygtittare?&quot; kanske du vill ha en målgrupp med alla användare som sökte efter skor de senaste 30 dagarna, men som inte slutförde ett köp.

När ett segment har definierats begreppsmässigt är det inbyggt i [!DNL Experience Platform]. Vanligtvis är segment byggda av marknadsföraren eller målgruppsspecialisten, även om vissa organisationer föredrar att de skapas av deras marknadsföringsavdelning i samarbete med deras dataanalytiker. När data som skickas till [!DNL Platform] granskas disponerar dataanalytikern segmentdefinitionen genom att välja vilka fält och värden som ska användas för att skapa reglerna eller villkoren för segmentet. Detta görs med antingen användargränssnittet eller API:t.

## Skapa segment

Oavsett om du skapar med API:t eller med [!DNL Segment Builder] definieras segment med [!DNL Profile Query Language] (PQL). Här beskrivs definitionen av konceptuellt segment i det språk som har byggts för att hämta profiler som uppfyller kriterierna. Mer information finns i översikten [PQL](./pql/overview.md).

Mer information om hur du skapar och använder segment i [!DNL Segment Builder] (gränssnittsimplementeringen av [!DNL Segmentation Service]) finns i [guiden Skapa segment](./ui/overview.md).

Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om att [skapa målgruppssegment med API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Om ett schema utökas måste alla framtida överföringar uppdatera nya fält i enlighet med detta. Mer information om hur du anpassar [!DNL Experience Data Model] (XDM) finns i självstudiekursen [Schemaredigeraren](../xdm/tutorials/create-schema-ui.md).

## Utvärdera segment

### Direktuppspelningssegmentering

Direktuppspelningssegmentering är en kontinuerlig process för val av data som uppdaterar era segment som svar på användaraktivitet. När ett segment har skapats och sparats tillämpas segmentdefinitionen på inkommande data till [!DNL Real-time Customer Profile]. Tillägg och borttagningar av segment behandlas regelbundet, vilket säkerställer att målgruppen förblir relevant.

Läs [dokumentationen för direktuppspelningssegmentering](./api/streaming-segmentation.md) om du vill veta mer om direktuppspelningssegmentering.

### Gruppsegmentering

Som ett alternativ till en pågående dataurvalsprocess flyttar gruppsegmentering alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När segmentet har skapats sparas det och lagras så att du kan exportera det för användning.

Mer information om hur du utvärderar segment finns i [självstudiekursen för segmentutvärdering](./tutorials/evaluate-a-segment.md).

## Få tillgång till segmenteringsresultat

Mer information om hur du får åtkomst till ett exporterat segment finns i [självstudiekursen för segmentutvärdering](./tutorials/evaluate-a-segment.md).

## Segmentmetadata

Metadata för segment underlättar indexering om något av segmenten ska återanvändas och/eller kombineras.

När du komponerar dina segment (antingen via API eller [!DNL Segment Builder]) måste du definiera ett segmentnamn och en sammanfogningsprincip.

### Segmentnamn

När du skapar ett nytt segment måste du ange ett segmentnamn. Segmentnamnet används för att identifiera ett visst segment i samlingen som skapats av [!DNL Segmentation Service]. Segmentnamn ska därför vara beskrivande, koncisa och unika.

>[!NOTE]
>
>När du planerar ett segment måste du komma ihåg att det går att referera till segment från och kombinera dem med andra segment. När du väljer ett namn bör du tänka på att ditt segment kan innehålla återanvändbara delar.

### Sammanfoga profiler

Sammanslagningsprinciper är regler som används av [!DNL Profile] för att bestämma hur data ska prioriteras och kombineras till en enhetlig vy under vissa villkor.
Om ingen sammanfogningsprincip har definierats används standardprincipen [!DNL Platform]. Om du hellre vill använda en sammanfogningspolicy som är specifik för din organisation, kan du skapa en egen och markera den som din organisations standardpolicy.

Mer information om sammanfogningsprinciper finns i [guiden](../profile/api/merge-policies.md) för sammanfogningsprinciper.

>[!NOTE]
>
>Uppskattningen av målgruppsstorlekar baseras på organisationens standardpolicy för profilsammanslagning.

### Andra segmentmetadata

Förutom segmentnamn och sammanfogningsprincip innehåller [!DNL Segment Builder] ett extra metadatafält för&quot;segmentbeskrivning&quot; där du kan sammanfatta syftet med segmentdefinitionen.

## Avancerade segmenteringsfunktioner

Segment kan konfigureras för att kontinuerligt generera en målgrupp genom att kombinera [dataöverföring](../ingestion/streaming-ingestion/overview.md) med någon av följande avancerade segmenteringsfunktioner:
- [Sekventiell segmentering](#sequential)
- [Dynamisk segmentering](#dynamic)
- [Segmentering för flera enheter](#multi-entity)

Dessa avancerade funktioner beskrivs närmare i följande avsnitt.

## Sekventiell segmentering {#sequential}

En vanlig användarresa är sekventiell till sin natur. Med Adobe Experience Platform kan ni definiera en ordnad serie segment för att återspegla resan och därigenom fånga upp händelsesekvenser när de inträffar. Du kan ordna händelser i önskad ordning med hjälp av tidslinjen för visuella händelser i [!DNL Segment Builder].

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

## Segmentering av flera enheter {#multi-entity}

Med den avancerade segmenteringsfunktionen för flera enheter kan du utöka [!DNL Real-time Customer Profile]-data med ytterligare data baserat på produkter, butiker eller andra icke-personella enheter, även kallade dimensionsenheter. Därför kan [!DNL Segmentation Service] få åtkomst till ytterligare fält under segmentdefinitionen som om de vore inbyggda i [!DNL Profile]-datalagret. Multientitetssegmentering ger flexibilitet när det gäller att identifiera målgrupper baserat på data som är relevanta för era unika affärsbehov. Mer information, inklusive användningsexempel och arbetsflöden, finns i [segmenteringsguiden för flera enheter](multi-entity-segmentation.md).

## [!DNL Segmentation Service] datatyper

[!DNL Segmentation Service] har stöd för flera olika primitiva och komplexa datatyper. Detaljerad information, inklusive en lista över datatyper som stöds, finns i [guiden för datatyper](./data-types.md) som stöds.

## Nästa steg

[!DNL Segmentation Service] ger ett konsoliderat arbetsflöde för att skapa segment utifrån  [!DNL Real-time Customer Profile] data. Sammanfattning:

- [!DNL Segmentation] är processen att definiera en deluppsättning av profiler från din profilbutik, vilket gör att du kan karakterisera beteenden eller attribut för en önskad marknadsföringsbar grupp. [!DNL Segmentation Service] gör processen möjlig.
- När du planerar ett segment bör du tänka på att det går att referera till ett segment från och kombinera det med andra segment.
- Ett segment kan byggas utifrån regler baserade på profildata, relaterade tidsseriedata eller både och.
- Segment kan antingen utvärderas på begäran eller kontinuerligt. När alla profildata utvärderas vid behov skickas de via segmentdefinitionerna samtidigt. Vid kontinuerlig utvärdering strömmar data genom segmentdefinitioner allt eftersom det anges [!DNL Platform].

Mer information om hur du definierar segment i användargränssnittet finns i handboken [Segment Builder](./ui/overview.md). Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om att [skapa segment med API](./tutorials/create-a-segment.md).