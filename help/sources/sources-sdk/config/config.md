---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Konfigurationsalternativ i självbetjäningskällor (batch-SDK)
description: Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda självbetjäningskällor (Batch SDK).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Konfigurationsalternativ i självbetjäningskällor (batch-SDK)

Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda självbetjäningskällor (Batch SDK).

## Anslutningsspecifikation

Anslutningsspecifikationerna returnerar en källas kopplingsegenskaper. De innehåller autentiseringsspecifikationer som är relaterade till att skapa bas- och källanslutningar samt ett fast anslutnings-ID som tilldelats en viss källa. Anslutningsspecifikationerna är innehavar- och organisationsagnostiker. En typisk anslutningsspecifikation innehåller grundläggande information om en viss källa samt tre olika avsnitt: `authSpec`, `sourceSpec` och `exploreSpec`.

| Specifikationer | Beskrivning |
| --- | --- |
| `authSpec` | Arrayen `authSpec` innehåller information om de autentiseringsparametrar som krävs för att ansluta en källa till plattformen. Alla angivna källor har stöd för flera olika typer av autentisering. |
| `sourceSpec` | Arrayen `sourceSpec` innehåller allmän information om en källa, inklusive information om attribut som krävs för att presentera källan i gränssnittet, dokumentationslänk och parametrar för sidnumrering, rubrik, brödtext och schemaläggning. Dessutom beskriver `sourceSpec` schemat för de parametrar som krävs för att skapa en källanslutning från en basanslutning och som är nödvändiga för att skapa en källanslutning. |
| `exploreSpec` | Arrayen `exploreSpec` definierar de parametrar som krävs för att utforska och inspektera objekt som finns i källan. `exploreSpec` definierar också svarsformatet som returneras när objekt utforskas och inspekteras. |

{style="table-layout:auto"}

## Fyll i värden för anslutningsspecifikation

En anslutningsspecifikation kan delas in i tre olika delar: autentiseringsspecifikationerna, källspecifikationerna och undersökningsspecifikationerna.

I följande dokument finns instruktioner om hur du fyller i värdena för varje del av en anslutningsspecifikation:

* [Konfigurera autentiseringsspecifikationen](./authspec.md)
* [Konfigurera din källspecifikation](./sourcespec.md)
* [Konfigurera din specifikation för utforskande](./explorespec.md)
