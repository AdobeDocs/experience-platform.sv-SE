---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Indata och utdata för AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 66ccea896846c1da4310c1077e2dc7066a258063

---


# Indata och utdata för AI

Följande dokument visar de olika in- och utdata som används i kundens AI.

## AI-indata för kund

Kunds-AI använder data från kundupplevelsehändelser för att beräkna benägenhetspoängen. Mer information om konsumentupplevelsehändelser finns i [Förbered data för användning i dokumentationen](../data-preparation.md)för intelligenta tjänster.

## Kundens AI-utdata

Kund-AI genererar flera attribut för enskilda profiler som anses berättigade. Det finns två sätt att använda poängen baserat på vad du har etablerat. Om du har aktiverat kundprofil i realtid för din datauppsättning kan du använda den via kundprofilen i realtid. Om du inte har någon kundprofil i realtid kan du hämta den kunds-AI-utdatauppsättning som finns tillgänglig i datasjön.

>[!NOTE]
>Utdatavärden används av kundprofilen i realtid som kan användas för att skapa och definiera segment.

Tabellen nedan beskriver de olika attribut som finns i utdata från kundens AI:

| Attribut | Beskrivning |
| ----- | ----------- |
| Poäng | Den relativa sannolikheten för att en kund ska uppnå det förväntade målet inom den definierade tidsramen. Detta värde ska inte behandlas som sannolikhetsprocent utan snarare som sannolikheten för en individ jämfört med den totala populationen. Poängen varierar mellan 0 och 100. |
| Sannolikhet | Det här attributet är den verkliga sannolikheten för att en profil ska uppnå det förväntade målet inom den definierade tidsramen. När du jämför utdata för olika mål bör du överväga sannolikhet över percentil eller poäng. Sannolikhet bör alltid användas vid bestämning av den genomsnittliga sannolikheten i hela den stödberättigade populationen, eftersom sannolikheten tenderar att vara på den nedre sidan för händelser som inte inträffar ofta. Värden för sannolikhetsintervallet mellan 0 och 1. |
| Procent | Det här värdet ger information om en profils prestanda i förhållande till andra profiler med liknande resultat. En profil med en percentilrankning på 99 för kurn visar till exempel att den har en större risk att kurva jämfört med 99 % av alla andra profiler som bedömdes. Percentiler varierar mellan 1 och 100. |
| Typ av benägenhet | Den valda benägenhetstypen. |
| Resultatdatum | Det datum som poängsättningen inträffade. |
| Influensafaktorer | Förväntade orsaker till varför en profil kan konverteras eller försvinna. Faktorer består av följande attribut:<ul><li>Kod: Profilen eller beteendeattributet som positivt påverkar en profils förväntade poäng. </li><li>Värde: Värdet på profilen eller beteendeattributet.</li><li>Prioritet: Anger hur viktig profilen eller beteendeattributet är för det förväntade poängvärdet (låg, medel, hög)</li></ul> |

## Nästa steg {#next-steps}

När du har förberett dina data och har alla dina autentiseringsuppgifter och scheman på plats börjar du med att följa guiden [Konfigurera en AI-instans](./user-guide/configure.md) . Den här guiden hjälper dig att skapa en instans för kundens AI.