---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;skyddsförslag;riktlinjer;begränsning;enhet;primär enhet;dimensionsenhet;
title: Experience Platform Guardrails för kundprofildata i realtid
solution: Experience Platform
product: experience platform
topic: guide
type: Documentation
description: 'Adobe Experience Platform tillhandahåller ett antal skyddsutkast som hjälper dig att undvika att skapa datamodeller som kundprofilen i realtid inte stöder. I det här dokumentet beskrivs de bästa metoderna och begränsningarna som du bör tänka på när du modellerar profildata. '
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 1%

---


# [!DNL Platform] skyddsräcken för  [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] innehåller individuella profiler som gör att ni kan leverera personaliserade upplevelser över flera kanaler baserat på beteendeinsikter och kundattribut. För att uppnå detta använder [!DNL Profile] och segmenteringsmotorn i Adobe Experience Platform en högdenormaliserad hybriddatamodell som erbjuder ett nytt sätt att utveckla kundprofiler. Användning av denna hybriddatamodell gör det oerhört viktigt att de data som samlas in är korrekt utformade. Trots att datalagret [!DNL Profile] som bevarar profildata inte är ett relationsarkiv, tillåter [!DNL Profile] integrering med små dimensionsenheter för att skapa segment på ett förenklat och intuitivt sätt. Denna integrering kallas segmentering för flera enheter.

Adobe Experience Platform tillhandahåller en serie skyddsutkast som hjälper dig att undvika att skapa datamodeller som [!DNL Real-time Customer Profile] inte stöder. I det här dokumentet beskrivs dessa skyddsutkast samt bästa praxis och begränsningar när profildata används för segmentering.

>[!NOTE]
>
>Skyddsritningarna och begränsningarna som beskrivs i det här dokumentet förbättras ständigt. Kontrollera regelbundet om det finns uppdateringar.

## Komma igång

Vi rekommenderar att du läser följande dokumentation för Experience Platform-tjänster innan du försöker skapa datamodeller som kan användas i [!DNL Real-time Customer Profile]. Att arbeta med datamodeller och de skyddsutkast som beskrivs i det här dokumentet kräver förståelse för de olika Experience Platform-tjänster som används för att hantera [!DNL Real-time Customer Profile]-enheter:

* [[!DNL Real-time Customer Profile]](home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Adobe Experience Platform Identity Service](../identity-service/home.md): Stöder skapandet av en&quot;enda bild av kunden&quot; genom att överbrygga identiteter från olika datakällor när de hämtas in i  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../xdm/schema/composition.md): En introduktion till scheman och datamodellering i Experience Platform.
* [Adobe Experience Platform segmenteringstjänst](../segmentation/home.md): Segmenteringsmotorn som  [!DNL Platform] används för att skapa målgruppssegment utifrån kundprofiler baserat på kundbeteenden och attribut.
   * [Segmentering](../segmentation/multi-entity-segmentation.md) av flera enheter: En guide för att skapa segment som integrerar dimensionsenheter med profildata.

## Enhetstyper

Lagringsdatamodellen [!DNL Profile] består av två huvudentitetstyper:

* **Primär entitet:** En primär entitet, eller profilentitet, sammanfogar data till en&quot;enda källa till sanning&quot; för en individ. Dessa enhetliga data representeras med hjälp av en s.k. fackvy. En unionsvy samlar fälten för alla scheman som implementerar samma klass i ett enda unionsschema. Unionsschemat för [!DNL Real-time Customer Profile] är en denormaliserad hybriddatamodell som fungerar som en behållare för alla profilattribut och beteendehändelser.

   Tidsoberoende attribut, som också kallas&quot;postdata&quot;, modelleras med [!DNL XDM Individual Profile], medan tidsseriedata, som också kallas&quot;händelsedata&quot;, modelleras med [!DNL XDM ExperienceEvent]. När post- och tidsseriedata importeras i Adobe Experience Platform utlöses [!DNL Real-time Customer Profile] för att börja inhämta data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

   ![](images/guardrails/profile-entity.png)

* **Dimension:** Din organisation kan också definiera XDM-klasser för att beskriva andra saker än enskilda, t.ex. butiker, produkter eller egenskaper. Dessa icke-[!DNL XDM Individual Profile]-scheman kallas för &quot;dimensionsenheter&quot; och innehåller inte tidsseriedata. Dimensioner tillhandahåller sökdata som underlättar och förenklar definitioner av flerenhetssegment och måste vara tillräckligt små för att segmenteringsmotorn ska kunna läsa in hela datauppsättningen i minnet för optimal bearbetning (snabbpunktssökning).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Begränsningstyper

När du definierar din datamodell bör du hålla dig inom de angivna säkerhetsrutorna för att säkerställa korrekt prestanda och undvika systemfel. Skyddsritningarna i det här dokumentet innehåller två begränsningstyper:

* **Mjuk gräns:** En mjuk gräns ger ett rekommenderat maximum för optimal systemprestanda. Det går att gå längre än en mjuk gräns utan att systemet bryts eller felmeddelanden tas emot, men om du går längre än en mjuk gräns försämras prestandan. Vi rekommenderar att du håller dig inom den mjuka gränsen för att undvika försämrade prestanda.

* **Hård gräns:** En hård gräns ger ett absolut maximum för systemet. Om du går längre än en hård gräns kommer det att leda till fel och att systemet inte fungerar som det ska.

## Skyddsutkast för datamodell

Du bör följa följande skyddsutkast när du skapar en datamodell som ska användas med [!DNL Real-time Customer Profile].

