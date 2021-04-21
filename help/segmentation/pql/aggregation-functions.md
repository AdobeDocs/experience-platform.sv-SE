---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profilfrågespråk;aggregeringsfunktioner;aggregering;
solution: Experience Platform
title: PQL-aggregeringsfunktioner
topic-legacy: developer guide
description: Sammanställningsfunktioner används för att gruppera flera värden inom PQL-arrayer (Profile Query Language) för att skapa ett enda sammanfattningsvärde.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 3%

---

# Sammanställningsfunktioner

Sammanställningsfunktioner används för att gruppera flera värden inom [!DNL Profile Query Language]-arrayer (PQL) för att skapa ett enda sammanfattningsvärde. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

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

Funktionen `average` returnerar det aritmetiska medelvärdet för alla markerade värden i arrayen.

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

Nu när du har lärt dig om sammanställningsfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [översikten över profilfrågespråk](./overview.md).
