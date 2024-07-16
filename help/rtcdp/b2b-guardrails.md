---
keywords: profil;kundprofil i realtid;felsökning;skyddsprofiler;riktlinjer;gräns;enhet;primär enhet;dimension;RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;kunddataplattform i realtid;cdp;b2b;cdp;
title: StandardguarDRAG för Real-time Customer Data Platform B2B Edition
type: Documentation
description: I Adobe Experience Platform används en mycket denormaliserad hybriddatamodell som skiljer sig från den traditionella relationsdatamodellen. Det här dokumentet innehåller standardgränser för användning och frekvens som hjälper dig att modellera data för optimala systemprestanda med Adobe Real-time Customer Data Platform B2B Edition.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Guardrails, B2B
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 1%

---

# StandardguarDRAG för Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Gränserna som beskrivs i det här dokumentet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkastet för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

Med Real-time Customer Data Platform B2B Edition kan ni leverera personaliserade flerkanalsupplevelser baserat på beteendeinsikter och kundattribut i form av kundprofiler i realtid och kontoprofiler. För att stödja den nya metoden för profiler använder Experience Platform en högdenormaliserad hybriddatamodell som skiljer sig från den traditionella relationsdatamodellen.

>[!IMPORTANT]
>
>Kontrollera dina licensrättigheter i din försäljningsorder och motsvarande [produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions.html) om faktiska användningsbegränsningar, utöver den här sidan med skyddsförslag.

Det här dokumentet innehåller standardgränser för användning och frekvens som hjälper dig att modellera data för optimala systemprestanda. När du granskar följande skyddsutkast förutsätts det att du har modellerat data korrekt. Om du har frågor om hur du modellerar data kan du kontakta kundtjänstrepresentanten.

>[!INFO]
>
>De flesta kunder överskrider inte dessa standardgränser. Om du vill veta mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

## Begränsningstyper

Det finns två typer av standardgränser i det här dokumentet:

| Typ av skyddsräcke | Beskrivning |
| -------------- | ----------- |
| **Prestandaskydd (mjuk gräns)** | Prestandaskydd är användarbegränsningar som relaterar till omfattningen av dina användningsfall. När du överskrider prestandaskyddet kan du uppleva prestandaförsämringar och fördröjning. Adobe ansvarar inte för sådana prestandaförsämringar. Kunder som genomgående överskrider ett prestandaresäkerhetsskydd kan välja att licensiera ytterligare kapacitet för att undvika prestandaförsämringar. |
| **Systemstyrda skyddsräcken (hård begränsning)** | Systemstyrda skyddsräcken används av Real-Time CDP gränssnitt eller API. Det här är begränsningar som du inte kan överskrida eftersom gränssnittet och API kommer att blockera dig från att göra det eller returnera ett fel. |

>[!INFO]
>
>De gränser som beskrivs i det här dokumentet förbättras ständigt. Kontrollera regelbundet om det finns uppdateringar. Om du är intresserad av att lära dig mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.

## Begränsningar för datamodell

