---
keywords: profil;kundprofil i realtid;felsökning;skyddsprofiler;riktlinjer;gräns;enhet;primär enhet;dimension;RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;kunddataplattform i realtid;cdp;b2b;cdp;
title: StandardguarDRAG för Real-time Customer Data Platform B2B Edition
type: Documentation
description: I Adobe Experience Platform används en mycket denormaliserad hybriddatamodell som skiljer sig från den traditionella relationsdatamodellen. Det här dokumentet innehåller standardgränser för användning och frekvens som hjälper dig att modellera data för optimala systemprestanda med Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 6327f5e6cb64a46c502613dd6074d84ed1fdd32b
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 2%

---

# StandardguarDRAG för Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Gränserna som beskrivs i det här dokumentet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkast för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

Med Real-time Customer Data Platform B2B Edition kan ni leverera personaliserade flerkanalsupplevelser baserat på beteendeinsikter och kundattribut i form av kundprofiler i realtid och kontoprofiler. För att stödja den nya metoden för profiler använder Experience Platform en högdenormaliserad hybriddatamodell som skiljer sig från den traditionella relationsdatamodellen.

Det här dokumentet innehåller standardgränser för användning och frekvens som hjälper dig att modellera data för optimala systemprestanda. När du granskar följande skyddsutkast förutsätts det att du har modellerat data korrekt. Om du har frågor om hur du modellerar data kan du kontakta kundtjänstrepresentanten.

>[!INFO]
>
>De flesta kunder överskrider inte dessa standardgränser. Om du vill veta mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

## Begränsningstyper

Det finns två typer av standardgränser i det här dokumentet:

* **Mjuk gräns:** Det går att gå längre än en mjuk gräns, men mjuka gränser ger en rekommenderad vägledning för systemprestanda.

* **Hård gräns:** En hård gräns ger ett absolut maximum.

>[!INFO]
>
>De gränser som beskrivs i det här dokumentet förbättras ständigt. Kontrollera regelbundet om det finns uppdateringar. Om du är intresserad av att lära dig mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

## Begränsningar för datamodell

