---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;skyddsförslag;riktlinjer;begränsning;enhet;primär enhet;dimensionsenhet;
title: Standardguardrutor för kundprofildata i realtid
solution: Experience Platform
product: experience platform
type: Documentation
description: I Adobe Experience Platform används en mycket denormaliserad hybriddatamodell som skiljer sig från den traditionella relationsdatamodellen. Det här dokumentet innehåller standardbegränsningar för användning och frekvens som hjälper dig att modellera profildata för optimal systemprestanda.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 1c092cd66a8a96623359a0e56de76e2a3d077c8d
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 4%

---

# Standardstödlinjer för [!DNL Real-Time Customer Profile] data

Med Adobe Experience Platform kan ni leverera personaliserade flerkanalsupplevelser baserat på beteendeinsikter och kundattribut i form av kundprofiler i realtid. För att stödja den nya metoden för profiler använder Experience Platform en högdenormaliserad hybriddatamodell som skiljer sig från den traditionella relationsdatamodellen.

Det här dokumentet innehåller standardbegränsningar för användning och frekvens som hjälper dig att modellera profildata för optimal systemprestanda. När du granskar följande skyddsutkast förutsätts det att du har modellerat data korrekt. Om du har frågor om hur du modellerar data kan du kontakta kundtjänstrepresentanten.

>[!NOTE]
>
>De flesta kunder överskrider inte dessa standardgränser. Om du vill veta mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

## Komma igång

Följande Experience Platform-tjänster är involverade i modellering av kundprofildata i realtid:

* [[!DNL Real-Time Customer Profile]](home.md): Skapa enhetliga kundprofiler med hjälp av data från flera källor.
* [Identiteter](../identity-service/home.md): Överbrygga identiteter från olika datakällor när de hämtas till Platform.
* [Scheman](../xdm/home.md): XDM-scheman (Experience Data Model) är det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [Segment](../segmentation/home.md): Segmenteringsmotorn i Platform används för att skapa segment utifrån era kundprofiler baserat på kundbeteenden och attribut.

## Begränsningstyper

Det finns två typer av standardgränser i det här dokumentet:

* **Mjuk gräns:** Det går att gå längre än en mjuk gräns, men mjuka gränser ger en rekommenderad vägledning för systemprestanda.

* **Hård gräns:** En hård gräns ger ett absolut maximum.

>[!NOTE]
>
>De gränser som beskrivs i det här dokumentet förbättras ständigt. Kontrollera regelbundet om det finns uppdateringar. Om du är intresserad av att lära dig mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

## Begränsningar för datamodell

