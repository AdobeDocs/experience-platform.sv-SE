---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sammanställningsfunktioner
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 3%

---


# Sammanställningsfunktioner

Sammanställningsfunktioner används för att gruppera flera värden inom [!DNL Profile Query Language] PQL-arrayer för att skapa ett enda sammanfattningsvärde. Mer information om andra PQL-funktioner finns i översikten [för](./overview.md)profilfrågespråk.

## Antal

Funktionen `count` returnerar antalet element i den angivna arrayen.

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

Funktionen `sum` returnerar summan av alla markerade värden i arrayen.

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

Funktionen returnerar det aritmetiska medelvärdet av alla markerade värden i arrayen. `average`

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

Funktionen `min` returnerar det minsta av alla markerade värden i arrayen.

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

Funktionen `max` returnerar det största av alla markerade värden i arrayen.

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

Nu när du har lärt dig om sammanställningsfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.
