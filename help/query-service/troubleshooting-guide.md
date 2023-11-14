---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;felsökningsguide;faq;felsökning;
solution: Experience Platform
title: Vanliga frågor
description: Det här dokumentet innehåller vanliga frågor och svar relaterade till frågetjänsten. Här finns ämnen som export av data, verktyg från tredje part och PSQL-fel.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '4291'
ht-degree: 1%

---

# Frågor och svar

Det här dokumentet innehåller svar på vanliga frågor om frågetjänsten och en lista med vanliga felkoder när frågetjänsten används. För frågor och felsökning som rör andra tjänster i Adobe Experience Platform, se [Felsökningsguide för Experience Platform](../landing/troubleshooting.md).

Följande lista med svar på vanliga frågor är indelad i följande kategorier:

- [Allmänt](#general)
- [Exportera data](#exporting-data)
- [Tredjepartsverktyg](#third-party-tools)
- [PostgreSQL API-fel](#postgresql-api-errors)
- [REST API-fel](#rest-api-errors)

## Allmänna frågor om frågetjänsten {#general}

Det här avsnittet innehåller information om prestanda, begränsningar och processer.

### Kan jag inaktivera funktionen för automatisk komplettering i frågetjänstredigeraren?

+++Svarsnr Redigeraren stöder för närvarande inte att funktionen Komplettera automatiskt stängs av.
+++

### Varför blir Frågeredigeraren ibland långsam när jag skriver en fråga?

+++Svar En möjlig orsak är funktionen för automatisk komplettering. Funktionen bearbetar vissa metadatakommandon som ibland kan göra redigeraren långsammare vid redigering av frågor.
+++

### Kan jag använda [!DNL Postman] för API:t för frågetjänsten?

+++Besvara Ja, du kan visualisera och interagera med alla Adobe API-tjänster med [!DNL Postman] (kostnadsfritt program från tredje part). Titta på [[!DNL Postman] installationsguide](https://video.tv.adobe.com/v/28832) steg-för-steg-instruktioner för hur du konfigurerar ett projekt i Adobe Developer Console och hämtar alla nödvändiga inloggningsuppgifter för användning med [!DNL Postman]. Läs den officiella dokumentationen för [riktlinjer för att starta, köra och dela [!DNL Postman] samlingar](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Finns det någon gräns för hur många rader som får returneras från en fråga via användargränssnittet?

+++Besvara Ja, frågetjänsten tillämpar internt en gräns på 50 000 rader om inte en explicit gräns anges externt. Se vägledningen på [interaktiv frågekörning](./best-practices/writing-queries.md#interactive-query-execution) för mer information.
+++

### Kan jag använda frågor för att uppdatera rader?

+++Svara i gruppfrågor, det går inte att uppdatera en rad i datauppsättningen.
+++

### Finns det någon gräns för datastorlek för resultatet från en fråga?

+++Svarsnr Det finns ingen gräns för datastorlek, men det finns en timeout för frågor på 10 minuter från en interaktiv session. Om frågan körs som en batch-CTAS gäller inte en 10-minuterstimeout. Se vägledningen på [interaktiv frågekörning](./best-practices/writing-queries.md#interactive-query-execution) för mer information.
+++

### Hur åsidosätter jag gränsen för antalet utgående rader i en SELECT-fråga?

+++Svar Om du vill åsidosätta gränsen för utdataraden använder du LIMIT 0 i frågan. Exempel:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### Hur stoppar jag mina frågor från att tajma ut på tio minuter?

+++Besvara En eller flera av följande lösningar rekommenderas vid timeout i frågor.

- [Konvertera frågan till en CTAS-fråga](./sql/syntax.md#create-table-as-select) och schemalägga körningen. Du kan schemalägga en körning antingen [via användargränssnittet](./ui/user-guide.md#scheduled-queries) eller [API](./api/scheduled-queries.md#create).
- Kör frågan i ett mindre datasegment genom att använda ytterligare [filtervillkor](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Kör kommandot EXPLAIN](./sql/syntax.md#explain) för att samla in mer information.
- Granska statistiken för data i datauppsättningen.
- Konvertera frågan till ett förenklat formulär och kör den igen med [förberedda programsatser](./sql/prepared-statements.md).
+++

### Finns det något problem eller någon inverkan på frågetjänstens prestanda om flera frågor körs samtidigt?

+++Svarsnr Frågetjänsten har en autoskalningsfunktion som säkerställer att samtidiga frågor inte har någon märkbar påverkan på tjänstens prestanda.
+++

### Kan jag använda reserverade nyckelord som kolumnnamn?

+++Svar Det finns vissa reserverade nyckelord som inte kan användas som kolumnnamn, till exempel `ORDER`, `GROUP BY`, `WHERE`, `DISTINCT`. Om du vill använda dessa nyckelord måste du undvika dessa kolumner.
+++

### Hur hittar jag ett kolumnnamn från en hierarkisk datauppsättning?

+++Svar Följande steg beskriver hur du visar en tabellvy av en datauppsättning via användargränssnittet, inklusive alla kapslade fält och kolumner i ett förenklat formulär.

- När du har loggat in i Experience Platform väljer du **[!UICONTROL Datasets]** i den vänstra navigeringen i användargränssnittet för att navigera till [!UICONTROL Datasets] kontrollpanel.
- Datamängderna [!UICONTROL Browse] -fliken öppnas. Du kan använda sökfältet för att förfina de tillgängliga alternativen. Välj en datauppsättning i den lista som visas.

![Kontrollpanelen för datauppsättningar i plattformsgränssnittet med sökfältet och en datauppsättning markerad.](./images/troubleshooting/dataset-selection.png)

- The [!UICONTROL Datasets activity] visas. Välj **[!UICONTROL Preview dataset]** om du vill öppna en dialogruta med XDM-schemat och en tabellvy med separerade data från den markerade datauppsättningen. Mer information finns i [förhandsgranska en datauppsättningsdokumentation](../catalog/datasets/user-guide.md#preview-a-dataset)

![Fliken Datauppsättningsaktivitet på kontrollpanelen Datamängder med datamängden Preview markerad.](./images/troubleshooting/dataset-preview.png)

- Markera ett fält i schemat om du vill visa innehållet i en förenklad kolumn. Kolumnens namn visas ovanför innehållet till höger på sidan. Du bör kopiera det här namnet om du vill använda det för att fråga om den här datauppsättningen.

![XDM-schemat och tabellvyn för de separerade data. Kolumnnamnet för en kapslad datauppsättning markeras i användargränssnittet.](./images/troubleshooting/column-name.png)

Se dokumentationen för fullständig vägledning om [arbeta med kapslade datastrukturer](./essential-concepts/nested-data-structures.md) med frågeredigeraren eller en tredjepartsklient.
+++

### Hur snabbar jag upp en fråga i en datauppsättning som innehåller arrayer?

+++Svar Om du vill förbättra prestanda för frågor om datauppsättningar som innehåller arrayer bör du [utnyttja arrayen](https://spark.apache.org/docs/latest/api/sql/index.html#explode) som [CTAS-fråga](./sql/syntax.md#create-table-as-select) i runtime och utforska den för att hitta möjligheter att förbättra bearbetningstiden.
+++

### Varför bearbetas min CTAS-fråga fortfarande efter många timmar för ett litet antal rader?

+++Svar Om frågan har tagit lång tid på en mycket liten datauppsättning kontaktar du kundsupport.

Det kan finnas många orsaker till att en fråga har fastnat under bearbetningen. För att fastställa den exakta orsaken krävs en djupgående analys från fall till fall. [Kontakta Adobe kundsupport](#customer-support) till att vara den här processen.
+++

### Hur kontaktar jag Adobe kundsupport? {#customer-support}

+++Svar
[En fullständig lista över telefonnummer till kundsupport från Adobe](https://helpx.adobe.com/ca/contact/phone.html) finns på hjälpsidan för Adobe. Du kan även hitta hjälp online genom att utföra följande steg:

- Navigera till [https://www.adobe.com/](https://www.adobe.com/) i webbläsaren.
- Till höger om det övre navigeringsfältet väljer du **[!UICONTROL Sign In]**.

![Adobe webbplats med inloggning markerad.](./images/troubleshooting/adobe-sign-in.png)

- Använd ditt Adobe ID och lösenord som är registrerat med din licens för Adobe.
- Välj **[!UICONTROL Help & Support]** i det övre navigeringsfältet.

![Den översta listrutan i navigeringsfältet med Hjälp och support, Enterprise Support och Kontakta oss är markerade.](./images/troubleshooting/help-and-support.png)

En rullgardinsbanderoll visas med en [!UICONTROL Help and support] -avsnitt. Välj **[!UICONTROL Contact us]** om du vill öppna den virtuella kundtjänstassistenten för Adobe, eller välja **[!UICONTROL Enterprise support]** för dedikerad hjälp för stora organisationer.
+++

### Hur implementerar jag en sekventiell serie med jobb, utan att köra efterföljande jobb om det tidigare jobbet inte slutförs korrekt?

+++Svar Med den anonyma blockfunktionen kan du kedja en eller flera SQL-satser som körs i följd. De gör det även möjligt att hantera undantag.

Se [anonym blockdokumentation](./essential-concepts/anonymous-block.md) för mer information.
+++

### Hur implementerar jag anpassad attribuering i Query Service?

+++Svar Det finns två sätt att implementera anpassad attribuering:

1. Använd en kombination av befintliga [Funktioner som definieras av Adobe](./sql/adobe-defined-functions.md) för att identifiera om behovet av ärendehantering är uppfyllt.
1. Om föregående förslag inte uppfyller ditt användningssätt bör du använda en kombination av [fönsterfunktioner](./sql/adobe-defined-functions.md#window-functions). Fönsterfunktioner tittar på alla händelser i en sekvens. De gör det även möjligt att granska historiska data och kan användas i valfri kombination.
+++

### Kan jag formatera mina frågor så att jag enkelt kan återanvända dem?

+++Besvara Ja, du kan mallsidentifiera frågor med hjälp av förberedda satser. Förförberedda satser kan optimera prestanda och undvika att behöva tolka en fråga flera gånger. Se [dokumentation om förberedda programsatser](./sql/prepared-statements.md) för mer information.
+++

### Hur hämtar jag felloggar för en fråga? {#error-logs}

+++Svar Om du vill hämta felloggar för en viss fråga måste du först använda API:t för frågetjänsten för att hämta information om frågeloggen. HTTP-svaret innehåller de fråge-ID:n som krävs för att undersöka ett frågefel.

Använd kommandot GET för att hämta flera frågor. Information om hur du anropar API:t finns i [exempeldokumentation för API-anrop](./api/queries.md#sample-api-calls).

Identifiera den fråga du vill undersöka och gör en annan GET-förfrågan med hjälp av svaret `id` värde. Fullständiga instruktioner finns i [hämta en fråga efter ID-dokumentation](./api/queries.md#retrieve-a-query-by-id).

Ett lyckat svar returnerar HTTP-status 200 och innehåller `errors` array. Svaret har förkortats av kortfattad anledning.

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

The [Referenshandbok för API för frågetjänst](https://www.adobe.io/experience-platform-apis/references/query-service/) innehåller mer information om alla tillgängliga slutpunkter.
+++

### Vad betyder &quot;Fel vid validering av schema&quot;?

+++Svar Meddelandet &quot;Fel vid validering av schema&quot; innebär att systemet inte kan hitta ett fält i schemat. Du bör läsa dokumentet med bästa praxis för att [ordna dataresurser i frågetjänsten](./best-practices/organize-data-assets.md) följt av [Skapa tabell som markerad dokumentation](./sql/syntax.md#create-table-as-select).

I följande exempel visas hur en CTAS-syntax och en strukturell datatyp används:

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### Hur behandlar jag snabbt nya data som kommer in i systemet varje dag?

+++Besvara [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) -satsen kan användas för att stegvis läsa data i en tabell baserat på ett ögonblicksbild-ID. Detta är idealiskt för [inkrementell belastning](./essential-concepts/incremental-load.md) designmönster som endast bearbetar information i datauppsättningen som har skapats eller ändrats sedan den senaste inläsningen. Resultatet blir effektivare bearbetning och kan användas med både direktuppspelning och batchdatabearbetning.
+++

### Varför är det en skillnad mellan siffrorna som visas i profilgränssnittet och siffrorna som beräknas från datauppsättningen för profilexport?

+++Svar Numren som visas på profilkontrollpanelen är korrekta vid den senaste ögonblicksbilden. De tal som genereras i exporttabellen är helt beroende av exportfrågan. Därför är det en vanlig orsak att fråga hur många profiler som är kvalificerade för en viss målgrupp.

>[!NOTE]
>
>Vid sökning inkluderas historiska data, medan användargränssnittet bara visar aktuella profildata.

+++

### Varför returnerade min fråga en tom delmängd och vad ska jag göra?

+++Svar Den troligaste orsaken är att frågan är för smal i omfånget. Du bör systematiskt ta bort ett avsnitt i `WHERE` tills du börjar se data.

Du kan också bekräfta att datauppsättningen innehåller data genom att använda en liten fråga som:

```sql
SELECT count(1) FROM myTableName
```

+++

### Kan jag ta prov på mina data?

+++Svar Den här funktionen är ett pågående arbete. Mer information finns i [versionsinformation](../release-notes/latest/latest.md) och via dialogrutorna för användargränssnittet när funktionen är klar för lansering.
+++

### Vilka hjälpfunktioner stöds av frågetjänsten?

+++Svarsfrågetjänsten innehåller flera inbyggda SQL-hjälpfunktioner som utökar SQL-funktionerna. Se dokumentet för en fullständig lista över [SQL-funktioner som stöds av frågetjänsten](./sql/spark-sql-functions.md).
+++

### Är alla inbyggda [!DNL Spark SQL] funktioner som stöds eller är användare begränsade till endast wrapper [!DNL Spark SQL] funktioner från Adobe?

+++Svara ännu, inte alla öppen källkod [!DNL Spark SQL] funktioner har testats på data i sjön. När de har testats och bekräftats läggs de till i listan över funktioner som stöds. Se [lista över stöd [!DNL Spark SQL] funktioner](./sql/spark-sql-functions.md) om du vill söka efter en viss funktion.
+++

### Kan användare definiera egna användardefinierade funktioner (UDF) som kan användas i andra frågor?

+++Svara På grund av datasäkerhetshänsyn är den anpassade definitionen av användardefinierat fält inte tillåten.
+++

### Vad ska jag göra om min schemalagda fråga misslyckas?

+++Besvara först, kontrollera loggarna för att ta reda på mer om felet. Frågor och svar om [hitta fel i loggar](#error-logs) innehåller mer information om hur du gör detta.

Du bör även läsa dokumentationen om hur du utför [schemalagda frågor i användargränssnittet](./ui/user-guide.md#scheduled-queries) och via [API](./api/scheduled-queries.md).

Tänk på det när du använder [!DNL Query Editor] Du kan bara lägga till ett schema i en fråga som redan har skapats, sparats och körts. Detta gäller inte för [!DNL Query Service] API.
+++

### Vad betyder felet &quot;Sessionsgräns nådd&quot;?

+++Svara &quot;Sessionsgränsen har nåtts&quot; innebär att det maximala antalet sessioner med frågetjänsten som tillåts för din organisation har uppnåtts. Kontakta Adobe Experience Platform-administratören i din organisation.
+++

### Hur hanterar frågeloggen frågor som relaterar till en borttagen datamängd?

+++Svarsfrågetjänsten tar aldrig bort frågehistoriken. Detta innebär att alla frågor som refererar till en borttagen datauppsättning returnerar&quot;Ingen giltig datauppsättning&quot; som ett resultat.
+++

### Hur hämtar jag bara metadata för en fråga?

+++Svar Du kan köra en fråga som returnerar noll rader för att bara få metadata som svar. Den här exempelfrågan returnerar bara metadata för den angivna tabellen.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Hur kan jag snabbt iterera på en CTAS-fråga (Skapa tabell som markerad) utan att materialisera den?

+++Svar Du kan skapa tillfälliga tabeller för att snabbt iterera och experimentera med en fråga innan den materialiseras för användning. Du kan också använda temporära tabeller för att validera om en fråga fungerar.

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

+++

### Hur ändrar jag tidszonen till och från en UTC-tidsstämpel?

+++Besvara Adobe Experience Platform består av data i UTC-format (Coordinated Universal Time) för tidsstämpling. Ett exempel på UTC-formatet är `2021-12-22T19:52:05Z`

Frågetjänsten stöder inbyggda SQL-funktioner för konvertering av en viss tidsstämpel till och från UTC-format. Båda `to_utc_timestamp()` och `from_utc_timestamp()` metoder har två parametrar: timestamp och timezone.

| Parameter | Beskrivning |
|-----------|---------------|
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

#### Konvertera från UTC-tidsstämpeln

The `from_utc_timestamp()` method tolkar de givna parametrarna **från tidsstämpeln i den lokala tidszonen** och ger motsvarande tidsstämpel för det önskade området i UTC-format. I exemplet nedan är timmen 2:40 PM i användarens lokala tidszon. Seoul-tidszonen som skickas som en variabel ligger nio timmar före den lokala tidszonen.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

Frågan returnerar en tidsstämpel i UTC-format för den tidszon som skickas som en parameter. Resultatet är nio timmar före den tidszon som körde frågan.

```
8/31/2021, 11:40 PM
```

### Hur ska jag filtrera mina tidsseriedata?

+++Svar Vid fråga med tidsseriedata bör du använda tidsstämpelfiltret när det är möjligt för mer korrekt analys.

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

+++

### Hur använder jag `CAST` för att konvertera mina tidsstämplar i SQL-frågor?

+++Svara när du använder `CAST` om du vill konvertera en tidsstämpel måste du inkludera både datumet och **och** tid.

Om du t.ex. saknar tidskomponenten, som visas nedan, uppstår ett fel:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Korrekt användning av `CAST` operatorn visas nedan:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### Ska jag använda jokertecken som * för att hämta alla rader från mina datamängder?

+++Svar Du kan inte använda jokertecken för att hämta alla data från dina rader, eftersom frågetjänsten ska behandlas som en **columnar-store** i stället för ett vanligt radbaserat lagringssystem.
+++

### Ska jag använda `NOT IN` i min SQL-fråga?

+++Besvara `NOT IN` används ofta för att hämta rader som inte finns i en annan tabell eller SQL-sats. Operatorn kan göra prestandan långsammare och kan returnera oväntade resultat om kolumnerna som jämförs accepterar `NOT NULL`eller så har du ett stort antal poster.

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

Om du använder `LEFT OUTER JOIN` kan du replikera med `NOT IN` genom att använda följande fråga:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### Kan jag skapa en datauppsättning med en CTAS-fråga med ett namn med dubbla understreck som de som visas i gränssnittet? Exempel: `test_table_001`.

+++Svarsnr. Detta är en avsiktlig begränsning i Experience Platform som gäller för alla Adobe-tjänster, inklusive frågetjänsten. Ett namn med två understreck accepteras som ett schema- och datauppsättningsnamn, men tabellnamnet för datauppsättningen får bara innehålla ett understreck.
+++

### Hur många samtidiga frågor kan du köra samtidigt?

+++Svar Det finns ingen gräns för samtidighet för frågor eftersom batchfrågor körs som backend-jobb. Det finns dock en timeout för frågor som är inställd på 24 timmar.
+++

### Finns det en aktivitetspanel där du kan se frågeaktiviteter och status?

+++Svar Det finns övervaknings- och varningsfunktioner för att kontrollera frågeaktiviteter och status. Se [Integrering av granskningslogg för frågetjänsten](./data-governance/audit-log-guide.md) och [frågeloggar](./ui/overview.md#log) -dokument för mer information.
+++

### Finns det något sätt att återställa uppdateringar? Om det till exempel finns ett fel eller om vissa beräkningar behöver konfigureras om när data skrivs tillbaka till plattformen, hur ska detta scenario hanteras?

+++Svar För närvarande stöder vi inte återställningar eller uppdateringar på det sättet.
+++

### Hur kan du optimera frågor i Adobe Experience Platform?

+++Svar Systemet har inga index eftersom det inte är en databas, men har andra optimeringar som är kopplade till datalagret. Följande alternativ är tillgängliga för att justera dina frågor:

- Ett tidsbaserat filter som bygger på tidsseriedata.
- Optimerad nedtryckning för strukturdatatypen.
- Optimerad kostnad och minneshantering för matriser och kartdatatyper.
- Inkrementell bearbetning med ögonblicksbilder.
- Ett beständigt dataformat.
+++

### Kan inloggningar begränsas till vissa aspekter av frågetjänsten eller är det en&quot;allt eller ingenting&quot;-lösning?

+++Svarsfrågetjänsten är en&quot;all eller ingenting&quot;-lösning. Det går inte att ge partiell åtkomst.
+++

### Kan jag begränsa vilka data Query Service kan använda, eller har den bara tillgång till hela Adobe Experience Platform datasjön?

+++Besvara Ja, du kan begränsa frågan till datauppsättningar med skrivskyddad åtkomst.
+++

### Vilka andra alternativ finns det för att begränsa vilka data som kan nås via frågetjänsten?

+++Svar Det finns tre sätt att begränsa åtkomsten. De är följande:

- Använd bara SELECT-programsatser och ge datauppsättningar skrivskyddad åtkomst. Tilldela även behörigheten Hantera fråga.
- Använd SELECT/INSERT/CREATE-programsatser och ge datauppsättningar skrivbehörighet. Tilldela även behörigheten för frågehantering.
- Använd ett integrationskonto med föregående förslag ovan och tilldela frågeintegrationsbehörigheten.

+++

### När data har returnerats av Query Service, finns det några kontroller som kan köras av Platform för att säkerställa att inga skyddade data har returnerats?

- Frågetjänsten stöder attributbaserad åtkomstkontroll. Du kan begränsa åtkomsten till data på kolumn-/lövnivå och/eller strukturnivå. Mer information om attributbaserad åtkomstkontroll finns i dokumentationen.

### Kan jag ange ett SSL-läge för anslutningen till en tredjepartsklient? Kan jag till exempel använda verify-full med Power BI?

+++Svara Ja, SSL-lägen stöds. Se [Dokumentation för SSL-lägen](./clients/ssl-modes.md) för en uppdelning av de olika SSL-lägena som är tillgängliga och den skyddsnivå de erbjuder.
+++

### Använder vi TLS 1.2 för alla anslutningar från Power BI-klienter för att fråga tjänsten?

+++Besvara Ja. Data-in-Transition är alltid HTTPS-kompatibel. Den version som stöds för närvarande är TLS1.2.
+++

### Använder en anslutning som görs på port 80 fortfarande https?

+++Svar Ja, en anslutning som görs på port 80 använder fortfarande SSL. Du kan också använda port 5432.
+++

### Kan jag styra åtkomsten till specifika datauppsättningar och kolumner för en viss anslutning? Hur är detta konfigurerat?

+++Svara Ja, attributbaserad åtkomstkontroll används om den har konfigurerats. Se [attributbaserad åtkomstkontroll - översikt](../access-control/abac/overview.md) för mer information.
+++

### Stöder frågetjänsten kommandot INSERT OVERWRITE INTO?

+++Svarsnr, frågetjänsten stöder inte kommandot INSERT OVERWRITE INTO.
+++

## Exportera data {#exporting-data}

I det här avsnittet finns information om hur du exporterar data och begränsningar.

### Finns det något sätt att extrahera data från frågetjänsten efter frågebearbetning och spara resultaten i en CSV-fil? {#export-csv}

+++Besvara Ja. Data kan extraheras från frågetjänsten och det finns även ett alternativ för att lagra resultaten i CSV-format via ett SQL-kommando.

Det finns två sätt att spara resultatet av en fråga när du använder en PSQL-klient. Du kan använda `COPY TO` eller skapa en programsats med följande format:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Vägledning om användningen av `COPY TO` kommando](./sql/syntax.md#copy) finns i referensdokumentationen för SQL-syntaxen.
+++

### Kan jag extrahera innehållet i den slutliga datauppsättningen som har importerats via CTAS-frågor (förutsatt att det är större mängder data som Terabytes)?

+++Svarsnr Det finns för närvarande ingen funktion för extrahering av inkapslade data.
+++

### Varför returnerar inte Analytics-dataanslutningen data?

+++Svar En vanlig orsak till det här problemet är att fråga efter data i tidsserier utan tidsfilter. Exempel:

```sql
SELECT * FROM prod_table LIMIT 1;
```

Ska skrivas som:

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## Tredjepartsverktyg {#third-party-tools}

Detta avsnitt innehåller information om användning av tredjepartsverktyg som PSQL och Power BI.

### Kan jag ansluta frågetjänsten till ett verktyg från tredje part?

+++Besvara Ja, du kan ansluta flera tredjepartsklienter till Query Service. Läs dokumentationen för [fullständig information om tillgängliga klienter och hur du ansluter dem till tjänsten Query](./clients/overview.md).
+++

### Finns det något sätt att ansluta frågetjänsten en gång för kontinuerlig användning med ett verktyg från tredje part?

+++Besvara Ja, klientdatorer från tredje part kan anslutas till frågetjänsten via en engångsinstallation av ej förfallande autentiseringsuppgifter. Autentiseringsuppgifter som inte förfaller kan genereras av en behörig användare och tas emot i en JSON-fil som automatiskt hämtas till den lokala datorn. Fullständig [vägledning om hur du skapar och hämtar ej förfallodatum för inloggningsuppgifter](./ui/credentials.md#non-expiring-credentials) finns i dokumentationen.
+++

### Varför fungerar inte mina inloggningsuppgifter som inte förfaller?

+++Svara Värdet för ej förfallande autentiseringsuppgifter är sammanfogade argument från `technicalAccountID` och `credential` hämtas från JSON-konfigurationsfilen. Lösenordsvärdet har följande format: `{{technicalAccountId}:{credential}}`.
Mer information om hur du gör det finns i dokumentationen [ansluta till externa klienter med autentiseringsuppgifter](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### Vilken typ av SQL-redigerare från tredje part kan jag ansluta till Query Service Editor?

+++Besvara någon SQL-redigerare från tredje part som är PSQL eller [!DNL Postgres] klientkompatibel kan anslutas till Query Service Editor. Läs dokumentationen för [ansluta klienter till frågetjänsten](./clients/overview.md) om du vill se en lista över tillgängliga instruktioner.
+++

### Kan jag ansluta Power BI-verktyget till Query Service?

+++Svar Ja, du kan ansluta Power BI till frågetjänsten. Läs dokumentationen för [anvisningar om hur du ansluter Power BI-datorprogrammet till Query Service](./clients/power-bi.md).
+++

### Varför tar det lång tid att läsa in kontrollpanelerna när de är anslutna till Query Service?

+++Svar När systemet är anslutet till frågetjänsten är det anslutet till en interaktiv eller gruppbearbetningsmotor. Detta kan leda till längre inläsningstider för att återspegla de bearbetade data.

Om du vill förbättra svarstiderna för dina instrumentpaneler bör du implementera en Business Intelligence-server (BI) som ett cachelagringslager mellan Query Service och BI-verktyg. I allmänhet har de flesta BI-verktyg ett extra erbjudande för en server.

Syftet med att lägga till cacheserverlagret är att cachelagra data från frågetjänsten och använda samma för kontrollpaneler för att snabba upp svaret. Detta är möjligt eftersom resultaten för frågor som körs cachelagras i BI-servern varje dag. Cachelagringsservern skickar sedan dessa resultat till alla användare med samma fråga för att minska fördröjningen. Se dokumentationen för verktyget eller tredjepartsverktyget som du använder för att få mer information om den här konfigurationen.
+++

### Är det möjligt att komma åt Query Service med anslutningsverktyget pgAdmin?

+++Svarsnr, pgAdmin-anslutning stöds inte. A [lista över tillgängliga tredjepartsklienter och instruktioner för hur de ska anslutas till frågetjänsten](./clients/overview.md) finns i dokumentationen.
+++

## PostgreSQL API-fel {#postgresql-api-errors}

Följande tabell innehåller PSQL-felkoder och deras möjliga orsaker.

| Felkod | Anslutningstillstånd | Beskrivning | Möjlig orsak |
|------------|---------------------------|-------------|----------------|
| **08P01** | Ej tillämpligt | Meddelandetypen stöds inte | Meddelandetypen stöds inte |
| **28P01** | Start - autentisering | Ogiltigt lösenord | Ogiltig autentiseringstoken |
| **28000** | Start - autentisering | Ogiltig auktoriseringstyp | Ogiltig auktoriseringstyp. Måste vara `AuthenticationCleartextPassword`. |
| **42P12** | Start - autentisering | Inga tabeller hittades | Inga tabeller hittades för användning |
| **42601** | Fråga | Syntaxfel | Ogiltigt kommando eller syntaxfel |
| **42P01** | Fråga | Tabellen hittades inte | Tabellen som angavs i frågan hittades inte |
| **42P07** | Fråga | Tabellen finns | Det finns redan en tabell med samma namn (CREATE TABLE) |
| **53400** | Fråga | LIMIT överskrider maxvärdet | Användaren angav en LIMIT-sats som är högre än 100 000 |
| **53400** | Fråga | Tidsgräns för instruktion | Den inskickade livebeskrivningen tog mer än maximalt 10 minuter |
| **58000** | Fråga | Systemfel | Internt systemfel |
| **0A000** | Fråga/kommando | Stöds inte | Funktionen/funktionen i frågan/kommandot stöds inte |
| **42501** | DROP TABLE Query | Släpptabellen har inte skapats av frågetjänsten | Tabellen som tas bort skapades inte av frågetjänsten med `CREATE TABLE` programsats |
| **42501** | DROP TABLE Query | Tabellen har inte skapats av den autentiserade användaren | Tabellen som tas bort skapades inte av den inloggade användaren |
| **42P01** | DROP TABLE Query | Tabellen hittades inte | Det gick inte att hitta tabellen som angavs i frågan |
| **42P12** | DROP TABLE Query | Ingen tabell hittades för `dbName`: kontrollera `dbName` | Inga tabeller hittades i den aktuella databasen |

### Varför fick jag en 58000-felkod när jag använde metoden history_meta() i min tabell?

+++Besvara `history_meta()` -metoden används för att få åtkomst till en ögonblicksbild från en datauppsättning. Tidigare, om du skulle köra en fråga på en tom datauppsättning i Azure Data Lake Storage (ADLS), skulle du få en felkod på 58000 som anger att datauppsättningen inte finns. Ett exempel på det gamla systemfelet visas nedan.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Det här felet uppstod eftersom det inte fanns något returvärde för frågan. Det här beteendet har nu åtgärdats för att returnera följande meddelande:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## REST API-fel {#rest-api-errors}

Följande tabell innehåller HTTP-felkoder och deras möjliga orsaker.

| HTTP-statuskod | Beskrivning | Möjliga orsaker |
|------------------|-----------------------|----------------------------|
| 400 | Felaktig begäran | Felaktig eller ogiltig fråga |
| 401 | Autentiseringen misslyckades | Ogiltig auth-token |
| 500 | Internt serverfel | Internt systemfel |
