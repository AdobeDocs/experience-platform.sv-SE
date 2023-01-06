---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mappning;data prep;data preparing;preparing data;
solution: Experience Platform
title: Hantera dataformat med Data Prep
description: Det här dokumentet ger en översikt över hur olika datatyper hanteras i Data Prep.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 12%

---

# Hantera dataformat med Data Prep

Data Prep kan hantera olika dataformat som importerats till Adobe Experience Platform på ett robust sätt. Det här dokumentet visar hur olika dataformat behandlas med Data Prep.

## Booleans {#booleans}

Om källtypen är en sträng och måltypen är en boolesk typ kan Data Prep automatiskt tolka värdet och konvertera källvärdet till ett booleskt värde.

Värdena `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true`och `TRUE` tolkas automatiskt för att `true`.

Värdena `n`, `N`, `no`, `NO`, `off`, `OFF`, `false`och `FALSE` tolkas automatiskt för att `false`.

## Datum {#dates}

Data Prep stöder datumfunktioner, både som strängar och som datetime-objekt.

### Format för datumfunktion

Datumfunktionen konverterar strängar och datetime-objekt till ett ISO 8601-formaterat ZonedDateTime-objekt.

**Format**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATE}` | Obligatoriskt. Strängen som representerar datumet. |
| `{FORMAT}` | Valfritt. Strängen som representerar formatet för källdatumet. Mer information om strängformatering finns i [strängavsnitt för datum-/tidsformat](#format). |
| `{DEFAULT_DATE}` | Valfritt. Standarddatumet som ska returneras om det angivna datumet är null. |

Uttrycket `date(orderDate, "yyyy-MM-dd")` konverterar `orderDate` värdet &quot;December 31st, 2020&quot; till datetime-värdet &quot;2020-12-31&quot;.

### Konvertering av datumfunktion

När strängfält från inkommande data mappas till datumfält i scheman med hjälp av Experience Data Model (XDM) bör datumformatet uttryckligen nämnas. Om det inte uttryckligen anges försöker Data Prep konvertera indata genom att matcha dem med följande format. När ett matchande format hittas slutar det att utvärdera eventuella efterföljande format.

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> Data Prep försöker konvertera strängar till datum så gott som möjligt. Dessa konverteringar kan dock ge oönskade resultat. Strängvärdet &quot;12112020&quot; matchar mönstret &quot;MMyyyy&quot;, men användaren kan ha tänkt att datumet ska läsas med mönstret &quot;ddMMyyyy&quot;. Därför bör användare uttryckligen ange datumformatet för strängar.

### Formatsträngar för datum/tid {#format}

Tabellen nedan visar vilka mönsterbokstäver som är definierade för formatsträngar. Observera att bokstäverna är skiftlägeskänsliga.

| Symbol | Betydelse | Presentation | Exempel |
| ------ | ------- | ------------ | ------- |
| G | The era | Text | AD; Anno Domini A |
| Y | År, baserat på ISO-veckan | Siffra | 1996; 96 |
| y | År | Siffra | 2004; 04 |
| M/L | Månad på året | Tal/text | 7. 07; juli Juli. J |
| w | Vecka under året | Siffra | 27 |
| W | Vecka i månaden | Siffra | 3 |
| D | Dag på året | Siffra | 189 |
| d | Dag i månaden | Siffra | 10 |
| F | Veckodag i en månad | Siffra | 2 |
| E | Namn på veckodag | Text | tisdag; Tis |
| u | Veckodag, som ett tal. 1 representerar måndag, ..., 7 representerar söndag | Siffra | 1 |
| a | AM/PM-markör | Text | PM |
| H | Timme på dagen (0-23) | Siffra | 0 |
| k | Timme på dagen (1-24) | Siffra | 24 |
|  000 | Timme i AM/PM (0-11) | Siffra | 0 |
| h | Timme i AM/PM (1-12) | Siffra | 12 |
| m | Minut på timmen | Siffra | 38 |
| s | Sekund i minuten | Siffra | 44 |
| S | Millisecond | Siffra | 245 |
| z | Tidszon | Allmän tidszon | Pacific, normaltid; PST, GMT-08.00 |
| Z | Tidszon | RFC 822-tidszon | -0800 |
| X | Tidszon | Tidszon enligt ISO 8601 | -08; -0800; -08:00 |
| V | Tidszon-ID | Text | America/Los_Angeles |
| O | Tidszonsförskjutning | Text | GMT+8 |
| Q/q | Kvartal på året | Tal/text | 3. 03, Q3; 3:e kvartalet |

## Kartor {#maps}

Kartor stöds för närvarande inte i [!DNL Data Prep].
