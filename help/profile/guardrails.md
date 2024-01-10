---
title: Standardgurkor för kundprofildata och segmentering i realtid
solution: Experience Platform
product: experience platform
type: Documentation
description: Läs om prestanda och systemstyrd säkerhet för profildata och segmentering för att säkerställa en optimal användning av Real-Time CDP-funktionalitet.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 17aa9029dc83454133847352c21aa9ac68f23be8
workflow-type: tm+mt
source-wordcount: '2428'
ht-degree: 1%

---

# Standardstödlinjer för [!DNL Real-Time Customer Profile] data och segmentering

Med Adobe Experience Platform kan ni leverera personaliserade flerkanalsupplevelser baserat på beteendeinsikter och kundattribut i form av kundprofiler i realtid. För att stödja den nya metoden för profiler använder Experience Platform en högdenormaliserad hybriddatamodell som skiljer sig från den traditionella relationsdatamodellen.

Det här dokumentet innehåller standardbegränsningar för användning och frekvens som hjälper dig att modellera profildata för optimala systemprestanda. När du granskar följande skyddsutkast förutsätts det att du har modellerat data korrekt. Om du har frågor om hur du modellerar data kan du kontakta kundtjänstrepresentanten.

>[!NOTE]
>
>De flesta kunder överskrider inte dessa standardgränser. Om du vill veta mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

## Komma igång

Följande Experience Platform-tjänster är involverade i modellering av kundprofildata i realtid:

* [[!DNL Real-Time Customer Profile]](home.md): Skapa enhetliga konsumentprofiler med data från flera källor.
* [Identiteter](../identity-service/home.md): Bridge-identiteter från olika datakällor när de hämtas till Platform.
* [Scheman](../xdm/home.md): XDM-scheman (Experience Data Model) är det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [Målgrupper](../segmentation/home.md): Segmenteringsmotorn i Platform används för att skapa målgrupper utifrån era kundprofiler utifrån kundbeteenden och attribut.

## Begränsningstyper

Det finns två typer av standardgränser i det här dokumentet:

| Typ av skyddsräcke | Beskrivning |
|----------|---------|
| **Prestandaskydd (mjuk gräns)** | Prestandaskydd är användarbegränsningar som relaterar till omfattningen av dina användningsfall. När du överskrider prestandaskyddet kan du uppleva prestandaförsämringar och fördröjning. Adobe ansvarar inte för sådana prestandaförsämringar. Kunder som genomgående överskrider ett prestandaresäkerhetsskydd kan välja att licensiera ytterligare kapacitet för att undvika prestandaförsämringar. |
| **Systemstyrda skyddsräcken (hård begränsning)** | Systemstyrda skyddsräcken används av Real-Time CDP gränssnitt eller API. Det här är begränsningar som du inte kan överskrida eftersom gränssnittet och API kommer att blockera dig från att göra det eller returnera ett fel. |

{style="table-layout:auto"}

>[!NOTE]
>
>De gränser som beskrivs i det här dokumentet förbättras ständigt. Kontrollera regelbundet om det finns uppdateringar. Om du är intresserad av att lära dig mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

## Begränsningar för datamodell