Följande skyddsprofiler ger rekommenderade gränser vid modellering av kundprofildata i realtid. Mer information om primära entiteter och dimensionsenheter finns i avsnittet [enhetstyper](#entity-types) i tillägget.

### Garantier för primära enheter

>[!NOTE]
>
>De datamodellsbegränsningar som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkastet för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --------- | ----- | ---------- | ----------- |
| Data för XDM-standardklassen i Real-Time CDP B2B Edition | 60 | Prestandaskydd | Högst 60 datauppsättningar rekommenderas som utnyttjar XDM-klasserna (Experience Data Model) som tillhandahålls av Real-Time CDP B2B Edition. En fullständig lista över XDM-standardklasser för B2B-användningsfall finns i [scheman i dokumentationen för Real-Time CDP B2B Edition](schemas/b2b.md). <br/><br/>*Obs! På grund av karaktären hos en standardiserad hybriddatamodell överskrider de flesta kunder inte den här gränsen. Om du har frågor om hur du modellerar dina data, eller om du vill veta mer om anpassade begränsningar, kontaktar du kundtjänstrepresentanten.* |
| Identitetsantal för enskilt konto i ett identitetsdiagram | 50 | Prestandaskydd | Det högsta antalet identiteter i ett identitetsdiagram för ett enskilt konto är 50. Alla profiler med fler än 50 identiteter exkluderas från segmentering, export och uppslag. |
| Äldre relationer för flera enheter | 20 | Prestandaskydd | Högst 20 multientitetsrelationer som definierats mellan primära entiteter och dimensionsenheter rekommenderas. Ytterligare relationsmappningar ska inte göras förrän en befintlig relation tas bort eller inaktiveras. |
| Många-till-ett-relationer per XDM-klass | 2 | Prestandaskydd | Högst 2 många-till-en-relationer per XDM-klass rekommenderas. Ytterligare relation bör inte skapas förrän en befintlig relation tas bort eller inaktiveras. Anvisningar om hur du skapar en relation mellan två scheman finns i självstudiekursen [Definiera B2B-schemarelationer](../xdm/tutorials/relationship-b2b.md). |

### Skyddsutkast för Dimension

>[!NOTE]
>
>De datamodellsbegränsningar som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkastet för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --------- | ----- | ---------- | ----------- |
| Inga kapslade äldre relationer | 0 | Prestandaskydd | Du bör inte skapa en relation mellan två scheman som inte är [!DNL XDM Individual Profile]. Det rekommenderas **inte** att skapa relationer för alla scheman som inte är en del av det [!DNL Profile] unionsschemat. |
| Endast B2B-objekt kan ingå i många-till-ett-relationer | 0 | Systemstyrt skyddsräcke | Systemet stöder endast många-till-ett-relationer mellan B2B-objekt. Mer information om många-till-ett-relationer finns i självstudiekursen [Definiera B2B-schemarelationer](../xdm/tutorials/relationship-b2b.md). |
| Högsta antal kapslade relationer mellan B2B-objekt | 3 | Systemstyrt skyddsräcke | Det maximala djupet för kapslade relationer mellan B2B-objekt är 3. Det innebär att du inte bör ha någon relation mellan B2B-objekt som är kapslade mer än tre nivåer i ett mycket kapslat schema. |
| Ett schema för varje dimensionsenhet | 1 | Systemstyrt skyddsräcke | Varje dimensionsenhet måste ha ett enda schema. Försök att använda dimensionsenheter som skapats från mer än ett schema kan påverka segmenteringsresultaten. Olika dimensionsenheter förväntas ha separata scheman. |

## Begränsningar för datastorlek

Följande skyddsutkast hänvisar till datastorlek och innehåller rekommenderade gränser för data som kan importeras, lagras och frågas efter behov. Mer information om primära entiteter och dimensionsenheter finns i avsnittet [enhetstyper](#entity-types) i tillägget.

>[!INFO]
>
>Datastorleken mäts som okomprimerade data i JSON vid tidpunkten för intag.

### Garantier för primära enheter

>[!NOTE]
>
>De begränsningar för datastorlek som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkastet för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --------- | ----- | ---------- | ----------- |
| Inmatade batchar per XDM-klass per dag | 45 | Prestandaskydd | Det totala antalet batchar som intagits varje dag per XDM-klass får inte överstiga 45. Om du samlar in ytterligare batchar kan prestandan bli optimal. |

### Skyddsutkast för Dimension

>[!NOTE]
>
>De begränsningar för datastorlek som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkastet för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --------- | ----- | ---------- | ----------- |
| Total storlek för alla dimensionella enheter | 5 GB | Prestandaskydd | Den rekommenderade totala storleken för alla dimensionella enheter är 5 GB. Inmatning av enheter med stora dimensioner kan påverka systemets prestanda. Vi rekommenderar till exempel inte att du försöker läsa in en produktkatalog på 10 GB som en dimensionsenhet. |
| Datamängder per dimensionellt entitetsschema | 5 | Prestandaskydd | Högst 5 datauppsättningar som är associerade med varje dimensionellt enhetsschema rekommenderas. Om du till exempel skapar ett schema för&quot;produkter&quot; och lägger till fem bidragande datauppsättningar, bör du inte skapa en sjätte datauppsättning som är kopplad till produktschemat. |
| Inkapslade batchar för Dimension per dag | 4 per enhet | Prestandaskydd | Rekommenderat maximalt antal inkapslade dimensionsentitetsbatchar per dag är 4 per entitet. Du kan till exempel importera uppdateringar till en produktkatalog upp till 4 gånger per dag. Om ytterligare dimensionsenhetsbatchar för samma enhet anges kan det påverka systemets prestanda. |

## Skyddsritningar för segmentering

De skyddsutkast som beskrivs i detta avsnitt avser antalet och typen av målgrupper som en organisation kan skapa inom Experience Platform samt kartläggning och aktivering av målgrupper till destinationer.

>[!NOTE]
>
>De segmenteringsgränser som beskrivs i det här avsnittet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkastet för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --------- | ----- | ---------- | ----------- |
| Segmentdefinitioner per B2B-sandlåda | 400 | Prestandaskydd | En organisation kan ha fler än 400 segmentdefinitioner totalt, förutsatt att det finns färre än 400 segmentdefinitioner i varje enskild B2B-sandlåda. Om du försöker skapa ytterligare segmentdefinitioner kan det påverka systemets prestanda. |

## Nästa steg

Gränserna som beskrivs i det här dokumentet representerar de ändringar som är aktiverade i Real-time Customer Data Platform B2B Edition. En fullständig lista över standardgränser för Real-Time CDP B2B Edition får du om du kombinerar dessa gränser med de allmänna Adobe Experience Platform-gränserna i [skyddsutkastet för dokumentationen av kundprofildata i realtid](../profile/guardrails.md).

## Bilaga

I det här avsnittet finns mer information om begränsningarna i det här dokumentet.

### Enhetstyper

Datamodellen för lagringsplatsen [!DNL Profile] består av två huvudentitetstyper: [primära entiteter](#primary-entity) och [dimensionsenheter](#dimension-entity).

#### Primär entitet

En primär enhet, eller profilenhet, sammanfogar data till en&quot;enda källa till sanning&quot; för en individ. Dessa enhetliga data representeras med hjälp av en s.k. fackvy. En unionsvy samlar fälten för alla scheman som implementerar samma klass i ett enda unionsschema. Unionsschemat för [!DNL Real-Time Customer Profile] är en denormaliserad hybriddatamodell som fungerar som en behållare för alla profilattribut och beteendehändelser.

Tidsoberoende attribut, som också kallas postdata, modelleras med [!DNL XDM Individual Profile], medan tidsseriedata, som också kallas händelsedata, modelleras med [!DNL XDM ExperienceEvent]. När post- och tidsseriedata importeras i Adobe Experience Platform, utlöses [!DNL Real-Time Customer Profile] för att börja inhämta data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

![En infografik som visar skillnaderna mellan postdata och tidsseriedata.](../profile/images/guardrails/profile-entity.png)

#### Dimension

Profildatalagret som bevarar profildata är inte ett relationslager, men profilen tillåter integrering med små dimensionsenheter för att skapa målgrupper på ett förenklat och intuitivt sätt. Integrationen kallas [segmentering för flera enheter](../segmentation/multi-entity-segmentation.md).

Din organisation kan också definiera XDM-klasser för att beskriva andra saker än enskilda, t.ex. butiker, produkter eller egenskaper. Dessa icke-[!DNL XDM Individual Profile]-scheman kallas för dimensionsenheter (kallas även för sökentiteter) och innehåller inga tidsseriedata. Scheman som representerar dimensionsenheter är länkade till profilentiteter med hjälp av [schemarelationer](../xdm/tutorials/relationship-ui.md).

Dimensioner tillhandahåller sökdata som underlättar och förenklar definitioner av flerenhetssegment och måste vara tillräckligt små för att segmenteringsmotorn ska kunna läsa in hela datauppsättningen i minnet för optimal bearbetning (snabbpunktssökning).

![En infografik som visar att en profilentitet består av dimensionsenheter.](../profile/images/guardrails/profile-and-dimension-entities.png)
