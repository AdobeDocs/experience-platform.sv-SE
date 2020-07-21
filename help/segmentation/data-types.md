---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datatyper för Adobe Experience Platform segmenteringstjänst
topic: overview
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Datatyper som stöds av Adobe Experience Platform [!DNL Segmentation Service]

Alla XDM-datatyper stöds i [!DNL Segmentation Service]. Reglerna som utgör en segmentdefinition är kontextualiserade med följande datatyper.

## Strängdata

Segmentdefinitioner använder strängdata för att definiera icke-numeriska begränsningar för segmentgrupper, som&quot;namn på land&quot; eller&quot;lojalitetsprogramnivå&quot;.

Strängdata inkluderas i segmentdefinitioner med hjälp av logiska, inkluderande/exklusiva och jämförelsesatser. När ett strängattribut har lagts till i segmentdefinitionen kan du använda strängrelevanta satser för att utvärdera det mot andra strängfält.

| Utdragstyp | Exempel |
| -------------- | -------- |
| Logisk | `and`, `or`, `not` |
| Inkluderande/exklusiv | `include`, `must` `exist`, `exclude`, `must not exist` |
| Jämförelse | `equals`, `does not equal`, `contains`, `starts with` |

## Datumdata

Med datumdata kan du tilldela tidsbaserade kontexter till dina segmentdefinitioner, antingen genom att använda specifika start-/slutdatum eller genom att använda datumrelevanta satser enligt tabellen nedan. En implementering kan vara att skapa en målgrupp med kunder som har interagerat med ert varumärke *i år* och som också har varit aktiva *under* de senaste dagarna.

| Exempelfält | Datumrelevanta kontoutdrag | Tidslinje |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevant för den dag segmentet skapades. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant inom en given vecka/månad. |

## Experience Events

Som ett Adobe Experience Platform-schema kan du spela in explicita och implicita kundinteraktioner med [!DNL XDM ExperienceEvents] [!DNL Platform]integrerade program, inklusive en ögonblicksbild av systemet när interaktionen ägde rum. [!DNL ExperienceEvents] är fakta. Därför är de en datakälla som är tillgänglig för dig under segmentdefinitionen.

Som framgår av tabellen nedan återges händelsedata med nyckelord som hjälper till att förfina händelsebeteendet och ange händelseattribut.

| Nyckelord | Använd |
| ------- | --- |
| Inkludera/exkludera | Beskriver hur händelsen beter sig genom att data inkluderas eller utelämnas. |
| Alla | Hjälper till att bestämma antalet kvalificerade segment. |
| Växlingsknappen Använd tidsregel | Innehåller datumdata. |
| Lika med, är inte lika med, börjar med, startar inte med, slutar med, slutar inte med, innehåller, inte innehåller, finns, finns inte | Innehåller strängdata. |

## Segment

Befintliga segmentdefinitioner kan också användas som komponenter i en ny segmentdefinition, vilket lägger till deras attribut och händelsebaserade regler i det nya segmentet.

## Målgrupper

Externa målgrupper kan också användas som komponenter i en ny segmentdefinition och lägga till deras attributregler i det nya segmentet.

För närvarande stöds bara Adobe Audience Manager som målgrupp. Ytterligare källor kommer att aktiveras i framtiden.

## Andra datatyper

Förutom de datatyper som nämns ovan innehåller listan över datatyper som stöds även:

- Uniform resource identifier (URI)
- Enum
- Siffra
- Lång
- Heltal
- Kort
- Byte
- Boolean
- Array
- Objekt
- Mappa