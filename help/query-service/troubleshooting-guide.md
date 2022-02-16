---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;felsökningsguide;faq;felsökning;
solution: Experience Platform
title: Felsökningsguide för frågetjänst
topic-legacy: troubleshooting
description: Det här dokumentet innehåller information om vanliga felkoder som du stöter på och möjliga orsaker.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 03cd013e35872bcc30c68508d9418cb888d9e260
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 2%

---

# [!DNL Query Service] felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om frågetjänsten och en lista med vanliga felkoder när frågetjänsten används. För frågor och felsökning som rör andra tjänster i Adobe Experience Platform, se [Felsökningsguide för Experience Platform](../landing/troubleshooting.md).

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

### Hur ändrar jag tidszonen till och från en UTC-tidsstämpel?

Adobe Experience Platform innehåller data i UTC-format (Coordinated Universal Time) för tidsstämpling. Ett exempel på UTC-formatet är `2021-12-22T19:52:05Z`

Frågetjänsten stöder inbyggda SQL-funktioner för konvertering av en viss tidsstämpel till och från UTC-format. Båda `to_utc_timestamp()` och `from_utc_timestamp()` metoder har två parametrar: tidsstämpel och tidszon.

| Parameter | Beskrivning |
|---|---|
| Tidsstämpel | Tidsstämpeln kan skrivas antingen i UTC-format eller enkelt `{year-month-day}` format. Om ingen tid anges är standardvärdet midnatt på morgonen den angivna dagen. |
| Tidszon | Tidszonen skrivs i en `{continent/city})` format. Det måste vara en av de erkända tidszonskoderna som finns i [TZ-databas för offentlig domän](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Konvertera till UTC-tidsstämpeln

The `to_utc_timestamp()` -metoden tolkar de givna parametrarna och konverterar dem **till tidsstämpeln i den lokala tidszonen** i UTC-format. Exempelvis är tidszonen i Seoul i Sydkorea UTC/GMT +9 timmar. Genom att ange en tidsstämpel som bara är ett datum, använder metoden standardvärdet midnatt på morgonen. Tidsstämpeln och tidszonen konverteras till UTC-format från tidpunkten i den regionen till en UTC-tidsstämpel för den lokala regionen.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

Frågan returnerar en tidsstämpel i användarens lokala tid. I det här fallet är klockan 16.00 föregående dag som Seoul nio timmar framåt.

```
2021-08-30 15:00:00
```

Som ett annat exempel om den angivna tidsstämpeln var `2021-07-14 12:40:00.0` för `Asia/Seoul` tidszon, skulle den returnerade UTC-tidsstämpeln `2021-07-14 03:40:00.0`

Konsolutdata i gränssnittet för frågetjänsten är ett mer läsbart format:

```
8/30/2021, 3:00 PM
```

### Konvertera från UTC-tidsstämpeln

The `from_utc_timestamp()` method tolkar de givna parametrarna **från tidsstämpeln i den lokala tidszonen** och ger motsvarande tidsstämpel för det önskade området i UTC-format. I exemplet nedan är timmen 2:40 PM i användarens lokala tidszon. Seoul-tidszonen som skickas som en variabel ligger nio timmar före den lokala tidszonen.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

Frågan returnerar en tidsstämpel i UTC-format för den tidszon som skickas som en parameter. Resultatet är nio timmar före den tidszon som körde frågan.

```
8/31/2021, 11:40 PM
```

### Hur ska jag filtrera mina tidsseriedata?

När du frågar med tidsseriedata bör du använda tidsstämpelfiltret när det är möjligt för att få en mer korrekt analys.

>[!NOTE]
>
> Datumsträngen **måste** vara i formatet `yyyy-mm-ddTHH24:MM:SS`.

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

Du kan inte använda jokertecken för att hämta alla data från dina rader, eftersom frågetjänsten ska behandlas som en **columnar-store** i stället för ett vanligt radbaserat lagringssystem.

### Ska jag använda `NOT IN` i min SQL-fråga?

The `NOT IN` används ofta för att hämta rader som inte finns i en annan tabell eller SQL-sats. Operatorn kan göra prestandan långsammare och kan returnera oväntade resultat om kolumnerna som jämförs accepterar `NOT NULL`eller så har du ett stort antal poster.

I stället för att använda `NOT IN`kan du använda antingen `NOT EXISTS` eller `LEFT OUTER JOIN`.

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

Om du använder `NOT EXISTS` kan du replikera med `NOT IN` genom att använda följande fråga:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Om du använder `LEFT OUTER JOIN` -operatorn kan du replikera med `NOT IN` genom att använda följande fråga:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### Vad är rätt användning av `OR` och `UNION` operatorer?

### Hur använder jag `CAST` för att konvertera mina tidsstämplar i SQL-frågor?

När du använder `CAST` om du vill konvertera en tidsstämpel måste du inkludera både datumet och **och** tid.

Om du till exempel saknar tidskomponenten, som visas nedan, uppstår ett fel:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Korrekt användning av `CAST` operatorn visas nedan:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

### Hur hämtar jag mina frågeresultat som en CSV-fil?

Det här är inte en funktion som frågetjänsten erbjuder direkt. Om [!DNL PostgreSQL] klienten som används för att ansluta till databasservern har den funktionen. Svaret på en SELECT-fråga kan skrivas och laddas ned som en CSV-fil. Se dokumentationen för verktyget eller tredjepartsverktyget som du använder för att få mer information om processen.

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
| **42501** | DROP TABLE Query | Släpptabellen har inte skapats av frågetjänsten | Tabellen som tas bort skapades inte av frågetjänsten med `CREATE TABLE` programsats |
| **42501** | DROP TABLE Query | Tabellen har inte skapats av den autentiserade användaren | Tabellen som tas bort skapades inte av den inloggade användaren |
| **42P01** | DROP TABLE Query | Tabellen hittades inte | Det gick inte att hitta tabellen som angavs i frågan |
| **42P12** | DROP TABLE Query | Ingen tabell hittades för `dbName`: kontrollera `dbName` | Inga tabeller hittades i den aktuella databasen |
