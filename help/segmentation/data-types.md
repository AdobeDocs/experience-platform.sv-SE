---
solution: Experience Platform
title: Datatyper som stöds i segmenteringstjänsten
description: Alla XDM-datatyper (Experience Data Model) stöds i Adobe segmenteringstjänst. Reglerna som utgör en segmentdefinition är kontextualiserade med följande datatyper.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Datatyper som stöds i segmenteringstjänsten

Alla XDM-datatyper (Experience Data Model) stöds i Adobe Experience Platform segmenteringstjänst. Reglerna som utgör en segmentdefinition är kontextualiserade med följande datatyper.

## Strängdata

Segmentdefinitioner använder strängdata för att definiera icke-numeriska begränsningar för målgrupper, till exempel&quot;landsnamn&quot; eller&quot;lojalitetsprogramnivå&quot;.

Strängdata inkluderas i segmentdefinitioner med hjälp av logiska, inkluderande/exklusiva och jämförelsesatser. När ett strängattribut har lagts till i segmentdefinitionen kan du använda strängrelevanta satser för att utvärdera det mot andra strängfält.

| Utdragstyp | Exempel |
| -------------- | -------- |
| Logisk | `and`, `or`, `not` |
| Inkluderande/exklusiv | `include`, `must` `exist`, `exclude`, `must not exist` |
| Jämförelse | `equals`, `does not equal`, `contains`, `starts with` |

## Datumdata

Med datumdata kan du tilldela tidsbaserade kontexter till dina segmentdefinitioner, antingen genom att använda specifika start-/slutdatum eller genom att använda datumrelevanta satser enligt tabellen nedan. En implementering kan vara att skapa en målgrupp med kunder som har interagerat med ert varumärke när som helst *i år* och som också har varit aktiva *inom* de senaste dagarna.

| Exempelfält | Datumrelevanta kontoutdrag | Tidslinje |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevant för den dag då segmentdefinitionen skapades. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant inom en given vecka/månad. |

## Experience Events

Som ett Adobe Experience Platform-schema spelar [!DNL XDM ExperienceEvents] in explicita och implicita kundinteraktioner med Experience-Platform-integrerade program, inklusive en ögonblicksbild av systemet när interaktionen ägde rum. [!DNL ExperienceEvents] är faktauppgifter. Därför är de en datakälla som är tillgänglig för dig under segmentdefinitionen.

Som framgår av tabellen nedan återges händelsedata med nyckelord som hjälper till att förfina händelsebeteendet och ange händelseattribut.

| Nyckelord | Använd |
| ------- | --- |
| Inkludera/exkludera | Beskriver hur händelsen beter sig genom att data inkluderas eller utelämnas. |
| Alla | Hjälper till att bestämma antalet kvalificerade segmentdefinitioner. |
| Växlingsknappen Använd tidsregel | Innehåller datumdata. |
| Lika med, är inte lika med, börjar med, startar inte med, slutar med, slutar inte med, innehåller, inte innehåller, finns, finns inte | Innehåller strängdata. |

### Målgruppsdelning

Externa målgrupper kan också användas som komponenter i en ny segmentdefinition och lägga till deras attributregler i de nya segmentdefinitionerna.

För närvarande stöds endast Adobe Audience Manager som extern publik, och ytterligare källor aktiveras i framtiden. Mer information om hur du använder Adobe Audience Manager-målgrupper med Experience Platform finns i [målgruppsdelningshandboken i Adobe Audience Manager-dokumentationen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Segmentdefinitionsdelning

Segmentdefinitioner som har skapats i Experience Platform kan användas i andra [Adobe Experience Cloud Core Services](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html). Om du vill aktivera den här funktionen måste du kontakta din lösningsarkitekt eller din konsult.

## Andra datatyper

Förutom de datatyper som nämns ovan innehåller listan över datatyper som stöds även:

- Uniform resource identifier (URI)
- Enum
- Nummer
- Lång
- Heltal
- Kort
- Byte
- Boolean
- Array
- Objekt
- Karta
