---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segment;Segment;Segments;segments
solution: Experience Platform
title: Adobe Experience Platform segmenteringstjänst
topic: overview
description: Det här dokumentet innehåller en översikt över segmenteringstjänsten och vilken roll den spelar i Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] overview

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile] data. Dessa segment är centralt konfigurerade och underhållna [!DNL Platform]och är lätt tillgängliga för alla Adobe-lösningar.

Det här dokumentet innehåller en översikt över [!DNL Segmentation Service] och vilken roll det spelar i Adobe Experience Platform.

## Getting started with [!DNL Segmentation Service]

Det är viktigt att förstå följande nyckeltermer som används i hela det här dokumentet:

- **Segmentering**: Att dela upp en stor grupp individer (t.ex. kunder, prospects, användare eller organisationer) i mindre grupper som delar liknande egenskaper och kommer att reagera på liknande sätt som marknadsföringsstrategier.
- **Segmentdefinition**: Den regeluppsättning som används för att beskriva nyckelegenskaper eller beteenden för en målgrupp. När reglerna i en segmentdefinition är färdiga används de för att avgöra vilka målgruppsmedlemmar som är kvalificerade för ett segment.
- **Målgrupp**: Den resulterande uppsättningen profiler som uppfyller villkoren för en segmentdefinition.

## Så här fungerar segmentering

Segmentering är processen att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från din kundbas. I en e-postkampanj som heter&quot;Har du glömt att köpa dina smygtittare?&quot; kanske du vill ha en målgrupp med alla användare som sökte efter skor de senaste 30 dagarna, men som inte slutförde ett köp.

När ett segment har definierats konceptuellt är det inbyggt [!DNL Experience Platform]. Vanligtvis är segment byggda av marknadsföraren eller målgruppsspecialisten, även om vissa organisationer föredrar att de skapas av deras marknadsföringsavdelning i samarbete med deras dataanalytiker. När dataanalytikern granskar de data som skickas till [!DNL Platform]skapar den segmentdefinitionen genom att välja vilka fält och värden som ska användas för att skapa segmentets regler eller villkor. Detta görs med antingen användargränssnittet eller API:t.

## Skapa segment

Oavsett om segmenten skapas med API:t eller med [!DNL Segment Builder]hjälp av, definieras segmenten slutligen med [!DNL Profile Query Language] (PQL). Här beskrivs definitionen av konceptuellt segment i det språk som har byggts för att hämta profiler som uppfyller kriterierna. Mer information finns i [PQL-översikten](./pql/overview.md).

Mer information om hur du skapar och använder segment i [!DNL Segment Builder] (gränssnittsimplementeringen av [!DNL Segmentation Service]) finns i guiden [för](./ui/overview.md)segmentbyggaren.

