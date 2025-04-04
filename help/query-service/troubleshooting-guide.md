---
keywords: Experience Platform;home;populära topics;query service;Query service;felsökningsguide;faq;troubleshooting;
solution: Experience Platform
title: Fråga service och data Distiller frågor och svar
description: Det här dokumentet innehåller vanliga frågor och svar om Query Service och Data Distiller. Här finns ämnen som export av data, verktyg från tredje part och PSQL-fel.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '5011'
ht-degree: 0%

---

# Fråga service och data Distiller frågor och svar

Det här dokumentet besvarar vanliga frågor om Query Service och Data Distiller. Den innehåller även vanliga felkoder när man använder produkten &quot;Frågor&quot; för datavalidering eller skriver transformerade data tillbaka till datasjön. Om du har frågor eller vill felsöka andra Adobe Experience Platform-tjänster kan du läsa [Experience Platform felsökningsguide](../landing/troubleshooting.md).

Här är två grundläggande frågor för att klargöra hur Query Service och Data Distiller samverkar inom Adobe Experience Platform.

## Vilken är relationen mellan Query Service och Data Distiller?

Query Service och Data Distiller är distinkta, kompletterande komponenter som ger specifika funktioner för datafrågor. Frågetjänsten är avsedd för ad hoc-frågor för att utforska, validera och experimentera med importerade data utan att ändra datasjön. Data Distiller fokuserar däremot på batchfrågor som omformar och berikar data, med resultat som lagras tillbaka i datasjön för framtida bruk. Batchfrågor i Data Distiller kan schemaläggas, övervakas och hanteras, vilket stöder mer omfattande databearbetning och -hantering som inte enbart kan hanteras med Query Service.

Frågetjänsten ger tillsammans snabba insikter, medan Data Distiller möjliggör djupgående, permanenta dataomvandlingar.

## Vad är skillnaden mellan Query Service och Data Distiller?

**Frågetjänst**: Används för SQL-frågor med fokus på datautforskande, validering och experimenterande. Utdata lagras inte i datasjön och körningstiden är begränsad till 10 minuter. Ad hoc-frågor är lämpliga för enkla, interaktiva datakontroller och analyser.

**Data Distiller**: Aktiverar gruppfrågor som bearbetar, rensar och berikar data, med resultat som lagras i datasjön. Dessa frågor har stöd för längre körningstid (upp till 24 timmar) och ytterligare funktioner som schemaläggning, övervakning och snabbare rapportering. Data Distiller är idealiskt för omfattande datamanipulering och schemalagda databehandlingsåtgärder.

Mer information finns i paketeringsdokumentet för [frågetjänsten](./packaging.md).

## Frågekategorier {#categories}

Följande lista med svar på vanliga frågor är indelad i följande kategorier:

