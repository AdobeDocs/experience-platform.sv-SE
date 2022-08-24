---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Konfigurationsalternativ i självbetjäningskällor (batch-SDK)
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda självbetjäningskällor (Batch SDK).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Konfigurationsalternativ i självbetjäningskällor (batch-SDK)

Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda självbetjäningskällor (Batch SDK).

## Anslutningsspecifikation

Anslutningsspecifikationerna returnerar en källas kopplingsegenskaper. De innehåller autentiseringsspecifikationer som relaterar till att skapa bas- och källanslutningar och ett fast anslutningsspecifikations-ID som tilldelats en viss källa. Anslutningsspecifikationerna är innehavar- och organisationsagnostiker. En typisk anslutningsspecifikation innehåller grundläggande information om en viss källa samt tre olika avsnitt: `authSpec`, `sourceSpec`och `exploreSpec`.

| Specifikationer | Beskrivning |
| --- | --- |
| `authSpec` | The `authSpec` arrayen innehåller information om de autentiseringsparametrar som krävs för att ansluta en källa till plattformen. Alla angivna källor har stöd för flera olika typer av autentisering. |
| `sourceSpec` | The `sourceSpec` arrayen innehåller allmän information om en källa, inklusive information om attribut som krävs för att visa källan i gränssnittet, dokumentationslänk och parametrar för sidnumrering, rubrik, brödtext och schemaläggning. Dessutom `sourceSpec` beskriver schemat för de parametrar som krävs för att skapa en källanslutning från en basanslutning och som är nödvändiga för att skapa en källanslutning. |
| `exploreSpec` | The `exploreSpec` -arrayen definierar de parametrar som krävs för att utforska och inspektera objekt som finns i källan. The `exploreSpec` definierar också det svarsformat som returneras när objekt utforskas och inspekteras. |

{style=&quot;table-layout:auto&quot;}

## Fyll i värden för anslutningsspecifikation

En anslutningsspecifikation kan delas in i tre olika delar: autentiseringsspecifikationer, källspecifikationer och specifikationer.

I följande dokument finns instruktioner om hur du fyller i värdena för varje del av en anslutningsspecifikation:

* [Konfigurera autentiseringsspecifikationen](./authspec.md)
* [Konfigurera källspecifikationen](./sourcespec.md)
* [Konfigurera din utforskarspecifikation](./explorespec.md)
