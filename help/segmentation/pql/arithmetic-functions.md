---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profile Query Language;aritmetiska funktioner;aritmetisk;
solution: Experience Platform
title: PAL - aritmetiska funktioner
topic-legacy: developer guide
description: Aritmetiska funktioner används för att utföra grundläggande beräkningar på värden i PQL (Profile Query Language).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 2%

---

# Aritmetiska funktioner

Aritmetiska funktioner används för att utföra grundläggande beräkningar på värden i [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

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

Nu när du har lärt dig om aritmetiska funktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [översikten över profilfrågespråk](./overview.md).