Följande skyddsprofiler ger rekommenderade gränser vid modellering av kundprofildata i realtid. Mer information om primära enheter och dimensionsenheter finns i avsnittet om [enhetstyper](#entity-types) i tillägget.

![Ett diagram som visar olika skyddsutkast för profildata i Adobe Experience Platform.](./images/guardrails/profile-guardrails.png)

### Garantier för primära enheter

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Data för klassen XDM Individuella profiler | 20 | Prestandaskydd | Högst 20 datauppsättningar rekommenderas som utnyttjar klassen XDM Individual Profile. |
| XDM ExperienceEvent, klassdatamängder | 20 | Prestandaskydd | Högst 20 datauppsättningar rekommenderas som utnyttjar klassen XDM ExperienceEvent. |
| Adobe Analytics rapportuppsättningar har aktiverats för profil | 1 | Prestandaskydd | Högst en (1) datauppsättning för analysrapportsviten ska aktiveras för profilen. Om du försöker aktivera flera datauppsättningar i Analytics-rapportsviten för profilen kan det få oönskade konsekvenser för datakvaliteten. Mer information finns i avsnittet om [Adobe Analytics dataset](#aa-datasets) i tillägget. |
| Relationer för flera enheter | 5 | Prestandaskydd | Högst fem multientitetsrelationer som definierats mellan primära entiteter och dimensionsenheter rekommenderas. Ytterligare relationsmappningar ska inte göras förrän en befintlig relation tas bort eller inaktiveras. |
| JSON-djup för ID-fält som används i relationer med flera enheter | 4 | Prestandaskydd | Rekommenderat maximalt JSON-djup för ett ID-fält som används i relationer med flera enheter är 4. Detta innebär att i ett mycket kapslat schema ska fält som är kapslade mer än fyra nivåer djupa inte användas som ID-fält i en relation. |
| Matriskardinalitet i ett profilfragment | &lt;=500 | Prestandaskydd | Den optimala arraykardinaliteten i ett profilfragment (tidsoberoende data) är &lt;=500. |
| Array-kardinalitet i ExperienceEvent | &lt;=10 | Prestandaskydd | Den optimala arraykardinaliteten i en ExperienceEvent (tidsseriedata) är &lt;=10. |
| Identitetsantal för individuell profil identitetsdiagram | 50 | Systemstyrt skyddsräcke | **Det högsta antalet identiteter i ett identitetsdiagram för en enskild profil är 50.** Alla profiler med fler än 50 identiteter exkluderas från segmentering, export och uppslag. |

{style="table-layout:auto"}

### Skyddsutkast för Dimension

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Inga tidsseriedata är tillåtna för icke-[!DNL XDM Individual Profile] enheter | 0 | Systemstyrt skyddsräcke | **Tidsseriedata är inte tillåtna för icke-[!DNL XDM Individual Profile] enheter i profiltjänsten.** Om en tidsseriedatauppsättning är associerad med en icke-[!DNL XDM Individual Profile] ID, datauppsättningen ska inte aktiveras för [!DNL Profile]. |
| Inga kapslade relationer | 0 | Prestandaskydd | Du bör inte skapa en relation mellan två[!DNL XDM Individual Profile] scheman. Möjligheten att skapa relationer rekommenderas inte för scheman som inte ingår i [!DNL Profile] union-schema. |
| JSON-djup för primärt ID-fält | 4 | Prestandaskydd | Rekommenderat maximalt JSON-djup för det primära ID-fältet är 4. Det innebär att du inte ska välja ett fält som primärt ID i ett kapslat schema om det är mer än fyra nivåer djupt. Ett fält på den fjärde kapslade nivån kan användas som primärt ID. |

{style="table-layout:auto"}

## Begränsningar för datastorlek

Följande skyddsutkast hänvisar till datastorlek och innehåller rekommenderade gränser för data som kan importeras, lagras och frågas efter behov. Mer information om primära enheter och dimensionsenheter finns i avsnittet om [enhetstyper](#entity-types) i tillägget.

>[!NOTE]
>
>Datastorleken mäts som okomprimerade data i JSON vid tidpunkten för intag.

### Garantier för primära enheter

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximal ExperienceEvent-storlek | 10 kB | Systemstyrt skyddsräcke | **Den största tillåtna storleken för en händelse är 10 kB.** Intag fortsätter, men alla händelser som är större än 10 kB kommer att släppas. |
| Största profilpoststorlek | 100 kB | Systemstyrt skyddsräcke | **Den största tillåtna storleken för en profilpost är 100 kB.** Inmatningen fortsätter, men profilposter som är större än 100 kB tas bort. |
| Största profilfragmentstorlek | 50 MB | Systemstyrt skyddsräcke | **Den största tillåtna storleken för ett profilfragment är 50 MB.** Segmentering, export och uppslag kan misslyckas för alla [profilfragment](#profile-fragments) som är större än 50 MB. |
| Maximal storlek för fillagring | 50 MB | Prestandaskydd | **Den maximala storleken för en lagrad profil är 50 MB.** Lägger till nytt [profilfragment](#profile-fragments) till en profil som är större än 50 MB kommer att påverka systemets prestanda. En profil kan till exempel innehålla ett enskilt fragment som är 50 MB eller innehålla flera fragment över flera datauppsättningar med en sammanlagd storlek på 50 MB. Om du försöker lagra en profil med ett enskilt fragment som är större än 50 MB, eller med flera fragment som är större än 50 MB i kombination, påverkas systemets prestanda. |
| Antal profiler eller ExperienceEvent-batchar som har importerats per dag | 90 | Prestandaskydd | **Det högsta antalet profiler eller ExperienceEvent-batchar som har importerats per dag är 90.** Det innebär att den sammanlagda summan av de profiler och ExperienceEvent-batchar som hämtas varje dag inte får överstiga 90. Om ytterligare batchar registreras påverkas systemets prestanda. |
| Antal ExperienceEvents per profilpost | 5000 | Prestandaskydd | **Det högsta antalet ExperienceEvents per profilpost är 5 000.** Profiler med fler än 5 000 ExperienceEvents kommer att **not** beaktas för segmentering. |

{style="table-layout:auto"}

### Skyddsutkast för Dimension

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Total storlek för alla dimensionella enheter | 5 GB | Prestandaskydd | Den rekommenderade totala storleken för alla dimensionella enheter är 5 GB. Inmatning av enheter med stora dimensioner kan påverka systemets prestanda. Vi rekommenderar till exempel inte att du försöker läsa in en produktkatalog på 10 GB som en dimensionsenhet. |
| Datamängder per dimensionellt entitetsschema | 5 | Prestandaskydd | Högst 5 datauppsättningar som är associerade med varje dimensionellt enhetsschema rekommenderas. Om du till exempel skapar ett schema för&quot;produkter&quot; och lägger till fem bidragande datauppsättningar, bör du inte skapa en sjätte datauppsättning som är kopplad till produktschemat. |
| Inkapslade batchar för Dimension per dag | 4 per enhet | Prestandaskydd | Rekommenderat maximalt antal inkapslade dimensionsentitetsbatchar per dag är 4 per entitet. Du kan till exempel importera uppdateringar till en produktkatalog upp till 4 gånger per dag. Om ytterligare dimensionsenhetsbatchar för samma enhet anges kan det påverka systemets prestanda. |

{style="table-layout:auto"}

## Skyddsritningar för segmentering {#segmentation-guardrails}

De skyddsutkast som beskrivs i detta avsnitt avser antalet och typen av målgrupper som en organisation kan skapa inom Experience Platform samt kartläggning och aktivering av målgrupper till destinationer.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Målgrupper per sandlåda | 4000 | Prestandaskydd | En organisation kan ha fler än 4000 målgrupper totalt, förutsatt att det finns färre än 4000 målgrupper i varje enskild sandlåda. Detta inkluderar grupper, strömning och gränspubliken. Försök att skapa fler målgrupper kan påverka systemets prestanda. Läs mer om [skapa målgrupper](/help/segmentation/ui/segment-builder.md) genom segmentbyggaren. |
| Utforma målgrupper per sandlåda | 150 | Prestandaskydd | En organisation kan ha fler än 150 målgrupper totalt, förutsatt att det finns färre än 150 målgrupper i varje enskild sandlåda. Om du försöker skapa fler målgrupper kan det påverka systemets prestanda. Läs mer om [kantmålgrupper](/help/segmentation/ui/edge-segmentation.md). |
| Kantgenomströmning över alla sandlådor | 1 500 RPS | Prestandaskydd | Edge-segmentering stöder upp till 1 500 inkommande händelser per sekund i Adobe Experience Platform Edge Network. Kantsegmentering kan ta upp till 350 millisekunder att bearbeta en inkommande händelse när den kommer in i Adobe Experience Platform Edge Network. Läs mer om [kantmålgrupper](/help/segmentation/ui/edge-segmentation.md). |
| Direktuppspelande målgrupper per sandlåda | 500 | Prestandaskydd | En organisation kan ha fler än 500 direktuppspelade målgrupper totalt, så länge det finns färre än 500 direktuppspelade målgrupper i varje enskild sandlåda. Detta inkluderar både strömnings- och edge-målgrupper. Försök att skapa fler direktuppspelade målgrupper kan påverka systemets prestanda. Läs mer om [direktuppspelande målgrupper](/help/segmentation/ui/streaming-segmentation.md). |
| Direktuppspelningsgenomströmning över alla sandlådor | 1 500 RPS | Prestandaskydd | Direktuppspelningssegmentering stöder upp till 1 500 inkommande händelser per sekund. Det kan ta upp till 5 minuter att kvalificera en profil för segmentmedlemskap. Läs mer om [direktuppspelande målgrupper](/help/segmentation/ui/streaming-segmentation.md). |
| Gruppera målgrupper per sandlåda | 4000 | Prestandaskydd | En organisation kan ha fler än 4000 gruppmålgrupper totalt, förutsatt att det finns färre än 4000 gruppmålgrupper i varje enskild sandlåda. Om du försöker skapa fler gruppmålgrupper kan det påverka systemets prestanda. |
| Målgrupper per sandlåda | 50 | Systemstyrt skyddsräcke | Du kan skapa högst 50 kontomålgrupper i en sandlåda. När ni har nått 50 målgrupper i en sandlåda **[!UICONTROL Create audience]** kontrollen är inaktiverad när du försöker skapa en ny kontopublik. Läs mer om [kontomålgrupper](/help/segmentation/ui/account-audiences.md). |
| Publicerade kompositioner per sandlåda | 10 | Prestandaskydd | Du kan ha högst 10 publicerade kompositioner i en sandlåda. Läs mer om [publiksammansättning i gränssnittsguiden](/help/segmentation/ui/audience-composition.md). |
| Maximal målgruppsstorlek | 30 procent | Prestandaskydd | Rekommenderat maximalt medlemskap för en målgrupp är 30 procent av det totala antalet profiler i systemet. Det är möjligt att skapa målgrupper med över 30 % av profilerna som medlemmar eller flera stora målgrupper, men det påverkar systemets prestanda. |

{style="table-layout:auto"}

## Förväntad tillgänglighet

I följande avsnitt beskrivs **förväntat** tillgänglighet för målgrupper och sammanslagningspolicyer för tjänster i senare led, t.ex. Real-Time CDP destinationer:

| Sandlådetyp | Tid |
| ------------ | ---- |
| Befintliga sandlådor | 1 timme |
| Nya sandlådor | 2 timmar |
| Återställ sandlådor nyligen | 2 timmar |

{style="table-layout:auto"}

## Bilaga

I det här avsnittet finns mer information om begränsningarna i det här dokumentet.

### Enhetstyper

The [!DNL Profile] lagringsdatamodellen består av två huvudenhetstyper: [primära enheter](#primary-entity) och [dimensionsenheter](#dimension-entity).

#### Primär entitet

En primär enhet, eller profilenhet, sammanfogar data till en&quot;enda källa till sanning&quot; för en individ. Dessa enhetliga data representeras med hjälp av en s.k. fackvy. En unionsvy samlar fälten för alla scheman som implementerar samma klass i ett enda unionsschema. Unionens schema för [!DNL Real-Time Customer Profile] är en denormaliserad hybriddatamodell som fungerar som behållare för alla profilattribut och beteendehändelser.

Tidsoberoende attribut, som också kallas&quot;postdata&quot;, modelleras med [!DNL XDM Individual Profile], medan tidsseriedata, som också kallas&quot;händelsedata&quot;, modelleras med [!DNL XDM ExperienceEvent]. När data från register och tidsserier hämtas i Adobe Experience Platform utlöses de [!DNL Real-Time Customer Profile] för att börja inhämta data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

![En infografik som visar skillnaderna mellan postdata och tidsseriedata.](images/guardrails/profile-entity.png)

#### Dimension

Profildatalagret som bevarar profildata är inte ett relationslager, men profilen tillåter integrering med små dimensionsenheter för att skapa målgrupper på ett förenklat och intuitivt sätt. Integrationen kallas [segmentering av flera enheter](../segmentation/multi-entity-segmentation.md).

Din organisation kan också definiera XDM-klasser för att beskriva andra saker än enskilda, t.ex. butiker, produkter eller egenskaper. Dessa[!DNL XDM Individual Profile] scheman kallas&quot;dimensionsenheter&quot; (kallas även&quot;uppslagsenheter&quot;) och innehåller inte tidsseriedata. Scheman som representerar dimensionsenheter är länkade till profilentiteter genom användning av [schemarelationer](../xdm/tutorials/relationship-ui.md).

Dimensioner tillhandahåller sökdata som underlättar och förenklar definitioner av flerenhetssegment och måste vara tillräckligt små för att segmenteringsmotorn ska kunna läsa in hela datauppsättningen i minnet för optimal bearbetning (snabbpunktssökning).

![En infografik som visar att en profilentitet består av dimensionsenheter.](images/guardrails/profile-and-dimension-entities.png)

### Profilfragment

I det här dokumentet finns det flera skyddsutkast som refererar till&quot;profilfragment&quot;. I Experience Platform sammanfogas flera profilfragment till kundprofilen i realtid. Varje fragment representerar en unik primär identitet och motsvarande post eller fullständiga händelsedata för det ID:t inom en given datamängd. Mer information om profilfragment finns i [Profilöversikt](home.md#profile-fragments-vs-merged-profiles).

### Sammanfoga profiler {#merge-policies}

När du sammanfogar data från flera olika källor är sammanslagningsprinciper de regler som används av plattformen för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de för att skapa en enda profil för kunden. När data från flera källor står i konflikt avgör sammanfogningsprincipen vilken information som ska inkluderas i profilen för den enskilda personen. Max fem (5) sammanslagningsprinciper tillåts per organisation. Läs mer om kopplingsregler i [sammanfogningsprinciper - översikt](merge-policies/overview.md).

### Adobe Analytics rapportuppsättningar av datauppsättningar i plattformen {#aa-datasets}

Flera rapportsviter kan aktiveras för profilen så länge som alla datakonflikter är lösta. Du kan använda funktionen Data Prep för att lösa datakonflikter mellan eVars, Lists och Props. Läs mer om hur du använder funktionen Prep i [Användargränssnittshandbok för Adobe Analytics Connector](../sources/tutorials/ui/create/adobe-applications/analytics.md).

## Nästa steg

Följande dokumentation innehåller mer information om andra Experience Platform-servicesäkrar, om total latenstid och licensinformation från Real-Time CDP produktbeskrivningsdokument:

* [Real-Time CDP skyddsräcken](/help/rtcdp/guardrails/overview.md)
* [Latensdiagram från början till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) för olika Experience Platform-tjänster.
* [Real-time Customer Data Platform (B2C Edition - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
