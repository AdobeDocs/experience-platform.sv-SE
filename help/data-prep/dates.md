---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mappning;date;date functions;dates;
solution: Experience Platform
title: Datumfunktioner
topic: overview
description: I det här dokumentet introduceras de datumfunktioner som används med Data Prep.
translation-type: tm+mt
source-git-commit: 28c13101be37c5c7680c5d46005509bfd122018f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 16%

---


# Datumfunktioner

Data Prep stöder datumfunktioner, både som strängar och som datetime-objekt.

## Konvertering av datumfunktion

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

## Formatsträngar för datum/tid

Tabellen nedan visar vilka mönsterbokstäver som är definierade för formatsträngar. Observera att bokstäverna är skiftlägeskänsliga.

| Symbol | Betydelse | Presentation | Exempel |
| ------ | ------- | ------------ | ------- |
| G | The era | Text | AD; Anno Domini A |
| Y | År, baserat på ISO-veckan | Siffra | 1996, 96 |
| y | År | Siffra | 2004, 04 |
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
| K | Timme i AM/PM (0-11) | Siffra | 0 |
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

**Exempel**

Uttrycket `date(orderDate, "yyyy-MM-dd")` konverterar `orderDate`-värdet &quot;December 31st, 2020&quot; till datetime-värdet &quot;2020-12-31&quot;.