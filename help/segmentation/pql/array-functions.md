---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;array functions;array;
solution: Experience Platform
title: Array-, list- och set-funktioner
topic: developer guide
description: PQL (Profile Query Language) har funktioner som underlättar interaktion med arrayer, listor och strängar.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 3%

---


# Array-, list- och set-funktioner

[!DNL Profile Query Language] (PQL) har funktioner som underlättar interaktion med arrayer, listor och strängar. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## I

Funktionen används `in` för att avgöra om ett objekt är medlem i en array eller lista.

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

Funktionen används `notIn` för att avgöra om ett objekt inte är medlem i en array eller lista.

>[!NOTE]
>
>Funktionen `notIn` ser *också* till att inget av värdena är lika med null. Resultatet är därför inte en exakt negation av `in` funktionen.

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**Exempel**

Följande PQL-fråga definierar personer med födelsedagar som inte är i mars, juni eller september.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Överlappningar

Funktionen används `intersects` för att avgöra om två arrayer eller listor har minst en gemensam medlem.

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

Funktionen används `intersection` för att bestämma de gemensamma medlemmarna i två arrayer eller listor.

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

Funktionen används för att avgöra om en viss array (array A) är en delmängd av en annan array (array B). `subsetOf` Det vill säga att alla element i array A är element i array B.

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

Funktionen används för att avgöra om en viss array (array A) är en överordnad mängd till en annan array (array B). `supersetOf` Arrayen A innehåller alltså alla element i array B.

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

Funktionen används `includes` för att avgöra om en array eller lista innehåller ett visst objekt.

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

Funktionen används `distinct` för att ta bort dubblettvärden från en array eller lista.

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

Funktionen används `groupBy` för att partitionera värden för en array eller lista i en grupp baserat på uttryckets värde.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{ARRAY}` | Arrayen eller listan som ska grupperas. |
| `{EXPRESSION}` | Ett uttryck som mappar varje objekt i arrayen eller listan returneras. |

**Exempel**

Följande PQL-fråga grupperar alla order som lagrar ordern på.

```sql
orders.groupBy(storeId)
```

## Filter

Funktionen används `filter` för att filtrera en array eller lista baserat på ett uttryck.

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

## Mappa

Funktionen används `map` för att skapa en ny array genom att tillämpa ett uttryck på varje objekt i en given array.

**Format**

```sql
array.map(expression)
```

**Exempel**

I följande PQL-fråga skapas en ny array med siffror och värdet för de ursprungliga talen fyrkantigt.

```sql
numbers.map(square)
```

## Först `n` i matris {#first-n}

Funktionen används `topN` för att returnera de första `N` objekten i en array, sorterade i stigande ordning baserat på det givna numeriska uttrycket.

**Format**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{ARRAY}` | Arrayen eller listan som ska sorteras. |
| `{VALUE}` | Den egenskap som arrayen eller listan ska sorteras i. |
| `{AMOUNT}` | Antalet artiklar som ska returneras. |

**Exempel**

Följande PQL-fråga returnerar de fem översta beställningarna med det högsta priset.

```sql
orders.topN(price, 5)
```

## Sista `n` i matris

Funktionen används `bottomN` för att returnera de sista `N` objekten i en array, sorterade i stigande ordning baserat på det givna numeriska uttrycket.

**Format**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Beskrivning |
| --------- | ----------- | 
| `{ARRAY}` | Arrayen eller listan som ska sorteras. |
| `{VALUE}` | Den egenskap som arrayen eller listan ska sorteras i. |
| `{AMOUNT}` | Antalet artiklar som ska returneras. |

**Exempel**

Följande PQL-fråga returnerar de fem översta beställningarna med det lägsta priset.

```sql
orders.bottomN(price, 5)
```

## Första objektet

Funktionen används `head` för att returnera det första objektet i arrayen eller listan.

**Format**

```sql
{ARRAY}.head()
```

**Exempel**

Följande PQL-fråga returnerar den första av de fem främsta beställningarna med det högsta priset. Mer information om `topN` funktionen finns i den [första `n` i arrayavsnittet](#first-n) .

```sql
orders.topN(price, 5).head()
```

## Nästa steg

Nu när du har lärt dig mer om arrayer, listor och inställningsfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.