- [Allmänt](#general)
- [Data Distiller](#data-distiller)
- [Användargränssnitt för frågor](#queries-ui)
- [Datauppsättningsexempel](#dataset-samples)
- [Exportera data](#exporting-data)
- [SQL-syntax](#sql-syntax) 
- [ITAS-frågor](#itas-queries)
- [Tredjepartsverktyg](#third-party-tools)
- [PostgreSQL API-fel](#postgresql-api-errors)
- [REST API-fel](#rest-api-errors)

## Allmänna frågor om frågetjänsten {#general}

Det här avsnittet innehåller information om prestanda, begränsningar och processer.

### Kan jag inaktivera funktionen för automatisk komplettering i frågetjänstredigeraren?

+++Svar
Nej. Redigeraren stöder för närvarande inte att funktionen Komplettera automatiskt stängs av.
+++

### Varför blir Frågeredigeraren ibland långsam när jag skriver en fråga?

+++Svar
En möjlig orsak är funktionen för automatisk komplettering. Funktionen bearbetar vissa metadatakommandon som ibland kan göra redigeraren långsammare vid redigering av frågor.
+++

### Kan jag använda [!DNL Postman] för API:t för frågetjänsten?

+++Svar
Ja, du kan visualisera och interagera med alla Adobe API-tjänster med [!DNL Postman] (ett kostnadsfritt program från tredje part). I [[!DNL Postman] installationsguiden](https://video.tv.adobe.com/v/28832) finns stegvisa instruktioner för hur du konfigurerar ett projekt i Adobe Developer Console och hämtar alla nödvändiga autentiseringsuppgifter för användning med [!DNL Postman]. I den officiella dokumentationen finns [vägledning om hur du startar, kör och delar [!DNL Postman] samlingar](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Finns det någon gräns för hur många rader som får returneras från en fråga via användargränssnittet?

+++Svar
Ja, frågetjänsten tillämpar internt en gräns på 50 000 rader om inte en explicit gräns anges externt. Mer information finns i vägledningen om [interaktiv frågekörning](./best-practices/writing-queries.md#interactive-query-execution).
+++

### Kan jag använda frågor för att uppdatera rader?

+++Svar
I gruppfrågor stöds inte uppdatering av en rad i datauppsättningen.
+++

### Finns det någon gräns för datastorlek för resultatet från en fråga?

+++Svar
Nej. Det finns ingen gräns för datastorlek, men det finns en timeout för frågor på 10 minuter från en interaktiv session. Om frågan körs som en batch-CTAS gäller inte en 10-minuterstimeout. Mer information finns i vägledningen om [interaktiv frågekörning](./best-practices/writing-queries.md#interactive-query-execution).
+++

### Hur stoppar jag mina frågor från att tajma ut på tio minuter?

+++Svar
En eller flera av följande lösningar rekommenderas vid timeout i frågor.

- [Konvertera frågan till en CTAS-fråga](./sql/syntax.md#create-table-as-select) och schemalägg körningen. Du kan schemalägga en körning antingen [ via gränssnittet ](./ui/user-guide.md#scheduled-queries) eller [API](./api/scheduled-queries.md#create).
- Kör frågan i ett mindre datasegment genom att tillämpa ytterligare [filtervillkor](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Kör EXPLAIN-kommandot](./sql/syntax.md#explain) om du vill samla in mer information.
- Granska statistiken för data i datauppsättningen.
- Konvertera frågan till ett förenklat formulär och kör den igen med [förberedda satser](./sql/prepared-statements.md).
+++

### Finns det något problem eller någon inverkan på frågetjänstens prestanda om flera frågor körs samtidigt?

+++Svar
Nej. Frågetjänsten har en autoskalningsfunktion som säkerställer att samtidiga frågor inte har någon märkbar påverkan på tjänstens prestanda.
+++

### Kan jag använda reserverade nyckelord som kolumnnamn?

+++Svar
Det finns vissa reserverade nyckelord som inte kan användas som kolumnnamn som `ORDER`, `GROUP BY`, `WHERE`, `DISTINCT`. Om du vill använda dessa nyckelord måste du undvika dessa kolumner.
+++

### Hur hittar jag ett kolumnnamn från en hierarkisk datauppsättning?

+++Svar
Följande steg beskriver hur du visar en tabellvy av en datauppsättning via användargränssnittet, inklusive alla kapslade fält och kolumner i ett förenklat formulär.

- När du har loggat in på Experience Platform väljer du **[!UICONTROL Datasets]** i den vänstra navigeringen i användargränssnittet för att navigera till [!UICONTROL Datasets]-instrumentpanelen.
- Fliken för datauppsättningar [!UICONTROL Browse] öppnas. Du kan använda sökfältet för att förfina de tillgängliga alternativen. Välj en datauppsättning i den lista som visas.

![Kontrollpanelen för datauppsättningar i Experience Platform-gränssnittet med sökfältet och en datauppsättning markerad.](./images/troubleshooting/dataset-selection.png)

- Skärmen [!UICONTROL Datasets activity] visas. Välj **[!UICONTROL Preview dataset]** om du vill öppna en dialogruta med XDM-schemat och en tabellvy med separerade data från den valda datauppsättningen. Mer information finns i [förhandsgranskningen av en datauppsättningsdokumentation](../catalog/datasets/user-guide.md#preview-a-dataset)

![Fliken Datauppsättningsaktivitet på kontrollpanelen Datamängder med datamängden Förhandsgranska markerad.](./images/troubleshooting/dataset-preview.png)

- Markera ett fält i schemat om du vill visa innehållet i en förenklad kolumn. Kolumnens namn visas ovanför innehållet till höger på sidan. Du bör kopiera det här namnet om du vill använda det för att fråga om den här datauppsättningen.

![XDM-schemat och tabellvyn för de separerade data. Kolumnnamnet för en kapslad datauppsättning markeras i användargränssnittet.](./images/troubleshooting/column-name.png)

I dokumentationen finns fullständig vägledning om [hur du arbetar med kapslade datastrukturer](./key-concepts/nested-data-structures.md) med frågeredigeraren eller en tredjepartsklient.
+++

### Hur snabbar jag upp en fråga i en datauppsättning som innehåller arrayer?

+++Svar
Om du vill förbättra prestanda för frågor om datauppsättningar som innehåller arrayer ska du [utforska arrayen](https://spark.apache.org/docs/latest/api/sql/index.html#explode) som en [CTAS-fråga](./sql/syntax.md#create-table-as-select) vid körning och sedan utforska den för att hitta möjligheter att förbättra bearbetningstiden.
+++

### Varför bearbetas min CTAS-fråga fortfarande efter många timmar för ett litet antal rader?

+++Svar
Om frågan har tagit lång tid på en mycket liten datauppsättning kontaktar du kundsupporten.

Det kan finnas många orsaker till att en fråga har fastnat under bearbetningen. För att fastställa den exakta orsaken krävs en djupgående analys från fall till fall. [Kontakta Adobe kundsupport](#customer-support) om du vill vara den här processen.
+++

### Hur kontaktar jag Adobe kundsupport? {#customer-support}

+++Svar
[En fullständig lista över Adobe telefonnummer för kundsupport](https://helpx.adobe.com/ca/contact/phone.html) finns på hjälpsidan för Adobe. Du kan även hitta hjälp online genom att utföra följande steg:

- Navigera till [https://www.adobe.com/](https://www.adobe.com/) i webbläsaren.
- Välj **[!UICONTROL Sign In]** till höger om det övre navigeringsfältet.

![Adobe webbplats med inloggning markerad.](./images/troubleshooting/adobe-sign-in.png)

- Använd ditt Adobe ID och lösenord som är registrerat med din Adobe-licens.
- Välj **[!UICONTROL Help & Support]** i det övre navigeringsfältet.

![Den översta listrutan i navigeringsfältet med Hjälp och support, Enterprise Support och Kontakta oss är markerade.](./images/troubleshooting/help-and-support.png)

En rullgardinsmeny med avsnittet [!UICONTROL Help and support] visas. Välj **[!UICONTROL Contact us]** om du vill öppna den virtuella kundtjänstassistenten för Adobe, eller välj **[!UICONTROL Enterprise support]** om du vill ha dedikerad hjälp för stora organisationer.
+++

### Hur implementerar jag en sekventiell serie med jobb, utan att köra efterföljande jobb om det tidigare jobbet inte slutförs korrekt?

+++Svar
Med den anonyma blockfunktionen kan du kedja en eller flera SQL-satser som körs i sekvens. De gör det även möjligt att hantera undantag.

Mer information finns i [dokumentationen för anonyma block](./key-concepts/anonymous-block.md).
+++

### Hur implementerar jag anpassad attribuering i Query Service?

+++Svar
Det finns två sätt att implementera anpassad attribuering:

1. Använd en kombination av befintliga [Adobe-definierade funktioner](./sql/adobe-defined-functions.md) för att identifiera om användningsbehoven uppfylls.
1. Om föregående förslag inte uppfyller ditt användningssätt bör du använda en kombination av [fönsterfunktioner](./sql/adobe-defined-functions.md#window-functions). Fönsterfunktioner tittar på alla händelser i en sekvens. De gör det även möjligt att granska historiska data och kan användas i valfri kombination.
+++

### Kan jag formatera mina frågor så att jag enkelt kan återanvända dem?

+++Svar
Ja, du kan mallsidigera frågor genom att använda förberedda satser. Förförberedda satser kan optimera prestanda och undvika att behöva tolka en fråga flera gånger. Mer information finns i [dokumentationen för förberedda programsatser](./sql/prepared-statements.md).
+++

### Hur hämtar jag felloggar för en fråga? {#error-logs}

+++Svar
Om du vill hämta felloggar för en viss fråga måste du först använda API:t för frågetjänsten för att hämta information om frågeloggen. HTTP-svaret innehåller de fråge-ID:n som krävs för att undersöka ett frågefel.

Använd kommandot GET för att hämta flera frågor. Information om hur du anropar API finns i [exempeldokumentationen för API-anrop](./api/queries.md#sample-api-calls).

Identifiera den fråga du vill undersöka från svaret och gör en annan GET-begäran med hjälp av dess `id`-värde. Fullständiga instruktioner finns i [Hämta en fråga efter ID-dokumentation](./api/queries.md#retrieve-a-query-by-id).

Ett lyckat svar returnerar HTTP-status 200 och innehåller arrayen `errors`. Svaret har förkortats av kortfattad anledning.

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

[Referensdokumentationen för API:t för frågetjänsten](https://www.adobe.io/experience-platform-apis/references/query-service/) innehåller mer information om alla tillgängliga slutpunkter.
+++

### Vad betyder &quot;Fel vid validering av schema&quot;?

+++Svar
Meddelandet &quot;Fel vid validering av schema&quot; betyder att systemet inte kan hitta ett fält i schemat. Du bör läsa dokumentet med bästa praxis för att [organisera dataresurser i frågetjänsten](./best-practices/organize-data-assets.md) följt av [Skapa tabell som markeringsdokumentation](./sql/syntax.md#create-table-as-select).

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

+++Svar
Satsen [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) kan användas för att stegvis läsa data i en tabell baserat på ett ögonblicksbild-ID. Detta är idealiskt för användning med designmönstret [inkrementell last](./key-concepts/incremental-load.md) som endast bearbetar information i datauppsättningen som har skapats eller ändrats sedan den senaste inläsningen. Resultatet blir effektivare bearbetning och kan användas med både direktuppspelning och batchdatabearbetning.
+++

### Varför är det en skillnad mellan siffrorna som visas i profilgränssnittet och siffrorna som beräknas från datauppsättningen för profilexport?

+++Svar
Siffrorna som visas på profilkontrollpanelen är korrekta vid den senaste ögonblicksbilden. De tal som genereras i exporttabellen är helt beroende av exportfrågan. Därför är det en vanlig orsak att fråga hur många profiler som är kvalificerade för en viss målgrupp.

>[!NOTE]
>
>Vid sökning inkluderas historiska data, medan användargränssnittet bara visar aktuella profildata.

+++

### Varför returnerade min fråga en tom delmängd och vad ska jag göra?

+++Svar
Den mest troliga orsaken är att frågan är för smal i omfånget. Du bör systematiskt ta bort ett avsnitt i `WHERE`-satsen tills du börjar se data.

Du kan också bekräfta att datauppsättningen innehåller data genom att använda en liten fråga som:

```sql
SELECT count(1) FROM myTableName
```

+++

### Kan jag ta prov på mina data?

+++Svar
Den här funktionen är ett pågående arbete. Information kommer att göras tillgänglig i [versionsinformationen](../release-notes/latest/latest.md) och i Experience Platform-dialogrutor så snart funktionen är klar för publicering.
+++

### Vilka hjälpfunktioner stöds av frågetjänsten?

+++Svar
Frågetjänsten innehåller flera inbyggda SQL-hjälpfunktioner som utökar SQL-funktionerna. I dokumentet finns en fullständig lista över de [SQL-funktioner som stöds av frågetjänsten](./sql/spark-sql-functions.md).
+++

### Stöds alla inbyggda [!DNL Spark SQL]-funktioner eller är användarna begränsade till endast de [!DNL Spark SQL]-wrapperfunktioner som tillhandahålls av Adobe?

+++Svar
Alla [!DNL Spark SQL]-funktioner med öppen källkod har ännu inte testats på data i sjön. När de har testats och bekräftats läggs de till i listan över funktioner som stöds. Se [listan över funktioner som stöds [!DNL Spark SQL] om du vill söka efter en viss funktion.](./sql/spark-sql-functions.md)
+++

### Kan användare definiera egna användardefinierade funktioner (UDF) som kan användas i andra frågor?

+++Svar
På grund av datasäkerhetshänsyn tillåts inte den anpassade definitionen av användardefinierat fält.
+++

### Vad ska jag göra om min schemalagda fråga misslyckas?

+++Svar
Kontrollera först loggarna för att få reda på mer om felet. Avsnittet med vanliga frågor om att [hitta fel i loggar](#error-logs) innehåller mer information om hur du gör detta.

Du bör även läsa dokumentationen om hur du utför [schemalagda frågor i användargränssnittet](./ui/user-guide.md#scheduled-queries) och via [API](./api/scheduled-queries.md).

När du använder [!DNL Query Editor] kan du bara lägga till ett schema i en fråga som redan har skapats och sparats. Detta gäller inte API:t [!DNL Query Service].
+++

### Vad betyder felet &quot;Sessionsgräns nådd&quot;?

+++Svar
&quot;Sessionsgränsen har nåtts&quot; innebär att det maximala antalet sessioner med frågetjänsten som tillåts för din organisation har uppnåtts. Kontakta Adobe Experience Platform-administratören i din organisation.
+++

### Hur hanterar frågeloggen frågor som relaterar till en borttagen datamängd?

+++Svar
Frågetjänsten tar aldrig bort frågehistoriken. Detta innebär att alla frågor som refererar till en borttagen datauppsättning returnerar&quot;Ingen giltig datauppsättning&quot; som ett resultat.
+++

### Hur hämtar jag bara metadata för en fråga?

+++Svar
Du kan köra en fråga som returnerar noll rader för att bara få metadata som svar. Den här exempelfrågan returnerar bara metadata för den angivna tabellen.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Hur kan jag snabbt iterera på en CTAS-fråga (Skapa tabell som markerad) utan att materialisera den?

+++Svar
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

+++

### Hur ändrar jag tidszonen till och från en UTC-tidsstämpel?

+++Svar
Adobe Experience Platform innehåller data i UTC-format (Coordinated Universal Time) för tidsstämpling. Ett exempel på UTC-formatet är `2021-12-22T19:52:05Z`

Frågetjänsten stöder inbyggda SQL-funktioner för konvertering av en viss tidsstämpel till och från UTC-format. Metoderna `to_utc_timestamp()` och `from_utc_timestamp()` har två parametrar: timestamp och timezone.

| Parameter | Beskrivning |
|-----------|---------------|
| Tidsstämpel | Tidsstämpeln kan skrivas i antingen UTC-format eller enkelt `{year-month-day}`-format. Om ingen tid anges är standardvärdet midnatt på morgonen den angivna dagen. |
| Tidszon | Tidszonen skrivs i formatet `{continent/city})`. Det måste vara en av de erkända tidszonskoderna som finns i TZ-databasen [för offentlig domän](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Konvertera till UTC-tidsstämpeln

Metoden `to_utc_timestamp()` tolkar de angivna parametrarna och konverterar den **till tidsstämpeln för den lokala tidszonen** i UTC-format. Exempelvis är tidszonen i Seoul i Sydkorea UTC/GMT +9 timmar. Genom att ange en tidsstämpel som bara är ett datum, använder metoden standardvärdet midnatt på morgonen. Tidsstämpeln och tidszonen konverteras till UTC-format från tidpunkten i den regionen till en UTC-tidsstämpel för den lokala regionen.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

Frågan returnerar en tidsstämpel i användarens lokala tid. I det här fallet är klockan 16.00 föregående dag som Seoul nio timmar framåt.

```
2021-08-30 15:00:00
```

Om den angivna tidsstämpeln var `2021-07-14 12:40:00.0` för tidszonen `Asia/Seoul` skulle den returnerade UTC-tidsstämpeln vara `2021-07-14 03:40:00.0`

Konsolutdata i gränssnittet för frågetjänsten är ett mer läsbart format:

```
8/30/2021, 3:00 PM
```

#### Konvertera från UTC-tidsstämpeln

Metoden `from_utc_timestamp()` tolkar de angivna parametrarna **från tidsstämpeln för den lokala tidszonen** och tillhandahåller motsvarande tidsstämpel för det önskade området i UTC-format. I exemplet nedan är timmen 2:40 PM i användarens lokala tidszon. Seoul-tidszonen som skickas som en variabel ligger nio timmar före den lokala tidszonen.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

Frågan returnerar en tidsstämpel i UTC-format för den tidszon som skickas som en parameter. Resultatet är nio timmar före den tidszon som körde frågan.

```
8/31/2021, 11:40 PM
```

### Hur ska jag filtrera mina tidsseriedata?

+++Svar
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

+++

### Hur använder jag operatorn `CAST` korrekt för att konvertera mina tidsstämplar i SQL-frågor?

+++Svar
När du använder operatorn `CAST` för att konvertera en tidsstämpel måste du inkludera både datumet **och** tid.

Om du t.ex. saknar tidskomponenten, som visas nedan, uppstår ett fel:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Korrekt användning av operatorn `CAST` visas nedan:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### Ska jag använda jokertecken som * för att hämta alla rader från mina datamängder?

+++Svar
Du kan inte använda jokertecken för att hämta alla data från raderna, eftersom frågetjänsten ska behandlas som ett **columnnar-store** i stället för som ett vanligt radbaserat lagringssystem.
+++

### Ska jag använda `NOT IN` i min SQL-fråga?

+++Svar
Operatorn `NOT IN` används ofta för att hämta rader som inte finns i en annan tabell eller SQL-sats. Operatorn kan göra prestandan långsammare och kan returnera oväntade resultat om kolumnerna som jämförs accepterar `NOT NULL`, eller om du har ett stort antal poster.

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

Om du använder operatorn `NOT EXISTS` kan du replikera med operatorn `NOT IN` genom att använda följande fråga:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Om du använder operatorn `LEFT OUTER JOIN` kan du också replikera med operatorn `NOT IN` genom att använda följande fråga:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### Kan jag skapa en datauppsättning med en CTAS-fråga med ett namn med dubbla understreck som de som visas i gränssnittet? Till exempel: `test_table_001`.

+++Svar
Nej, detta är en avsiktlig begränsning i Experience Platform som gäller alla Adobe-tjänster, inklusive Query Service. Ett namn med två understreck accepteras som ett schema- och datauppsättningsnamn, men tabellnamnet för datauppsättningen får bara innehålla ett understreck.
+++

### Hur många samtidiga frågor kan du köra samtidigt?

+++Svar
Det finns ingen gräns för samtidighet för frågor eftersom batchfrågor körs som backend-jobb. Det finns dock en timeout för frågor som är inställd på 24 timmar.
+++

### Finns det en aktivitetspanel där du kan se frågeaktiviteter och status?

+++Svar
Det finns övervaknings- och varningsfunktioner för att kontrollera frågeaktiviteter och status. Mer information finns i loggintegreringen för [frågetjänstens granskningslogg](./data-governance/audit-log-guide.md) och i [frågeloggarna](./ui/overview.md#log) .
+++

### Finns det något sätt att återställa uppdateringar? Om det till exempel finns ett fel eller om vissa beräkningar behöver konfigureras om när data skrivs tillbaka till Experience Platform, hur ska då detta scenario hanteras?

+++Svar
För närvarande stöder vi inte återställningar eller uppdateringar på det sättet.
+++

### Hur kan du optimera frågor i Adobe Experience Platform?

+++Svar
Systemet har inga index eftersom det inte är en databas, men det har andra optimeringar som är kopplade till datalagret. Följande alternativ är tillgängliga för att justera dina frågor:

- Ett tidsbaserat filter som bygger på tidsseriedata.
- Optimerad nedtryckning för strukturdatatypen.
- Optimerad kostnad och minneshantering för matriser och kartdatatyper.
- Inkrementell bearbetning med ögonblicksbilder.
- Ett beständigt dataformat.
+++

### Kan inloggningar begränsas till vissa aspekter av frågetjänsten eller är det en&quot;allt eller ingenting&quot;-lösning?

+++Svar
Frågetjänsten är en&quot;all eller ingenting&quot;-lösning. Det går inte att ge partiell åtkomst.
+++

### Kan jag begränsa vilka data Query Service kan använda, eller har den bara tillgång till hela Adobe Experience Platform datasjön?

+++Svar
Ja, du kan begränsa frågan till datauppsättningar med skrivskyddad åtkomst.
+++

### Vilka andra alternativ finns det för att begränsa vilka data som kan nås via frågetjänsten?

+++Svar
Det finns tre sätt att begränsa åtkomsten. De är följande:

- Använd bara SELECT-programsatser och ge datauppsättningar skrivskyddad åtkomst. Tilldela även behörigheten Hantera fråga.
- Använd SELECT/INSERT/CREATE-programsatser och ge datauppsättningar skrivbehörighet. Tilldela även behörigheten för frågehantering.
- Använd ett integrationskonto med föregående förslag ovan och tilldela frågeintegrationsbehörigheten.

+++

### När data har returnerats av Query Service, finns det några kontroller som Experience Platform kan köra för att säkerställa att inga skyddade data har returnerats?

- Frågetjänsten stöder attributbaserad åtkomstkontroll. Du kan begränsa åtkomsten till data på kolumn-/lövnivå och/eller strukturnivå. Mer information om attributbaserad åtkomstkontroll finns i dokumentationen.

### Kan jag ange ett SSL-läge för anslutningen till en tredjepartsklient? Kan jag till exempel använda verify-full med Power BI?

+++Svar
Ja, SSL-lägen stöds. I [dokumentationen för SSL-lägen](./clients/ssl-modes.md) finns en beskrivning av de olika SSL-lägena som är tillgängliga och vilken skyddsnivå de erbjuder.
+++

### Använder vi TLS 1.2 för alla anslutningar från Power BI-klienter för att fråga tjänsten?

+++Svar
Ja. Data-in-Transition är alltid HTTPS-kompatibel. Den version som stöds för närvarande är TLS1.2.
+++

### Använder en anslutning som görs på port 80 fortfarande https?

+++Svar
Ja, en anslutning som görs på port 80 använder fortfarande SSL. Du kan också använda port 5432.
+++

### Kan jag styra åtkomsten till specifika datauppsättningar och kolumner för en viss anslutning? Hur är detta konfigurerat?

+++Svar
Ja, attributbaserad åtkomstkontroll används om den har konfigurerats. Mer information finns i [attributbaserad åtkomstkontroll](../access-control/abac/overview.md).
+++

### Stöder frågetjänsten kommandot INSERT OVERWRITE INTO?

+++Svar
Nej, frågetjänsten stöder inte kommandot INSERT OVERWRITE INTO.
+++

### Hur ofta uppdateras användningsdata på kontrollpanelen för licensanvändning för Data Distiller Compute-timmar?

+++Svar
Kontrollpanelen för licensanvändning för datavärden i Distiller uppdateras fyra gånger om dagen, var sjätte timme.
+++

### Kan jag använda kommandot CREATE VIEW utan åtkomst till Data Distiller?

+++Svar
Ja, du kan använda kommandot `CREATE VIEW` utan åtkomst till Data Distiller. Det här kommandot ger en logisk vy av data men skriver inte tillbaka dem till datasjön.
+++

### Kan jag använda anonyma block i DbVisualizer?

+++Svar
Ja. Vissa tredjepartsklienter, som DbVisualizer, kan kräva en separat identifierare före och efter ett SQL-block för att ange att en del av ett skript ska hanteras som en enda sats. Mer information finns i [anonym blockdokumentation](./key-concepts/anonymous-block.md) eller i [den officiella DbVisualizer-dokumentationen](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsinganSQLDialect).
+++

## Data Distiller {#data-distiller}

### Hur spåras användningen av Data Distiller-licenser och var kan jag se den här informationen?

+++Svar\
Huvudmåttet som används för att spåra batchfrågeanvändning är beräkningstiden. Du har tillgång till den här informationen och din nuvarande förbrukning via kontrollpanelen för [licensanvändning](../dashboards/guides/license-usage.md).
+++

### Vad är en Compute Hour?

+++Svar\
Beräkningstimmar är det tidsmått som Query Service-motorerna tar för att läsa, bearbeta och skriva data tillbaka till datasjön när en batchfråga körs.
+++

### Hur mäts Beräkna timmar?

+++Svar\
Beräkna timmar mäts kumulativt över alla dina godkända sandlådor.
+++

### Varför märker jag ibland en variation i konsumtionen av Beräkna timmar även när jag kör samma fråga i följd?

+++Svar\
Beräkningstimmar för en fråga kan fluktuera på grund av flera faktorer. Dessa omfattar den bearbetade datavolymen, komplexiteten hos omformningsåtgärder i SQL-frågan och så vidare. Frågetjänsten skalar klustret baserat på ovanstående parametrar för varje fråga, vilket kan leda till skillnader i beräkningstimmar.
+++

### Är det normalt att lägga märke till en minskning av beräkningstimmar när jag kör samma fråga med samma data under en lång tid? Varför händer detta?

+++Svar\
Infrastruktur för serverdelen har ständigt förbättrats för att optimera användningen av timmor för beräkning och bearbetningstid. Det innebär att du kan märka att prestandaförbättringarna förändras över tid.
+++

## Användargränssnitt för frågor

### &quot;Skapa fråga&quot; fastnar &quot;Anslutningen initieras..&quot; när du försöker ansluta till frågetjänsten. Hur åtgärdar jag problemet?

+++Svar
Om frågan &quot;Skapa fråga&quot; har fastnat på &quot;Initialiserar anslutning..&quot; är detta troligen ett anslutnings- eller sessionsproblem. Uppdatera webbläsaren om du använder Experience Platform-gränssnittet och försök igen.
+++

## Datauppsättningsexempel

### Kan jag skapa exempel på en systemdatauppsättning?

+++Svar
Nej. Skrivbehörigheter är begränsade för systemdatauppsättningar så du kan inte skapa exempel.
+++

## Exportera data {#exporting-data}

I det här avsnittet finns information om hur du exporterar data och begränsningar.

### Finns det något sätt att extrahera data från frågetjänsten efter frågebearbetning och spara resultaten i en CSV-fil? {#export-csv}

+++Svar
Ja. Data kan extraheras från frågetjänsten och det finns även ett alternativ för att lagra resultaten i CSV-format via ett SQL-kommando.

Det finns två sätt att spara resultatet av en fråga när du använder en PSQL-klient. Du kan använda kommandot `COPY TO` eller skapa en sats med följande format:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Vägledning om hur `COPY TO` command](./sql/syntax.md#copy) används finns i referensdokumentationen för SQL-syntaxen.
+++

### Kan jag extrahera innehållet i den slutliga datauppsättningen som har importerats via CTAS-frågor (förutsatt att det är större mängder data som Terabytes)?

+++Svar
Nej. Det finns för närvarande ingen funktion för extrahering av inkapslade data.
+++

### Varför returnerar inte Analytics-dataanslutningen data?

+++Svar
En vanlig orsak till det här problemet är att fråga efter tidsseriedata utan tidsfilter. Exempel:

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

## SQL-syntax

### Stöds MERGE INTO av Data Distiller eller Query Service?

+++Svar
SQL-konstruktionen MERGE INTO stöds inte av Data Distiller eller Query Service.
+++

## ITAS-frågor

### Vad är ITAS-frågor?

+++Svar
INSERT INTO-frågor kallas ITAS-frågor. Observera att CREATE TABLE-frågor kallas för CTAS-frågor.
+++

## Tredjepartsverktyg {#third-party-tools}

I det här avsnittet finns information om hur du använder verktyg från tredje part som PSQL och Power BI.

### Kan jag ansluta frågetjänsten till ett verktyg från tredje part?

+++Svar
Ja, du kan ansluta flera tredjepartsklienter till Query Service. I dokumentationen finns [fullständig information om de tillgängliga klienterna och hur du ansluter dem till frågetjänsten](./clients/overview.md).
+++

### Finns det något sätt att ansluta frågetjänsten en gång för kontinuerlig användning med ett verktyg från tredje part?

+++Svar
Ja, klientdatorer från tredje part kan anslutas till Query Service via en engångsinstallation av ej förfallande autentiseringsuppgifter. Autentiseringsuppgifter som inte förfaller kan genereras av en behörig användare och tas emot i en JSON-fil som automatiskt hämtas till den lokala datorn. Fullständig [vägledning om hur du skapar och hämtar ej förfallande autentiseringsuppgifter](./ui/credentials.md#non-expiring-credentials) finns i dokumentationen.
+++

### Varför fungerar inte mina inloggningsuppgifter som inte förfaller?

+++Svar
Värdet för autentiseringsuppgifter som inte förfaller är sammanfogade argument från `technicalAccountID` och `credential` från JSON-konfigurationsfilen. Lösenordsvärdet har formatet: `{{technicalAccountId}:{credential}}`.
Mer information om hur du [ansluter till externa klienter med autentiseringsuppgifter finns i dokumentationen ](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### Vilken typ av SQL-redigerare från tredje part kan jag ansluta till Query Service Editor?

+++Svar
Alla SQL-redigerare från tredje part som är PSQL- eller [!DNL Postgres]-klientkompatibla kan anslutas till Query Service Editor. I dokumentationen för [att ansluta klienter till frågetjänsten](./clients/overview.md) finns en lista med tillgängliga instruktioner.
+++

### Kan jag ansluta Power BI-verktyget till Query Service?

+++Svar
Ja, du kan ansluta Power BI till Query Service. I dokumentationen finns [instruktioner om hur du ansluter Power BI-datorprogrammet till frågetjänsten](./clients/power-bi.md).
+++

### Varför tar det lång tid att läsa in kontrollpanelerna när de är anslutna till Query Service?

+++Svar
När systemet är anslutet till frågetjänsten är det anslutet till en interaktiv motor eller batchbearbetningsmotor. Detta kan leda till längre inläsningstider för att återspegla de bearbetade data.

Om du vill förbättra svarstiderna för dina instrumentpaneler bör du implementera en Business Intelligence (BI)-server som ett cachelagringslager mellan Query Service och BI-verktyg. I allmänhet har de flesta BI-verktyg ett extra erbjudande för en server.

Syftet med att lägga till cacheserverlagret är att cachelagra data från frågetjänsten och använda samma för kontrollpaneler för att snabba upp svaret. Detta är möjligt eftersom resultaten för frågor som körs cachelagras i BI-servern varje dag. Cachelagringsservern skickar sedan dessa resultat till alla användare med samma fråga för att minska fördröjningen. Se dokumentationen för verktyget eller tredjepartsverktyget som du använder för att få mer information om den här konfigurationen.
+++

### Är det möjligt att komma åt Query Service med anslutningsverktyget pgAdmin?

+++Svar
Nej, pgAdmin-anslutningen stöds inte. En [lista över tillgängliga tredjepartsklienter och instruktioner om hur du ansluter dem till frågetjänsten](./clients/overview.md) finns i dokumentationen.
+++

## PostgreSQL API-fel {#postgresql-api-errors}

Följande tabell innehåller PSQL-felkoder och deras möjliga orsaker.

| Felkod | Anslutningstillstånd | Beskrivning | Möjlig orsak |
|------------|---------------------------|-------------|----------------|
| **08P01** | N/A | Meddelandetypen stöds inte | Meddelandetypen stöds inte |
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
| **42501** | DROP TABLE Query | Släpptabellen har inte skapats av frågetjänsten | Tabellen som tas bort skapades inte av frågetjänsten med programsatsen `CREATE TABLE` |
| **42501** | DROP TABLE Query | Tabellen har inte skapats av den autentiserade användaren | Tabellen som tas bort skapades inte av den inloggade användaren |
| **42P01** | DROP TABLE Query | Tabellen hittades inte | Det gick inte att hitta tabellen som angavs i frågan |
| **42P12** | DROP TABLE Query | Ingen tabell hittades för `dbName`: kontrollera `dbName` | Inga tabeller hittades i den aktuella databasen |

### Varför fick jag en 58000-felkod när jag använde metoden history_meta() i min tabell?

+++Svar
Metoden `history_meta()` används för att komma åt en ögonblicksbild från en datauppsättning. Tidigare, om du skulle köra en fråga på en tom datauppsättning i Azure Data Lake Storage (ADLS), skulle du få en felkod på 58000 som anger att datauppsättningen inte finns. Ett exempel på det gamla systemfelet visas nedan.

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
