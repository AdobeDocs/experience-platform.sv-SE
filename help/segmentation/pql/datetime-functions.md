---
solution: Experience Platform
title: Datum- och tidsfunktioner för PQL
description: Datum- och tidsfunktioner används för att utföra datum- och tidsåtgärder på värden inom PQL (Profile Query Language).
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---

# Datum- och tidsfunktioner

Datum- och tidsfunktioner används för att utföra datum- och tidsåtgärder på värden inom [!DNL Profile Query Language] (PQL). Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikt](./overview.md).

## Aktuell månad

The `currentMonth` funktionen returnerar den aktuella månaden som ett heltal.

**Format**

```sql
currentMonth()
```

**Exempel**

Följande PQL-fråga kontrollerar om personens födelsemånad är den aktuella månaden.

```sql
person.birthMonth = currentMonth()
```

## Få månad

The `getMonth` returnerar månaden som ett heltal baserat på en viss tidsstämpel.

**Format**

```sql
{TIMESTAMP}.getMonth()
```

**Exempel**

Följande PQL-fråga kontrollerar om personens födelsemånad är i juni.

```sql
person.birthdate.getMonth() = 6
```

## Aktuellt år

The `currentYear` funktionen returnerar det aktuella året som ett heltal.

**Format**

```sql
currentYear()
```

**Exempel**

Följande PQL-fråga kontrollerar om produkten har sålts det aktuella året.

```sql
product.saleYear = currentYear()
```

## Skaffa år

The `getYear` funktionen returnerar året som ett heltal baserat på en viss tidsstämpel.

**Format**

```sql
{TIMESTAMP}.getYear()
```

**Exempel**

Följande PQL-fråga kontrollerar om personens födelseår infaller 1991, 1992, 1993, 1994 eller 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Aktuell dag i månaden

The `currentDayOfMonth` funktionen returnerar den aktuella dagen i månaden som ett heltal.

**Format**

```sql
currentDayOfMonth()
```

**Exempel**

Följande PQL-fråga kontrollerar om personens födelsedag matchar den aktuella dagen i månaden.

```sql
person.birthDay = currentDayOfMonth()
```

## Hämta dag i månaden

The `getDayOfMonth` funktionen returnerar dagen som ett heltal baserat på en given tidsstämpel.

**Format**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Exempel**

Följande PQL-fråga kontrollerar om artikeln har sålts inom de första 15 dagarna i månaden.

```sql
product.sale.getDayOfMonth() <= 15
```

## Inträffar

The `occurs` funktionen jämför den angivna tidsstämpelfunktionen med en fast tidsperiod.

**Format**

The `occurs` kan skrivas med något av följande format:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argument | Beskrivning |
| --------- | ----------- |
| `{COMPARISON}` | En jämförelseoperator. Kan vara någon av följande operatorer: `>`, `>=`, `<`, `<=`, `=`, `!=`. Mer information om jämförelsefunktionerna finns i [jämförelsefunktionsdokument](./comparison-functions.md). |
| `{INTEGER}` | Ett positivt heltal. |
| `{TIME_UNIT}` | En tidsenhet. Kan vara något av följande ord: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | En preposition som beskriver när datumet ska jämföras med. Kan vara något av följande ord: `before`, `after`, `from`. |
| `{TIME}` | Kan vara en tidsstämpellitteral (`today`, `now`, `yesterday`, `tomorrow`), en relativ tidsenhet (en av `this`, `last`, eller `next` följt av en tidsenhet) eller ett tidsstämpelattribut. |

>[!NOTE]
>
>Användning av ordet `on` är valfritt. Det finns för att förbättra läsbarheten för vissa kombinationer, som `timestamp occurs on date(2019,12,31)`.

**Exempel**

Följande PQL-fråga kontrollerar om artikeln såldes förra veckan.

```sql
product.saleDate occurs last week
```

Följande PQL-fråga kontrollerar om ett objekt har sålts mellan 8 januari 2015 och 1 juli 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Nu

`now` är ett reserverat ord som representerar tidsstämpeln för PQL-körningen.

**Exempel**

Följande PQL-fråga kontrollerar om en artikel har sålts exakt tre timmar tidigare.

```sql
product.saleDate occurs = 3 hours before now
```

## Idag

`today` är ett reserverat ord som representerar tidsstämpeln för början av dagen för PQL-körningen.

**Exempel**

Följande PQL-fråga kontrollerar om en persons födelsedag var för tre dagar sedan.

```sql
person.birthday occurs = 3 days before today
```

## Nästa steg

Nu när du har lärt dig om datum- och tidsfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profilfrågespråk - översikt](./overview.md).
