---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aritmetiska funktioner
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---


# Aritmetiska funktioner

Aritmetiska funktioner används för att utföra grundläggande beräkningar av värden i [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i översikten [för](./overview.md)profilfrågespråk.

## Lägg till

Funktionen `+` (addition) används för att hitta summan av två argumentuttryck.

**Format**

```sql
{NUMBER} + {NUMBER}
```

**Exempel**

Följande PQL-fråga summerar priset för två olika produkter.

```sql
product1.price + product2.price
```

## Multiplicera

Funktionen `*` (multiplikation) används för att hitta produkten av två argumentuttryck.

**Format**

```sql
{NUMBER} * {NUMBER}
```

**Exempel**

Följande PQL-fråga hittar produkten i lagret och priset på en produkt för att hitta produktens bruttovärde.

```sql
product.inventory * product.price
```

## Subtrahera

Funktionen `-` (subtraktion) används för att hitta skillnaden mellan två argumentuttryck.

**Format**

```sql
{NUMBER} - {NUMBER}
```

**Exempel**

Följande PQL-fråga hittar prisskillnaden mellan två olika produkter.

```sql
product1.price - product2.price
```

## Dela

Funktionen `/` (division) används för att hitta kvoten mellan två argumentuttryck.

**Format**

```sql
{NUMBER} / {NUMBER}
```

**Exempel**

I följande PQL-fråga hittas kvoten mellan den totala sålda produkten och den totala intjänade kostnaden för att se den genomsnittliga kostnaden per artikel.

```sql
totalProduct.price / totalProduct.sold
```

## Återstående

Funktionen `%` (modulo/rest) används för att hitta resten efter att de två argumentuttrycken har delats.

**Format**

```sql
{NUMBER} % {NUMBER}
```

**Exempel**

Följande PQL-fråga kontrollerar om personens ålder är delbar med fem.

```sql
person.age % 5 = 0
```

## Nästa steg

Nu när du har lärt dig om aritmetiska funktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.
