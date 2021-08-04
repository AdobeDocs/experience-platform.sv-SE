---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;felsökningsguide;faq;felsökning;
solution: Experience Platform
title: Felsökningsguide för frågetjänst
topic-legacy: troubleshooting
description: Det här dokumentet innehåller information om vanliga felkoder som du stöter på och möjliga orsaker.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 2b118228473a5f07ab7e2c744b799f33a4c44c98
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 5%

---

# [!DNL Query Service] felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om frågetjänsten och en lista med vanliga felkoder när frågetjänsten används. För frågor och felsökning som rör andra tjänster i Adobe Experience Platform, se [felsökningsguiden för Experience Platform](../landing/troubleshooting.md).

## Frågor och svar

Nedan följer en lista med svar på vanliga frågor om frågetjänsten.

### Hur hämtar jag bara metadata för en fråga?

Om du bara vill hämta metadata för en fråga kan du köra en fråga som returnerar noll rader enligt följande:

```sql
SELECT * FROM <table> WHERE 1=0
```

Den här frågan returnerar bara metadata för den angivna tabellen.

### Hur itererar jag snabbt på en CTAS-fråga (Skapa tabell som markerad) utan att materialisera den?

Du kan skapa tillfälliga tabeller för att snabbt iterera och experimentera med en fråga innan den materialiseras för användning. Du kan också använda temporära tabeller för att validera om en fråga fungerar.

Du kan till exempel skapa en tillfällig tabell:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Sedan kan du använda den temporära tabellen enligt följande:

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

### Hur ska jag filtrera mina tidsseriedata?

När du frågar med tidsseriedata bör du använda tidsstämpelfiltret när det är möjligt för att få en mer korrekt analys.

Ett exempel på hur du använder tidsstämpelfiltret visas nedan:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### Ska jag använda jokertecken, till exempel *, för att hämta alla rader från mina datamängder?

Du kan inte använda jokertecken för att hämta alla data från raderna, eftersom frågetjänsten ska behandlas som ett **columnnar-store**-system i stället för som ett vanligt radbaserat lagringssystem.

## REST API-fel

| HTTP-statuskod | Beskrivning | Möjliga orsaker |
| ---------------- | ----------- | --------------- |
| 400 | Felaktig begäran | Felaktig eller ogiltig fråga |
| 401 | Autentiseringen misslyckades | Ogiltig autentiseringstoken |
| 500 | Internt serverfel | Internt systemfel |

## PostgreSQL API-fel

| Felkod | Anslutningstillstånd | Beskrivning | Möjlig orsak |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | Ej tillämpligt | Meddelandetypen stöds inte | Meddelandetypen stöds inte |
| **28P01** | Start - autentisering | Ogiltigt lösenord | Ogiltig autentiseringstoken |
| **28000** | Start - autentisering | Ogiltig auktoriseringstyp | Ogiltig auktoriseringstyp. Måste vara `AuthenticationCleartextPassword`. |
| **42P12** | Start - autentisering | Inga tabeller hittades | Inga tabeller hittades för användning |
| **42601** | Fråga | Syntaxfel | Ogiltigt kommando eller syntaxfel |
| **42P01** | Fråga | Tabellen hittades inte | Det gick inte att hitta tabellen som angavs i frågan |
| **42P07** | Fråga | Tabellen finns | Det finns redan en tabell med samma namn (CREATE TABLE) |
| **53400** | Fråga | LIMIT överskrider maxvärdet | Användaren angav en LIMIT-sats som är högre än 100 000 |
| **53400** | Fråga | Tidsgräns för instruktion | Den inskickade livebeskrivningen tog mer än maximalt 10 minuter |
| **58000** | Fråga | Systemfel | Internt systemfel |
| **0A000** | Fråga/kommando | Stöds inte | Funktionen/funktionen i frågan/kommandot stöds inte |
| **42501** | DROP TABLE Query | Släpptabellen har inte skapats av frågetjänsten | Tabellen som tas bort skapades inte av frågetjänsten med `CREATE TABLE`-satsen |
| **42501** | DROP TABLE Query | Tabellen har inte skapats av den autentiserade användaren | Tabellen som tas bort skapades inte av den inloggade användaren |
| **42P01** | DROP TABLE Query | Tabellen hittades inte | Det gick inte att hitta tabellen som angavs i frågan |
| **42P12** | DROP TABLE Query | Ingen tabell hittades för `dbName`: kontrollera `dbName` | Inga tabeller hittades i den aktuella databasen |
