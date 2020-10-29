---
keywords: Experience Platform;getting started;customer ai;popular topics;customer ai input;customer ai output
solution: Experience Platform
title: Indata och utdata för AI
topic: Getting started
description: Följande dokument visar de olika in- och utdata som används i kundens AI.
translation-type: tm+mt
source-git-commit: 0f45f12ca4f43de9489eb609fd541aa2be3bae78
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# Indata och utdata för AI

Följande dokument visar de olika in- och utdata som används i kundens AI.

## AI-indata för kund

Kunds-AI använder data från kundupplevelsehändelser för att beräkna benägenhetspoängen. Mer information om konsumentupplevelsehändelser finns i [Förbered data för användning i dokumentationen](../data-preparation.md)för intelligenta tjänster.

### Historiska data

Kundens AI kräver historiska data för modellutbildning, men mängden data som krävs baseras på två nyckelelement: resultatfönstret och den berättigade populationen.

Som standard söker AI efter en användare att ha haft aktivitet de senaste 120 dagarna om ingen tillämplig populationsdefinition anges under programkonfigurationen. Dessutom kräver kundens AI minst 500 kvalificerande och 500 icke-kvalificerande händelser (totalt 1 000) av historiska data baserat på en förutsedd måldefinition.

I följande exempel används en enkel formel som hjälper dig att fastställa den minsta mängden data som krävs. Om du har mer än minimikraven är det troligt att modellen ger mer korrekta resultat. Om du har mindre än minimiantalet som krävs kommer modellen att misslyckas eftersom det inte finns tillräckligt med data för modellutbildning.

**Formel**:

Minsta längd på de data som krävs = stödberättigande population + resultatfönster

>[!NOTE]
>
> 30 är det minsta antal dagar som krävs för en stödberättigad population. Om detta inte anges är standardinställningen 120 dagar.

Exempel :

- Ni vill förutsäga om kunden sannolikt kommer att köpa en klocka inom 30 dagar. Du vill även göra poäng för användare som har viss webbaktivitet de senaste 60 dagarna. I det här fallet är den minsta tillåtna längden på de data som krävs = 60 dagar + 30 dagar. Den stödberättigade populationen är 60 dagar och resultatfönstret är 30 dagar, totalt 90 dagar.

- Du vill förutsäga om användaren sannolikt kommer att köpa en klocka inom de kommande 7 dagarna. I det här fallet är den minsta längden på de data som krävs = 120 dagar + 7 dagar. Den giltiga populationen är som standard 120 dagar och resultatfönstret är 7 dagar, totalt 127 dagar.

- Ni vill förutsäga om kunden sannolikt kommer att köpa en klocka inom de kommande 7 dagarna. Du vill även göra poäng för användare som har viss webbaktivitet de senaste 7 dagarna. I det här fallet är den minsta längden på de data som krävs = 30 dagar + 7 dagar. Den stödberättigade populationen kräver minst 30 dagar och resultatfönstret är 7 dagar, totalt 37 dagar.

Förutom de minsta data som krävs fungerar kundens AI också bäst med aktuella data. I det här fallet gör kundens AI en förutsägelse för framtiden baserat på användarens senaste beteendedata. Med andra ord är det troligt att nyare data ger en mer korrekt förutsägelse.

## Kundens AI-utdata

Kund-AI genererar flera attribut för enskilda profiler som anses berättigade. Det finns två sätt att använda poängen baserat på vad du har etablerat. Om du har aktiverat kundprofil i realtid för din datauppsättning kan du använda den via kundprofilen i realtid. Om du inte har någon kundprofil i realtid kan du hämta den kunds-AI-utdatauppsättning som finns tillgänglig i datasjön.

>[!NOTE]
>
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