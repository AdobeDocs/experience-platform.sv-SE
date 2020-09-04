---
keywords: Experience Platform;home;popular topics;query service;Query service;sql syntax;sql;ctas;CTAS;Create table as select
solution: Experience Platform
title: SQL-syntax
topic: syntax
description: Det här dokumentet visar SQL-syntax som stöds av Query Service.
translation-type: tm+mt
source-git-commit: 041165f501d35b811202362b524523b103d18113
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 0%

---


# SQL-syntax

[!DNL Query Service] ger möjlighet att använda ANSI SQL-standard för satser och andra begränsade kommandon `SELECT` . I det här dokumentet visas SQL-syntax som stöds av [!DNL Query Service].

## Definiera en SELECT-fråga

Följande syntax definierar en `SELECT` fråga som stöds av [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

där `from_item` kan vara något av följande:

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

och `grouping_element` kan vara något av följande:

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

och `with_query` är:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### WHERE ILIKE-sats

Nyckelordet ILIKE kan användas i stället för LIKE för att skapa matchningar för WHERE-satsen i SELECT-frågans skiftlägeskänsliga.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

Logiken i LIKE- och ILIKE-klausulerna är följande:
- ```WHERE condition LIKE pattern```, ```~~``` motsvarar mönster
- ```WHERE condition NOT LIKE pattern```, ```!~~``` motsvarar mönster
- ```WHERE condition ILIKE pattern```, ```~~*``` motsvarar mönster
- ```WHERE condition NOT ILIKE pattern```, ```!~~*``` motsvarar mönster


#### Exempel

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Returnerar kunder med namn som börjar på A eller a.

## FÖRENINGAR

En `SELECT` fråga som använder kopplingar har följande syntax:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNION, INTERSECT, and EXCEPT

Programsatserna `UNION`, `INTERSECT`och `EXCEPT` stöds för att kombinera eller exkludera liknande rader från två eller flera tabeller:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## SKAPA TABELL SOM MARKERAD

Följande syntax definierar en `CREATE TABLE AS SELECT` (CTAS)-fråga som stöds av [!DNL Query Service]:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title') ] AS (select_query)
```

var `target_schema_title` är XDM-schemats titel. Använd bara den här satsen om du vill använda ett befintligt XDM-schema för den nya datauppsättningen som skapas av CTAS-frågan.

och `select_query` är en `SELECT` -programsats vars syntax definieras ovan i det här dokumentet.


### Exempel

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Observera att för en viss CTAS-fråga:

1. Programsatsen `SELECT` måste ha ett alias för de sammanställningsfunktioner som `COUNT`, `SUM`, `MIN`och så vidare.
2. Programsatsen `SELECT` kan tillhandahållas med eller utan parenteser ().

## INFOGA I

Följande syntax definierar en `INSERT INTO` fråga som stöds av [!DNL Query Service]:

```sql
INSERT INTO table_name select_query
```

där `select_query` är en `SELECT` -programsats vars syntax definieras ovan i det här dokumentet.

### Exempel

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Observera att för en given INSERT INTO-fråga:

1. Programsatsen `SELECT` FÅR INTE omslutas av parenteser ().
2. Schemat för resultatet av `SELECT` programsatsen måste överensstämma med schemat i tabellen som definierats i `INSERT INTO` programsatsen .

### DROP TABLE

Släpp en tabell och ta bort katalogen som är associerad med tabellen från filsystemet om det inte är en EXTERN tabell. Om tabellen som ska tas bort inte finns inträffar ett undantag.

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Parametrar

- `IF EXISTS`: Om tabellen inte finns händer ingenting
- `TEMP`: Tillfälligt register

## SKAPA VY

Följande syntax definierar en `CREATE VIEW` fråga som stöds av [!DNL Query Service]:

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

Var `view_name` är namnet på den vy som ska skapas och `select_query` är en `SELECT` -programsats vars syntax definieras ovan i det här dokumentet.

Exempel:

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### DROP VIEW

Följande syntax definierar en `DROP VIEW` fråga som stöds av [!DNL Query Service]:

```sql
DROP VIEW [IF EXISTS] view_name
```

Var `view_name` är namnet på vyn som ska tas bort

Exempel:

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL-kommandon

### ANGE

Ange en egenskap, returnera värdet för en befintlig egenskap eller visa alla befintliga egenskaper. Om ett värde anges för en befintlig egenskapsnyckel åsidosätts det gamla värdet.

```sql
SET property_key [ To | =] property_value
```

Om du vill returnera värdet för en inställning använder du `SHOW [setting name]`.

## PostgreSQL-kommandon

### BÖRJA

Det här kommandot tolkas och det slutförda kommandot skickas tillbaka till klienten. Detta är samma som `START TRANSACTION` kommandot.

```sql
BEGIN [ TRANSACTION ]
```

#### Parametrar

- `TRANSACTION`: Valfria nyckelord. Lyssnar, ingen åtgärd vidtas angående detta.

### STÄNG

`CLOSE` frigör resurser som är kopplade till en öppen markör. När markören har stängts tillåts inga efterföljande åtgärder på den. En markör bör stängas när den inte längre behövs.

```sql
CLOSE { name }
```

#### Parametrar

- `name`: namnet på en öppen markör som ska stängas.

### implementera

Ingen åtgärd vidtas i [!DNL Query Service] som svar på implementeringstransaktionssatsen.

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### Parametrar

- `WORK`
- `TRANSACTION`: Valfria nyckelord. De har ingen effekt.

### DEALOCATE

Använd `DEALLOCATE` för att frigöra en tidigare förberedd SQL-sats. Om du inte uttryckligen frigör en förberedd sats, frigörs den när sessionen avslutas.

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Parametrar

- `Prepare`: Nyckelordet ignoreras.
- `name`: Namnet på den förberedda sats som ska frigöras.
- `ALL`: Frigör alla förberedda satser.

### DEKLARERA

`DECLARE` gör att användaren kan skapa markörer, som kan användas för att hämta ett litet antal rader i taget från en större fråga. När markören har skapats hämtas rader från den med `FETCH`.

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Parametrar

- `name`: Namnet på den markör som ska skapas.
- `WITH HOLD`: Anger att markören kan fortsätta att användas efter att transaktionen som den skapades har genomförts.
- `query`: Ett `SELECT` eller `VALUES` kommando som innehåller de rader som markören ska returnera.

### KÖR

`EXECUTE` används för att köra en tidigare förberedd sats. Eftersom förberedda satser bara finns under en session måste den förberedda satsen ha skapats av en `PREPARE` -sats som kördes tidigare i den aktuella sessionen.

Om programsatsen som `PREPARE` skapade programsatsen angav vissa parametrar måste en kompatibel uppsättning parametrar skickas till `EXECUTE` programsatsen, annars uppstår ett fel. Observera att förberedda satser (till skillnad från funktioner) inte överläses baserat på parametrarnas typ eller antal. Namnet på en förberedd sats måste vara unikt i en databassession.

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Parametrar

- `name`: Namnet på den förberedda sats som ska köras.
- `parameter`: Det faktiska värdet för en parameter till den förberedda programsatsen. Det här måste vara ett uttryck som ger ett värde som är kompatibelt med den här parameterns datatyp, vilket bestämdes när den förberedda satsen skapades.

### FÖRKLARA

Det här kommandot visar den körningsplan som PostgreSQL-plannern genererar för den angivna satsen. Körningsplanen visar hur tabellerna som programsatsen refererar till skannas - med vanlig sekventiell skanning, indexskanning och så vidare - och om flera tabeller refereras, vilka kopplingsalgoritmer som används för att sammanfoga de nödvändiga raderna från varje indatatabell.

Den mest kritiska delen av visningen är den uppskattade kostnaden för satskörning, som är planeringens gissning på hur lång tid det tar att köra kontoutdraget (mäts i kostnadsenheter som är godtyckliga, men vanligtvis är disksideshämtningar). Faktiskt visas två tal: startkostnaden innan den första raden kan returneras och totalkostnaden för att returnera alla rader. För de flesta frågor är den totala kostnaden det som är viktigast, men i sammanhang som en underfråga i EXISTS väljer planeraren den minsta startkostnaden i stället för den minsta totalkostnaden (eftersom köraren slutar efter att ha hämtat en rad i alla fall). Om du begränsar antalet rader som ska returneras med en `LIMIT` sats, skapar planeraren en lämplig interpolation mellan slutpunktskostnaderna för att beräkna vilken plan som faktiskt är den billigaste.

Alternativet `ANALYZE` gör att satsen körs, inte bara planerad. Sedan läggs statistik om faktisk körtid till i visningen, inklusive den totala förflutna tid som förbrukats i varje plannod (i millisekunder) och det totala antalet rader som returneras. Detta är användbart för att se om planeringens uppskattningar är i närheten av verkligheten.

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Parametrar

- `ANALYZE`: Utför kommandot och visa faktiska körtider och annan statistik. Parametern är som standard `FALSE`.
- `FORMAT`: Ange utdataformatet, som kan vara TEXT, XML, JSON eller YAML. Utdata som inte är text innehåller samma information som textutdataformatet, men är enklare att tolka i program. Parametern är som standard `TEXT`.
- `statement`: Alla `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`eller `CREATE MATERIALIZED VIEW AS` -programsatser vars körningsplan du vill se.

>[!IMPORTANT]
>
>Kom ihåg att programsatsen faktiskt körs när alternativet `ANALYZE` används. Även om utdata som `EXPLAIN` returneras `SELECT` ignoreras, inträffar andra biverkningar av satsen som vanligt.

#### Exempel

Så här visar du planen för en enkel fråga i en tabell med en enda `integer` kolumn och 10 000 rader:

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` hämtar rader med hjälp av en markör som skapats tidigare.

En markör har en associerad position som används av `FETCH`. Markörpositionen kan vara före den första raden i frågeresultatet, på en viss resultatrad eller efter den sista resultatraden. När du skapar en markör placeras den före den första raden. När du har hämtat några rader placeras markören på den rad som senast hämtades. Om du `FETCH` inte längre kommer till den sista raden, kommer markören att vara kvar efter den sista raden. Om det inte finns någon sådan rad returneras ett tomt resultat och markörerna placeras före den första raden eller efter den sista raden.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Parametrar

- `num_of_rows`: En heltalskonstant som kan vara signerad och som bestämmer platsen eller antalet rader som ska hämtas.
- `cursor_name`: En öppen markörs namn.

### FÖRBEREDA

`PREPARE` skapar en förberedd programsats. En förberedd programsats är ett objekt på serversidan som kan användas för att optimera prestanda. När `PREPARE` programsatsen körs tolkas, analyseras och skrivs om den angivna programsatsen. När ett `EXECUTE` kommando sedan utfärdas planeras och körs den förberedda satsen. Denna arbetsfördelning undviker repetitivt analysarbete, samtidigt som körningsplanen kan vara beroende av de angivna parametervärdena.

Förförberedda satser kan innehålla parametrar, värden som ersätts med programsatsen när den körs. När du skapar den förberedda programsatsen ska du referera till parametrar per position, med $1, $2 och så vidare. Du kan också ange en motsvarande lista med parameterdatatyper. När en parameters datatyp inte har angetts eller deklarerats som okänd, härleds typen från kontexten där parametern först refereras, om det är möjligt. När du kör satsen anger du de faktiska värdena för de här parametrarna i `EXECUTE` -satsen.

Förförberedda satser varar bara så länge den aktuella databassessionen varar. När sessionen avslutas, glöms den förberedda programsatsen bort, så den måste återskapas innan den används igen. Det innebär också att en enda förberedd sats inte kan användas av flera samtidiga databasklienter. Varje klient kan dock skapa en egen förberedd sats som ska användas. Förförberedda satser kan rensas manuellt med hjälp av `DEALLOCATE` kommandot.

Förberedda satser kan ha den största prestandafördelen när en session används för att köra ett stort antal liknande satser. Prestandaskillnaden är särskilt stor om programsatserna är komplexa att planera eller skriva om, till exempel om frågan innehåller en join från många tabeller eller kräver tillämpning av flera regler. Om programsatsen är relativt enkel att planera och skriva om men relativt dyr att utföra, är prestandafördelen med förberedda programsatser mindre märkbar.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Parametrar

- `name`: Ett godtyckligt namn som ges till den här förberedda satsen. Den måste vara unik i en enda session och används sedan för att köra eller frigöra en tidigare förberedd programsats.
- `data-type`: Datatypen för en parameter till den förberedda programsatsen. Om datatypen för en viss parameter är ospecificerad eller har angetts som okänd, härleds den från kontexten där parametern först refereras. Om du vill referera till parametrarna i den förberedda satsen använder du $1, $2 och så vidare.


### ROLLBACK

`ROLLBACK` återställer den aktuella transaktionen och gör att alla uppdateringar som gjorts av transaktionen ignoreras.

```sql
ROLLBACK [ WORK ]
```

#### Parametrar

- `WORK`

### MARKERA I

`SELECT INTO` skapar en ny tabell och fyller den med data som beräknas av en fråga. Data returneras inte till klienten, som de är med en normal `SELECT`. Den nya tabellens kolumner har de namn och datatyper som är associerade med utdatakolumnerna för `SELECT`.

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

#### Parametrar

- `TEMPORARAY` eller `TEMP`: Om det anges skapas tabellen som ett temporärt register.
- `UNLOGGED:` om det anges skapas tabellen som en ologgad tabell.
- `new_table` Namnet (eventuellt schemakvalificerat) på tabellen som ska skapas.

#### Exempel

Skapa en ny tabell `films_recent` som endast består av de senaste posterna från tabellen `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### VISA

`SHOW` visar den aktuella inställningen för körningsparametrar. Dessa variabler kan ställas in med `SET` programsatsen, genom att redigera konfigurationsfilen postgresql.conf, via `PGOPTIONS` miljövariabeln (när libpq eller ett libpq-baserat program används) eller via kommandoradsflaggor när postgres-servern startas.

```sql
SHOW name
```

#### Parametrar

- `name`:
   - `SERVER_VERSION`: Visar serverns versionsnummer.
   - `SERVER_ENCODING`: Visar kodning av teckenuppsättning på serversidan. För närvarande kan den här parametern visas men inte anges eftersom kodningen bestäms när databasen skapas.
   - `LC_COLLATE`: Visar databasens språkområdesinställning för sortering (textordning). För närvarande kan den här parametern visas men inte anges eftersom inställningen bestäms när databasen skapas.
   - `LC_CTYPE`: Visar databasens språkområdesinställning för teckenklassificering. För närvarande kan den här parametern visas men inte anges eftersom inställningen bestäms när databasen skapas.
      `IS_SUPERUSER`: True if the current role has superuser privileges.
- `ALL`: Visa värdena för alla konfigurationsparametrar med beskrivningar.

#### Exempel

Visa parameterns aktuella inställning `DateStyle`

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### STARTA TRANSAKTION

Det här kommandot tolkas och skickar tillbaka det slutförda kommandot till klienten. Detta är samma som `BEGIN` kommandot.

```sql
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### COPY

Med det här kommandot dumpas utdata från en SELECT-fråga till en angiven plats. Användaren måste ha åtkomst till den här platsen för att det här kommandot ska lyckas.

```sql
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>Den fullständiga utdatasökvägen `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`