Mer information om hur du skapar segmentdefinitioner med API finns i självstudiekursen om hur du [skapar målgruppssegment med API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Om ett schema utökas måste alla framtida överföringar uppdatera nya fält i enlighet med detta. Mer information om hur du anpassar [!DNL Experience Data Model] (XDM) finns i [Schemaredigerarens självstudiekurs](../xdm/tutorials/create-schema-ui.md).

## Utvärdera segment

### Direktuppspelningssegmentering

Direktuppspelningssegmentering är en kontinuerlig process för val av data som uppdaterar era segment som svar på användaraktivitet. När ett segment har skapats och sparats tillämpas segmentdefinitionen på inkommande data i [!DNL Real-time Customer Profile]. Tillägg och borttagningar av segment behandlas regelbundet, vilket säkerställer att målgruppen förblir relevant.

Mer information om direktuppspelningssegmentering finns i [dokumentationen](./api/streaming-segmentation.md)för direktuppspelningssegmentering.

### Gruppsegmentering

Som ett alternativ till en pågående dataurvalsprocess flyttar gruppsegmentering alla profildata samtidigt genom segmentdefinitioner för att skapa motsvarande målgrupper. När segmentet har skapats sparas det och lagras så att du kan exportera det för användning.

Mer information om hur du utvärderar segment finns i [självstudiekursen](./tutorials/evaluate-a-segment.md)för segmentutvärdering.

## Få tillgång till segmenteringsresultat

Mer information om hur du får åtkomst till ett exporterat segment finns i självstudiekursen om [segmentutvärdering](./tutorials/evaluate-a-segment.md).

## Segmentmetadata

Metadata för segment underlättar indexering om något av segmenten ska återanvändas och/eller kombineras.

När du komponerar dina segment (antingen via API eller [!DNL Segment Builder]) måste du definiera ett segmentnamn och en sammanfogningsprincip.

### Segmentnamn

När du skapar ett nytt segment måste du ange ett segmentnamn. Segmentnamnet används för att identifiera ett visst segment i den samling som skapas av [!DNL Segmentation Service]. Segmentnamn ska därför vara beskrivande, koncisa och unika.

>[!NOTE]
>
>När du planerar ett segment måste du komma ihåg att det går att referera till segment från och kombinera dem med andra segment. När du väljer ett namn bör du tänka på att ditt segment kan innehålla återanvändbara delar.

### Sammanfoga profiler

Sammanslagningsprinciper är regler som används för [!DNL Profile] att bestämma hur data ska prioriteras och kombineras till en enhetlig vy under vissa villkor.
Om ingen sammanfogningsprincip har definierats används standardprincipen för [!DNL Platform] sammanfogning. Om du hellre vill använda en sammanfogningspolicy som är specifik för din organisation, kan du skapa en egen och markera den som din organisations standardpolicy.

Mer information om sammanfogningsprinciper finns i guiden [för](../profile/api/merge-policies.md)sammanfogningsprinciper.

>[!NOTE]
>
>Uppskattningen av målgruppsstorlekar baseras på organisationens standardpolicy för profilsammanslagning.

### Andra segmentmetadata

Förutom segmentnamn och sammanfogningsprincip [!DNL Segment Builder] finns det ytterligare ett metadatafält för&quot;segmentbeskrivning&quot; där du kan sammanfatta syftet med segmentdefinitionen.

## Avancerade segmenteringsfunktioner

Segment kan konfigureras för att kontinuerligt generera en målgrupp genom att kombinera [strömmande datainmatning](../ingestion/streaming-ingestion/overview.md) med någon av följande avancerade segmenteringsfunktioner:
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

## Segmentering för flera enheter {#multi-entity}

Med den avancerade funktionen för segmentering av flera enheter kan du skapa segment med hjälp av flera XDM-klasser och på så sätt lägga till tillägg till personscheman. Det innebär att [!DNL Segmentation Service] kan få åtkomst till ytterligare fält under segmentdefinitionen som om de vore inbyggda i profildatalagret.

Multientitetssegmentering ger den flexibilitet som behövs för att identifiera målgrupper baserat på data som är relevanta för företagets behov. Denna process kan utföras snabbt och enkelt utan att man behöver ha expertis i databasfrågor. På så sätt kan ni lägga till nyckeldata i era segment utan att behöva göra kostsamma ändringar i dataströmmar eller vänta på en datasammanfogning.

Följande video är avsedd att ge stöd för din förståelse av segmentering för flera enheter och ger en översikt över både segmentsegmentering och segmentkontext (segmentnyttolast).

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

### Användningsfall: Prisdriven kampanj

För att illustrera värdet av den här avancerade segmenteringsfunktionen bör du överväga en dataarkitekt som samarbetar med en marknadsförare.

I det här exemplet förenar dataarkitekten data för en individ (som består av scheman med [!DNL XDM Individual Profile] och [!DNL XDM ExperienceEvent] som basklasser) till en annan klass med hjälp av en nyckel. När de är anslutna kan dataarkitekten eller marknadsföraren använda dessa nya fält under segmentdefinitionen som om de vore inbyggda i basklassens schema.

**Problemet**

Både dataarkitekten och marknadsföraren fungerar för samma klädåterförsäljare. Detaljhandlaren har över 1 000 butiker i Nordamerika och sänker regelbundet sina produktpriser under hela livscykeln. Marknadsföraren vill därför genomföra en specialkampanj för att ge de kunder som köpt produkterna en chans att köpa dem till det rabatterade priset.

Datasektionens resurser omfattar tillgång till webbdata från kundsurfning samt kundvagnsinformation som innehåller produkt-SKU-identifierare. De har också tillgång till en separat&quot;produkter&quot;-klass där ytterligare produktinformation (inklusive produktpris) lagras. Deras vägledning är att fokusera på kunder som har lagt till en produkt i kundvagnen de senaste 14 dagarna, men inte köpt artikeln, vars pris nu har sjunkit.

**Lösningen**

>[!NOTE]
>
>I det här exemplet antar vi att dataarkitekten redan har upprättat ett ID-namnutrymme.

Med API:t kopplar dataarkitekten nyckeln från [!DNL ExperienceEvent] schemat till klassen&quot;products&quot;. På så sätt kan dataarkitekten använda de extra fälten från klassen&quot;products&quot; som om de vore inbyggda i [!DNL ExperienceEvent] schemat. Som det sista steget i konfigurationsarbetet måste dataarkitekten överföra rätt data till [!DNL Real-time Customer Profile]. Detta görs genom att aktivera datauppsättningen&quot;products&quot; för användning med [!DNL Profile]. När konfigurationen är klar kan antingen dataarkitekten eller marknadsföraren skapa målsegmentet i [!DNL Segment Builder].

Se översikten över [](../xdm/schema/composition.md#union) schemakomposition för att lära dig hur du definierar relationer mellan XDM-klasser.

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### Användningsfall

För att illustrera värdet av den här avancerade segmenteringsfunktionen bör du överväga tre standardanvändningsfall som illustrerar de utmaningar som fanns i marknadsföringsapplikationer innan segmentnyttolastförbättringen:
- E-postpersonalisering
- Återmarknadsföring via e-post
- Återannonsering

**E-postpersonalisering**

En marknadsförare som har skapat en e-postkampanj kan ha försökt att skapa ett segment för en målgrupp genom att använda de senaste kundbutikerna de senaste tre månaderna. Helst skulle det här segmentet kräva både artikelnamnet och namnet på butiken där köpet gjordes. Före förbättringarna var utmaningen att hämta butiksidentifieraren från inköpshändelsen och tilldela den till kundens profil.

**Återmarknadsföring via e-post**

Det är ofta komplicerat att skapa och kvalificera segment för e-postkampanjer som riktar sig till &quot;kundvagnsöverlåtelse&quot;. Före förbättringarna var det svårt att veta vilka produkter som skulle inkluderas i ett personaliserat meddelande på grund av att de nödvändiga uppgifterna fanns tillgängliga. Data som produkterna övergavs för är knutna till upplevelsehändelser som tidigare var utmanande att övervaka och extrahera data från.

**Återannonsering**

En annan traditionell utmaning för marknadsförare har varit att skapa annonser för att rikta om kunder med övergivna kundvagnsartiklar. Även om segmentdefinitionerna var en utmaning fanns det ingen formell metod för att skilja mellan inköpta produkter och övergivna produkter innan förbättringarna gjordes. Nu kan du rikta in dig på specifika datauppsättningar under segmentdefinitionen.

## [!DNL Segmentation Service] datatyper

[!DNL Segmentation Service] har stöd för flera olika datatyper, inklusive:

- Sträng
- Unik resurs-ID
- Enum
- Siffra
- Lång
- Heltal
- Kort
- Byte
- Boolean
- Datum
- Datum-tid
- Array
- Objekt
- Mappa
- Händelser
- Externa målgrupper
- Segment

Mer detaljerad information om dessa datatyper som stöds finns i det [datatypsdokument](./data-types.md)som stöds.

## Nästa steg

[!DNL Segmentation Service] ger ett konsoliderat arbetsflöde för att skapa segment utifrån [!DNL Real-time Customer Profile] data. Sammanfattning:

- [!DNL Segmentation] är processen att definiera en deluppsättning av profiler från din profilbutik, vilket gör att du kan karakterisera beteenden eller attribut för en önskad marknadsföringsbar grupp. [!DNL Segmentation Service] gör processen möjlig.
- När du planerar ett segment bör du tänka på att det går att referera till ett segment från och kombinera det med andra segment.
- Ett segment kan byggas utifrån regler baserade på profildata, relaterade tidsseriedata eller både och.
- Segment kan antingen utvärderas på begäran eller kontinuerligt. När alla profildata utvärderas vid behov skickas de via segmentdefinitionerna samtidigt. Vid kontinuerlig utvärdering strömmar data genom segmentdefinitioner allt eftersom de anges [!DNL Platform].

Mer information om hur du definierar segment i användargränssnittet finns i guiden [Skapa](./ui/overview.md)segment. Information om hur du skapar segmentdefinitioner med API finns i självstudiekursen om hur du [skapar segment med API](./tutorials/create-a-segment.md).