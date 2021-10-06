---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;felsökningsguide;faq;felsökning;
solution: Experience Platform
title: Felsökningsguide för frågetjänst
topic-legacy: troubleshooting
description: Det här dokumentet innehåller information om vanliga felkoder som du stöter på och möjliga orsaker.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 42288ae7db6fb19bc0a0ee8e4ecfa50b7d63d017
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 4%

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

>[!NOTE]
>
> Datumsträngen **måste** ha formatet `yyyy-mm-ddTHH24:MM:SS`.

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

### Ska jag använda `NOT IN` i min SQL-fråga?

Operatorn `NOT IN` används ofta för att hämta rader som inte finns i en annan tabell eller SQL-sats. Operatorn kan göra prestandan långsammare och kan returnera oväntade resultat om kolumnerna som jämförs accepterar `NOT NULL` eller om du har ett stort antal poster.

I stället för att använda `NOT IN` kan du använda antingen `NOT EXISTS` eller `LEFT OUTER JOIN`.

Om du till exempel har skapat följande tabeller:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Om du använder operatorn `NOT EXISTS` kan du replikera med operatorn `NOT IN` med följande fråga:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Om du använder operatorn `LEFT OUTER JOIN` kan du replikera med operatorn `NOT IN` med följande fråga:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### Hur används operatorerna `OR` och `UNION` korrekt?

### Hur använder jag operatorn `CAST` för att konvertera mina tidsstämplar i SQL-frågor?

När du använder operatorn `CAST` för att konvertera en tidsstämpel måste du ta med både datumet **och** tid.

Om du till exempel saknar tidskomponenten, som visas nedan, uppstår ett fel:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

En korrekt användning av operatorn `CAST` visas nedan:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

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