### Garantier för primära enheter

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Antal datauppsättningar som rekommenderas för att bidra till unionsschemat [!DNL Profile] | 20 | Mjuk | **Högst 20  [!DNL Profile]aktiverade datauppsättningar rekommenderas.** Om du vill aktivera en annan datauppsättning för  [!DNL Profile]måste du först ta bort eller inaktivera en befintlig datauppsättning. |
| Antal multientitetsrelationer som rekommenderas | 5 | Mjuk | **Högst fem multientitetsrelationer som definierats mellan primära entiteter och dimensionsenheter rekommenderas.** Ytterligare relationsmappningar ska inte göras förrän en befintlig relation tas bort eller inaktiveras. |
| Högsta JSON-djup för ID-fält som används i relationer med flera enheter | 4 | Mjuk | **Rekommenderat maximalt JSON-djup för ett ID-fält som används i relationer med flera enheter är 4.** Detta innebär att i ett mycket kapslat schema ska fält som är kapslade mer än fyra nivåer djupa inte användas som ID-fält i en relation. |
| Matriskardinalitet i ett profilfragment | &lt;> | Mjuk | **Den optimala arraykardinaliteten i ett profilfragment (tidsoberoende data) är  &lt;>** |
| Array-kardinalitet i ExperienceEvent | &lt;> | Mjuk | **Den optimala arraykardinaliteten i en ExperienceEvent (tidsseriedata) är  &lt;>** |

### Dimensionens skyddsräcken

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Inga tidsseriedata tillåts för icke-[!DNL XDM Individual Profile]-entiteter | 0 | Hård | **Tidsseriedata tillåts inte för icke-[!DNL XDM Individual Profile] enheter i profiltjänsten.** Om en tidsseriedatauppsättning är associerad med ett icke-[!DNL XDM Individual Profile] ID ska datauppsättningen inte aktiveras för  [!DNL Profile]. |
| Inga kapslade relationer | 0 | Mjuk | **Du bör inte skapa en relation mellan två icke-[!DNL XDM Individual Profile] scheman.** Möjligheten att skapa relationer rekommenderas inte för scheman som inte ingår i  [!DNL Profile] unionsschemat. |
| Högsta JSON-djup för primärt ID-fält | 4 | Mjuk | **Rekommenderat maximalt JSON-djup för det primära ID-fältet är 4.** Det innebär att du inte ska välja ett fält som primärt ID i ett kapslat schema om det är mer än fyra nivåer djupt. Ett fält på den fjärde kapslade nivån kan användas som primärt ID. |

## Skyddsutkast för datastorlek

Följande skyddsutkast refererar till datastorleken och rekommenderas för att säkerställa att data kan importeras, lagras och frågas på rätt sätt.

>[!NOTE]
>
>Datastorleken mäts som okomprimerade data i JSON vid tidpunkten för intag.

### Garantier för primära enheter

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximal storlek per profilfragment | 10 kB | Mjuk | **Den rekommenderade maximala storleken för ett profilfragment är 10 kB.** Om du samlar in större profilfragment påverkas systemets prestanda. Om du till exempel läser in en stor CRM-datauppsättning där vissa profilfragment är 50 kB så försämras systemets prestanda. |
| Absolut maxstorlek per profilfragment | 1 MB | Hård | **Den absoluta största storleken för ett profilfragment är 1 MB.** Inmatningen misslyckas när du försöker överföra ett profilfragment som är större än 1 MB. |

### Dimensionens skyddsräcken

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximal total storlek för alla dimensionsenheter | 5 GB | Mjuk | **Den maximala rekommenderade totala storleken för alla dimensionella enheter är 5 GB.** Inhämtning av enheter med stora dimensioner resulterar i försämrade systemprestanda. Vi rekommenderar till exempel inte att du försöker läsa in en produktkatalog på 10 GB som en dimensionsenhet. |
| Datamängder per dimensionellt entitetsschema | 5 | Mjuk | **Högst 5 datauppsättningar som är associerade med varje dimensionellt enhetsschema rekommenderas.** Om du till exempel skapar ett schema för&quot;produkter&quot; och lägger till fem bidragande datauppsättningar, bör du inte skapa en sjätte datauppsättning som är kopplad till produktschemat. |

## Skyddsritningar för segmentering

Skyddsförslaget som beskrivs i detta avsnitt avser antalet segment och typen av segment som en organisation kan skapa inom Experience Platform samt att mappa och aktivera segment till destinationer.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal segment per sandlåda | 10 kB | Mjuk | **Det högsta antalet segment som en organisation kan skapa är 10 000 per sandlåda.** En organisation kan ha fler än 10 000 segment totalt, förutsatt att det finns färre än 10 000 segment i varje enskild sandlåda. Om du försöker skapa ytterligare segment försämras systemets prestanda. |
| Maximalt antal direktuppspelningssegment per sandlåda | 500 | Mjuk | **Det maximala antalet direktuppspelningssegment som en organisation kan skapa är 500 per sandlåda.** En organisation kan ha fler än 500 direktuppspelningssegment totalt, förutsatt att det finns färre än 500 direktuppspelningssegment i varje enskild sandlåda. Om du försöker skapa ytterligare strömningssegment försämras systemets prestanda. |
| Maximalt antal gruppsegment per sandlåda | 10 kB | Mjuk | **Det maximala antalet gruppsegment som en organisation kan skapa är 10 000 per sandlåda.** En organisation kan ha fler än 10 000 gruppsegment totalt, förutsatt att det finns färre än 10 000 gruppsegment i varje enskild sandlåda. Om du försöker skapa ytterligare gruppsegment försämras systemets prestanda. |