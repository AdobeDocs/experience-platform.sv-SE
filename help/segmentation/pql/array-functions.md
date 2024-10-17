---
solution: Experience Platform
title: Array-, List- och Set PQL-funktioner
description: Profile Query Language (PQL) har funktioner som gör det enklare att interagera med arrayer, listor och strängar.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Array-, list- och set-funktioner

[!DNL Profile Query Language] (PQL) erbjuder funktioner som gör det enklare att interagera med arrayer, listor och strängar. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## I

Funktionen `in` används för att avgöra om ett objekt är medlem i en matris eller lista som ett booleskt värde.

**Format**

```sql
{VALUE} in {ARRAY}
```

**Exempel**

Följande PQL-fråga definierar personer med födelsedagar i mars, juni eller september.

```sql
person.birthMonth in [3, 6, 9]
```

## Inte i

Funktionen `notIn` används för att avgöra om ett objekt inte är medlem i en matris eller lista som booleskt värde.

>[!NOTE]
>
>`notIn`-funktionen *ser också* till att inget av värdena är lika med null. Resultatet är därför inte en exakt negation av funktionen `in`.

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**Exempel**

Följande PQL-fråga definierar personer med födelsedagar som inte infaller i mars, juni eller september.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Överlappningar

Funktionen `intersects` används för att avgöra om två arrayer eller listor har minst en gemensam medlem som boolesk.

**Format**

```sql
{ARRAY}.intersects({ARRAY})
```

**Exempel**

Följande PQL-fråga definierar personer vars favoritfärger innehåller minst en röd, blå eller grön färg.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Skärningspunkt

Funktionen `intersection` används för att bestämma de gemensamma medlemmarna i två arrayer eller listor som en lista.

**Format**

```sql
{ARRAY}.intersection({ARRAY})
```

**Exempel**

Följande PQL-fråga definierar om person 1 och person 2 båda har favoritfärgerna rött, blått och grönt.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Delmängd av

Funktionen `subsetOf` används för att avgöra om en viss array (array A) är en delmängd av en annan array (array B). Det vill säga att alla element i array A är element i array B som booleska.

**Format**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Exempel**

Följande PQL-fråga definierar personer som har besökt alla sina favoritstäder.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Supermängd till

Funktionen `supersetOf` används för att avgöra om en viss array (array A) är en överordnad mängd till en annan array (array B). Arrayen A innehåller alltså alla element i array B som booleska.

**Format**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Exempel**

Följande PQL-fråga definierar personer som har ätit sushi och pizza minst en gång.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Inkluderar

Funktionen `includes` används för att avgöra om en array eller lista innehåller ett givet objekt som ett booleskt värde.

**Format**

```sql
{ARRAY}.includes({ITEM})
```

**Exempel**

Följande PQL-fråga definierar personer vars favoritfärg är röd.

```sql
person.favoriteColors.includes("red")
```

## Distinkt

Funktionen `distinct` används för att ta bort dubblettvärden från en array eller lista som en array.

**Format**

```sql
{ARRAY}.distinct()
```

**Exempel**

Följande PQL-fråga anger personer som har lagt order i mer än en butik.

```sql
person.orders.storeId.distinct().count() > 1
```

## Gruppera efter

Funktionen `groupBy` används för att partitionera värden för en matris eller lista i en grupp baserat på värdet för uttrycket som en mappning från unika värden för grupperingsuttrycket till matriser som är partitioner av värdet för matrisuttrycket.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{ARRAY}` | Arrayen eller listan som ska grupperas. |
| `{EXPRESSION}` | Ett uttryck som mappar varje objekt i arrayen eller listan returneras. |

**Exempel**

Följande PQL-fråga grupperar alla order som lagrar ordern på.

```sql
xEvent[type="order"].groupBy(storeId)
```

## Filter

Funktionen `filter` används för att filtrera en array eller lista baserat på ett uttryck som en array eller lista, beroende på indata.

**Format**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{ARRAY}` | Arrayen eller listan som ska filtreras. |
| `{EXPRESSION}` | Ett uttryck att filtrera efter. |

**Exempel**

Följande PQL-fråga definierar alla personer som är 21 eller äldre.

```sql
person.filter(age >= 21)
```

## Karta

Funktionen `map` används för att skapa en ny array genom att tillämpa ett uttryck på varje objekt i en given array som en array.

**Format**

```sql
array.map(expression)
```

**Exempel**

Följande PQL-fråga skapar en ny array med siffror och fyrkantiger värdet för de ursprungliga talen.

```sql
numbers.map(square)
```

## Första `n` i matris {#first-n}

Funktionen `topN` används för att returnera de första `N` objekten i en array, sorterade i stigande ordning baserat på det angivna numeriska uttrycket som en array.

**Format**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{ARRAY}` | Den array eller lista som ska sorteras. |
| `{VALUE}` | Den egenskap som arrayen eller listan ska sorteras i. |
| `{AMOUNT}` | Antalet artiklar som ska returneras. |

**Exempel**

Följande PQL-fråga returnerar de fem främsta beställningarna med det högsta priset.

```sql
orders.topN(price, 5)
```

## Senaste `n` i matris

Funktionen `bottomN` används för att returnera de sista `N` objekten i en array, sorterade i stigande ordning baserat på det angivna numeriska uttrycket som en array.

**Format**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Beskrivning |
| --------- | ----------- | 
| `{ARRAY}` | Den array eller lista som ska sorteras. |
| `{VALUE}` | Den egenskap som arrayen eller listan ska sorteras i. |
| `{AMOUNT}` | Antalet artiklar som ska returneras. |

**Exempel**

Följande PQL-fråga returnerar de fem främsta beställningarna med det lägsta priset.

```sql
orders.bottomN(price, 5)
```

## Första objektet

Funktionen `head` används för att returnera det första objektet i arrayen eller listan som ett objekt.

**Format**

```sql
{ARRAY}.head()
```

**Exempel**

Följande PQL-fråga returnerar den första av de fem främsta beställningarna med det högsta priset. Mer information om funktionen `topN` finns i avsnittet [first `n` i array](#first-n).

```sql
orders.topN(price, 5).head()
```

## Nästa steg

Nu när du har lärt dig mer om arrayer, listor och inställningsfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profile Query Language-översikten](./overview.md).
