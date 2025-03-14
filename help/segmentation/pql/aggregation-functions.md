---
solution: Experience Platform
title: PQL aggregeringsfunktioner
description: Sammanställningsfunktioner används för att gruppera flera värden inom Profile Query Language (PQL)-arrayer för att skapa ett enda sammanfattningsvärde.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Sammanställningsfunktioner

Sammanställningsfunktioner används för att gruppera flera värden inom [!DNL Profile Query Language] (PQL)-arrayer för att skapa ett enda sammanfattningsvärde. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Antal

Funktionen `count` returnerar antalet element i den angivna arrayen som ett tal.

**Format**

```sql
{ARRAY}.count()
```

**Exempel**

Följande PQL-fråga returnerar antalet order i arrayen.

```sql
orders.count()
```

## Summa

Funktionen `sum` returnerar summan av alla markerade värden i arrayen som ett tal.

**Format**

```sql
{ARRAY}.sum()
```

**Exempel**

Följande PQL-fråga returnerar summan av alla orderpriser.

```sql
orders.sum(order.price)
```

## Genomsnittlig

Funktionen `average` returnerar det aritmetiska medelvärdet av alla markerade värden i arrayen som ett tal.

**Format**

```sql
{ARRAY}.average()
```

**Exempel**

Följande PQL-fråga returnerar genomsnittspriset för alla order.

```sql
orders.average(order.price)
```

## Minimum

Funktionen `min` returnerar det minsta av alla markerade värden i arrayen som ett tal.

**Format**

```sql
{ARRAY}.min()
```

**Exempel**

Följande PQL-fråga returnerar det lägsta priset för alla order.

```sql
orders.min(order.price)
```

## Maximal

Funktionen `max` returnerar det största av alla markerade värden i arrayen som ett tal.

**Format**

```sql
{ARRAY}.max()
```

**Exempel**

Följande PQL-fråga returnerar det högsta priset för alla order.

```sql
orders.max(order.price)
```

## Nästa steg

Nu när du har lärt dig mer om sammanställningsfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profile Query Language-översikten](./overview.md).