Följande skyddsprofiler ger rekommenderade gränser vid modellering av kundprofildata i realtid. Mer information om primära enheter och dimensionsenheter finns i avsnittet om [enhetstyper](#entity-types) i tillägget.

### Garantier för primära enheter

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Data för klassen XDM Individuella profiler | 20 | Mjuk | Högst 20 datauppsättningar rekommenderas som utnyttjar klassen XDM Individual Profile. |
| XDM ExperienceEvent, klassdatamängder | 20 | Mjuk | Högst 20 datauppsättningar rekommenderas som utnyttjar klassen XDM ExperienceEvent. |
| Adobe Analytics rapportuppsättningar har aktiverats för profil | 1 | Mjuk | Högst en (1) datauppsättning för analysrapportsviten ska aktiveras för profilen. Om du försöker aktivera flera datauppsättningar i Analytics-rapportsviten för profilen kan det få oönskade konsekvenser för datakvaliteten. Mer information finns i avsnittet om [Adobe Analytics dataset](#aa-datasets) i tillägget. |
| Relationer för flera enheter | 5 | Mjuk | Högst fem multientitetsrelationer som definierats mellan primära entiteter och dimensionsenheter rekommenderas. Ytterligare relationsmappningar ska inte göras förrän en befintlig relation tas bort eller inaktiveras. |
| JSON-djup för ID-fält som används i relationer med flera enheter | 4 | Mjuk | Rekommenderat maximalt JSON-djup för ett ID-fält som används i relationer med flera enheter är 4. Detta innebär att i ett mycket kapslat schema ska fält som är kapslade mer än fyra nivåer djupa inte användas som ID-fält i en relation. |
| Matriskardinalitet i ett profilfragment | &lt;=500 | Mjuk | Den optimala arraykardinaliteten i ett profilfragment (tidsoberoende data) är &lt;=500. |
| Array-kardinalitet i ExperienceEvent | &lt;=10 | Mjuk | Den optimala arraykardinaliteten i en ExperienceEvent (tidsseriedata) är &lt;=10. |
| Identitetsantal för individuell profil identitetsdiagram | 50 | Hård | **Det högsta antalet identiteter i ett identitetsdiagram för en enskild profil är 50.** Alla profiler med fler än 50 identiteter exkluderas från segmentering, export och uppslag. |

{style=&quot;table-layout:auto&quot;}

### Dimensionens skyddsräcken

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Inga tidsseriedata tillåts för icke-[!DNL XDM Individual Profile] enheter | 0 | Hård | **Tidsseriedata är inte tillåtna för icke-[!DNL XDM Individual Profile] enheter i profiltjänsten.** Om en tidsseriedatauppsättning är associerad med en icke-[!DNL XDM Individual Profile] ID, datauppsättningen ska inte aktiveras för [!DNL Profile]. |
| Inga kapslade relationer | 0 | Mjuk | Du bör inte skapa en relation mellan två[!DNL XDM Individual Profile] scheman. Möjligheten att skapa relationer rekommenderas inte för scheman som inte ingår i [!DNL Profile] union-schema. |
| JSON-djup för primärt ID-fält | 4 | Mjuk | Rekommenderat maximalt JSON-djup för det primära ID-fältet är 4. Det innebär att du inte ska välja ett fält som primärt ID i ett kapslat schema om det är mer än fyra nivåer djupt. Ett fält på den fjärde kapslade nivån kan användas som primärt ID. |

{style=&quot;table-layout:auto&quot;}

## Begränsningar för datastorlek

Följande skyddsutkast hänvisar till datastorlek och innehåller rekommenderade gränser för data som kan importeras, lagras och frågas efter behov. Mer information om primära enheter och dimensionsenheter finns i avsnittet om [enhetstyper](#entity-types) i tillägget.

>[!NOTE]
>
>Datastorleken mäts som okomprimerade data i JSON vid tidpunkten för intag.

### Garantier för primära enheter

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximal ExperienceEvent-storlek | 10KB | Hård | **Den största tillåtna storleken för en händelse är 10 kB.** Intag fortsätter, men alla händelser som är större än 10 kB kommer att släppas. |
| Största profilpoststorlek | 100KB | Hård | **Den maximala storleken för en profilpost är 100 kB.** Inmatningen fortsätter, men profilposter som är större än 100 kB tas bort. |
| Största profilfragmentstorlek | 50MB | Hård | **Den största tillåtna storleken för ett profilfragment är 50 MB.** Segmentering, export och uppslag kan misslyckas för alla [profilfragment](#profile-fragments) som är större än 50 MB. |
| Maximal storlek för fillagring | 50MB | Mjuk | **Den maximala storleken för en lagrad profil är 50 MB.** Lägger till nytt [profilfragment](#profile-fragments) till en profil som är större än 50 MB kommer att påverka systemets prestanda. En profil kan till exempel innehålla ett enskilt fragment som är 50 MB eller innehålla flera fragment över flera datauppsättningar med en sammanlagd storlek på 50 MB. Om du försöker lagra en profil med ett enskilt fragment som är större än 50 MB, eller med flera fragment som är större än 50 MB i kombination, påverkas systemets prestanda. |
| Antal inkapslade Profile- eller ExperienceEvent-batchar per dag | 90 | Mjuk | **Det högsta antalet profiler eller ExperienceEvent-batchar som har importerats per dag är 90.** Det innebär att den sammanlagda summan av de profiler och ExperienceEvent-batchar som hämtas varje dag inte får överstiga 90. Om du samlar in ytterligare batchar påverkas systemets prestanda. |
| Antal ExperienceEvents per profilpost | 5000 | Mjuk | **Det högsta antalet ExperienceEvents per profilpost är 5 000.** Profiler med fler än 5 000 ExperienceEvents kommer att **not** beaktas för segmentering. |

{style=&quot;table-layout:auto&quot;}

### Dimensionens skyddsräcken

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Total storlek för alla dimensionella enheter | 5GB | Mjuk | Den rekommenderade totala storleken för alla dimensionella enheter är 5 GB. Inmatning av enheter med stora dimensioner kan påverka systemets prestanda. Vi rekommenderar till exempel inte att du försöker läsa in en produktkatalog på 10 GB som en dimensionsenhet. |
| Datamängder per dimensionellt entitetsschema | 5 | Mjuk | Högst 5 datauppsättningar som är associerade med varje dimensionellt enhetsschema rekommenderas. Om du till exempel skapar ett schema för&quot;produkter&quot; och lägger till fem bidragande datauppsättningar, bör du inte skapa en sjätte datauppsättning som är kopplad till produktschemat. |
| Inkapslade batchar för Dimension per dag | 4 per enhet | Mjuk | Rekommenderat maximalt antal inkapslade dimensionsentitetsbatchar per dag är 4 per entitet. Du kan till exempel importera uppdateringar till en produktkatalog upp till 4 gånger per dag. Om ytterligare dimensionsenhetsbatchar för samma enhet anges kan det påverka systemets prestanda. |

{style=&quot;table-layout:auto&quot;}

## Skyddsritningar för segmentering

Skyddsförslaget som beskrivs i detta avsnitt avser antalet segment och typen av segment som en organisation kan skapa inom Experience Platform samt att mappa och aktivera segment till destinationer.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Segment per sandlåda | 4000 | Mjuk | En organisation kan ha mer än 4000 segment totalt, förutsatt att det finns mindre än 4000 segment i varje enskild sandlåda. Om du försöker skapa ytterligare segment kan det påverka systemets prestanda. |
| Kantsegment per sandlåda | 150 | Mjuk | En organisation kan ha fler än 150 kantsegment totalt, förutsatt att det finns mindre än 150 kantsegment i varje enskild sandlåda. Försök att skapa ytterligare kantsegment kan påverka systemets prestanda. |
| Direktuppspelningssegment per sandlåda | 500 | Mjuk | En organisation kan ha fler än 500 direktuppspelningssegment totalt, förutsatt att det finns färre än 500 direktuppspelningssegment i varje enskild sandlåda. Om du försöker skapa fler direktuppspelningssegment kan det påverka systemets prestanda. |
| Gruppsegment per sandlåda | 4000 | Mjuk | En organisation kan ha mer än 4000 gruppsegment totalt, förutsatt att det finns mindre än 4000 gruppsegment i varje enskild sandlåda. Om du försöker skapa ytterligare gruppsegment kan det påverka systemets prestanda. |

{style=&quot;table-layout:auto&quot;}

## Bilaga

I det här avsnittet finns mer information om begränsningarna i det här dokumentet.

### Enhetstyper

The [!DNL Profile] lagringsdatamodellen består av två huvudenhetstyper: [primära enheter](#primary-entity) och [dimensionsenheter](#dimension-entity).

#### Primär entitet

En primär enhet, eller profilenhet, sammanfogar data till en&quot;enda källa till sanning&quot; för en individ. Dessa enhetliga data representeras med hjälp av en s.k. fackvy. En unionsvy samlar fälten för alla scheman som implementerar samma klass i ett enda unionsschema. Unionsschemat för [!DNL Real-Time Customer Profile] är en denormaliserad hybriddatamodell som fungerar som behållare för alla profilattribut och beteendehändelser.

Tidsoberoende attribut, som också kallas&quot;postdata&quot;, modelleras med [!DNL XDM Individual Profile], medan tidsseriedata, som också kallas&quot;händelsedata&quot;, modelleras med [!DNL XDM ExperienceEvent]. När data från register och tidsserier hämtas i Adobe Experience Platform utlöses de [!DNL Real-Time Customer Profile] för att börja inhämta data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

![En infografik som visar skillnaderna mellan postdata och tidsseriedata.](images/guardrails/profile-entity.png)

#### Dimension

Profildatalagret som bevarar profildata är inte ett relationslager, men profilen tillåter integrering med små dimensionsenheter för att skapa segment på ett förenklat och intuitivt sätt. Integrationen kallas [segmentering av flera enheter](../segmentation/multi-entity-segmentation.md).

Din organisation kan också definiera XDM-klasser för att beskriva andra saker än enskilda, t.ex. butiker, produkter eller egenskaper. Dessa[!DNL XDM Individual Profile] scheman kallas&quot;dimensionsenheter&quot; (kallas även&quot;uppslagsenheter&quot;) och innehåller inte tidsseriedata. Scheman som representerar dimensionsenheter är länkade till profilentiteter genom användning av [schemarelationer](../xdm/tutorials/relationship-ui.md).

Dimensioner tillhandahåller sökdata som underlättar och förenklar definitioner av flerenhetssegment och måste vara tillräckligt små för att segmenteringsmotorn ska kunna läsa in hela datauppsättningen i minnet för optimal bearbetning (snabbpunktssökning).

![En infografik som visar att en profilentitet består av dimensionsenheter.](images/guardrails/profile-and-dimension-entities.png)

### Profilfragment

I det här dokumentet finns det flera skyddsutkast som refererar till&quot;profilfragment&quot;. I Experience Platform sammanfogas flera profilfragment till kundprofilen i realtid. Varje fragment representerar en unik primär identitet och motsvarande post eller fullständiga händelsedata för det ID:t inom en given datamängd. Mer information om profilfragment finns i [Profilöversikt](home.md#profile-fragments-vs-merged-profiles).

### Sammanfoga profiler {#merge-policies}

När du sammanfogar data från flera olika källor är sammanslagningsprinciper de regler som används av plattformen för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de för att skapa en enda profil för kunden. När data från flera källor står i konflikt avgör sammanfogningsprincipen vilken information som ska inkluderas i profilen för den enskilda personen. Max fem (5) sammanslagningsprinciper tillåts per organisation. Läs mer om kopplingsregler i [sammanfogningsprinciper - översikt](merge-policies/overview.md).

### Adobe Analytics rapportuppsättningar av datauppsättningar i plattformen {#aa-datasets}

Flera rapportsviter kan aktiveras för profilen så länge som alla datakonflikter är lösta. Du kan använda funktionen Data Prep för att lösa datakonflikter mellan eVars, Lists och Props. Läs mer om hur du använder funktionen Prep i [Användargränssnittshandbok för Adobe Analytics Connector](../sources/tutorials/ui/create/adobe-applications/analytics.md).