Följande skyddsprofiler ger rekommenderade gränser vid modellering av kundprofildata i realtid. Mer information om primära enheter och dimensionsenheter finns i avsnittet om [enhetstyper](#entity-types) i tillägget.

### Garantier för primära enheter

>[!NOTE]
>
>De datamodellsbegränsningar som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkast för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Data för XDM-standardklassen i Real-Time CDP B2B Edition | 60 | Mjuk | Högst 60 datauppsättningar rekommenderas som utnyttjar XDM-klasserna (Experience Data Model) som tillhandahålls av Real-Time CDP B2B Edition. En fullständig lista över XDM-standardklasser för B2B-fall finns i [scheman i Real-Time CDP B2B Edition-dokumentation](schemas/b2b.md). <br/><br/>*Obs! På grund av karaktären hos Experience Platform standardiserade hybriddatamodell överskrider de flesta kunder inte denna gräns. Om du har frågor om hur du modellerar data, eller om du vill veta mer om anpassade begränsningar, kontaktar du kundtjänstrepresentanten.* |
| Äldre relationer för flera enheter | 20 | Mjuk | Högst 20 multientitetsrelationer som definierats mellan primära entiteter och dimensionsenheter rekommenderas. Ytterligare relationsmappningar ska inte göras förrän en befintlig relation tas bort eller inaktiveras. |
| Många-till-ett-relationer per XDM-klass | 2 | Mjuk | Högst 2 många-till-en-relationer per XDM-klass rekommenderas. Ytterligare relation bör inte skapas förrän en befintlig relation tas bort eller inaktiveras. Anvisningar om hur du skapar en relation mellan två scheman finns i självstudiekursen om [definiera B2B-schemarelationer](../xdm/tutorials/relationship-b2b.md). |

### Dimensionens skyddsräcken

>[!NOTE]
>
>De datamodellsbegränsningar som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkast för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Inga kapslade äldre relationer | 0 | Mjuk | Du bör inte skapa en relation mellan två[!DNL XDM Individual Profile] scheman. Möjligheten att skapa relationer rekommenderas inte för scheman som inte ingår i [!DNL Profile] union-schema. |
| Endast B2B-objekt kan ingå i många-till-ett-relationer | 0 | Hård | Systemet stöder endast många-till-ett-relationer mellan B2B-objekt. Mer information om många-till-ett-relationer finns i självstudiekursen om [definiera B2B-schemarelationer](../xdm/tutorials/relationship-b2b.md). |
| Maximalt djup för kapslade relationer mellan B2B-objekt | 3 | Hård | Det maximala djupet för kapslade relationer mellan B2B-objekt är 3. Det innebär att du inte bör ha någon relation mellan B2B-objekt som är kapslade mer än tre nivåer i ett mycket kapslat schema. |

## Begränsningar för datastorlek

Följande skyddsutkast hänvisar till datastorlek och innehåller rekommenderade gränser för data som kan importeras, lagras och frågas efter behov. Mer information om primära enheter och dimensionsenheter finns i avsnittet om [enhetstyper](#entity-types) i tillägget.

>[!INFO]
>
>Datastorleken mäts som okomprimerade data i JSON vid tidpunkten för intag.

### Garantier för primära enheter

>[!NOTE]
>
>De begränsningar för datastorlek som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkast för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Inmatade batchar per XDM-klass per dag | 45 | Mjuk | Det totala antalet batchar som intagits varje dag per XDM-klass får inte överstiga 45. Om du samlar in ytterligare batchar kan prestandan bli optimal. |

### Dimensionens skyddsräcken

>[!NOTE]
>
>De begränsningar för datastorlek som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkast för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Total storlek för alla dimensionella enheter | 5GB | Mjuk | Den rekommenderade totala storleken för alla dimensionella enheter är 5 GB. Inmatning av enheter med stora dimensioner kan påverka systemets prestanda. Vi rekommenderar till exempel inte att du försöker läsa in en produktkatalog på 10 GB som en dimensionsenhet. |
| Datamängder per dimensionellt entitetsschema | 5 | Mjuk | Högst 5 datauppsättningar som är associerade med varje dimensionellt enhetsschema rekommenderas. Om du till exempel skapar ett schema för&quot;produkter&quot; och lägger till fem bidragande datauppsättningar, bör du inte skapa en sjätte datauppsättning som är kopplad till produktschemat. |
| Inkapslade batchar för Dimension per dag | 4 per enhet | Mjuk | Rekommenderat maximalt antal inkapslade dimensionsentitetsbatchar per dag är 4 per entitet. Du kan till exempel importera uppdateringar till en produktkatalog upp till 4 gånger per dag. Om ytterligare dimensionsenhetsbatchar för samma enhet anges kan det påverka systemets prestanda. |

## Skyddsritningar för segmentering

Skyddsförslaget som beskrivs i detta avsnitt avser antalet segment och typen av segment som en organisation kan skapa inom Experience Platform samt att mappa och aktivera segment till destinationer.

>[!NOTE]
>
>De segmenteringsgränser som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkast för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Segment per B2B-sandlåda | 400 | Mjuk | En organisation kan ha fler än 400 segment totalt, förutsatt att det finns färre än 400 segment i varje enskild B2B-sandlåda. Om du försöker skapa ytterligare segment kan det påverka systemets prestanda. |

## Nästa steg

Gränserna som beskrivs i det här dokumentet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkast för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

## Bilaga

I det här avsnittet finns mer information om begränsningarna i det här dokumentet.

### Enhetstyper

The [!DNL Profile] lagringsdatamodellen består av två huvudenhetstyper: [primära enheter](#primary-entity) och [dimensionsenheter](#dimension-entity).

#### Primär entitet

En primär enhet, eller profilenhet, sammanfogar data till en&quot;enda källa till sanning&quot; för en individ. Dessa enhetliga data representeras med hjälp av en s.k. fackvy. En unionsvy samlar fälten för alla scheman som implementerar samma klass i ett enda unionsschema. Unionsschemat för [!DNL Real-Time Customer Profile] är en denormaliserad hybriddatamodell som fungerar som behållare för alla profilattribut och beteendehändelser.

Tidsoberoende attribut, som också kallas&quot;postdata&quot;, modelleras med [!DNL XDM Individual Profile], medan tidsseriedata, som också kallas&quot;händelsedata&quot;, modelleras med [!DNL XDM ExperienceEvent]. När data från register och tidsserier hämtas i Adobe Experience Platform utlöses de [!DNL Real-Time Customer Profile] för att börja inhämta data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

![En infografik som visar skillnaderna mellan postdata och tidsseriedata.](../profile/images/guardrails/profile-entity.png)

#### Dimension

Profildatalagret som bevarar profildata är inte ett relationslager, men profilen tillåter integrering med små dimensionsenheter för att skapa segment på ett förenklat och intuitivt sätt. Integrationen kallas [segmentering av flera enheter](../segmentation/multi-entity-segmentation.md).

Din organisation kan också definiera XDM-klasser för att beskriva andra saker än enskilda, t.ex. butiker, produkter eller egenskaper. Dessa[!DNL XDM Individual Profile] scheman kallas&quot;dimensionsenheter&quot; (kallas även&quot;uppslagsenheter&quot;) och innehåller inte tidsseriedata. Scheman som representerar dimensionsenheter är länkade till profilentiteter genom användning av [schemarelationer](../xdm/tutorials/relationship-ui.md).

Dimensioner tillhandahåller sökdata som underlättar och förenklar definitioner av flerenhetssegment och måste vara tillräckligt små för att segmenteringsmotorn ska kunna läsa in hela datauppsättningen i minnet för optimal bearbetning (snabbpunktssökning).

![En infografik som visar att en profilentitet består av dimensionsenheter.](../profile/images/guardrails/profile-and-dimension-entities.png)