---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Frågetjänst;SQL-syntax;sql;ctas;CTAS;Skapa tabell som markerad
solution: Experience Platform
title: SQL-syntax i frågetjänst
topic: syntax
description: I det här dokumentet visas SQL-syntax som stöds av Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 78707257c179101b29e68036bf9173d74f01e03a
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---


# SQL-syntax i Query Service

Med Adobe Experience Platform Query Service kan du använda ANSI SQL av standardtyp för `SELECT`-satser och andra begränsade kommandon. Det här dokumentet innehåller den SQL-syntax som stöds av [!DNL Query Service].

## SELECT-frågor {#select-queries}

Följande syntax definierar en `SELECT`-fråga som stöds av [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

där `from_item` kan vara ett av följande alternativ:

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

och `grouping_element` kan vara något av följande alternativ:

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

och `with_query` är:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

Följande underavsnitt innehåller information om ytterligare satser som du kan använda i dina frågor, förutsatt att de följer det format som beskrivs ovan.

### SNAPSHOT-sats

Den här satsen kan användas för att stegvis läsa data i en tabell baserat på ID:n för ögonblicksbilder. Ett ID för en ögonblicksbild är en kontrollpunktsmarkör som representeras av ett Long-typnummer som används på en datarintabell varje gång data skrivs till den. Satsen `SNAPSHOT` kopplar sig till den registerrelation som den används bredvid.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Exempel

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Observera att en `SNAPSHOT`-sats fungerar med en tabell eller ett tabellalias men inte ovanpå en underfråga eller vy. En `SNAPSHOT`-sats fungerar var som helst där en `SELECT`-fråga för en tabell kan tillämpas.

Dessutom kan du använda `HEAD` och `TAIL` som särskilda förskjutningsvärden för ögonblicksbildssatser. Om du använder `HEAD` refereras en förskjutning före den första ögonblicksbilden, medan `TAIL` refererar till en förskjutning efter den sista ögonblicksbilden.

### WHERE-sats

Som standard är matchningar som skapats med en `WHERE`-sats i en `SELECT`-fråga skiftlägeskänsliga. Om du vill att matchningar ska vara skiftlägeskänsliga kan du använda nyckelordet `ILIKE` i stället för `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

Logiken i LIKE- och ILIKE-klausulerna förklaras i följande tabell:

| Klausul | Operatör |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**Exempel**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Den här frågan returnerar kunder med namn som börjar på A eller a.

### GÅ MED

En `SELECT`-fråga som använder kopplingar har följande syntax:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT, and EXCEPT

Satserna `UNION`, `INTERSECT` och `EXCEPT` används för att kombinera eller exkludera liknande rader från två eller flera tabeller:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### SKAPA TABELL SOM MARKERAD

Följande syntax definierar en `CREATE TABLE AS SELECT`-fråga (CTAS):

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**Parametrar**

- `schema`: Titeln på XDM-schemat. Använd bara den här satsen om du vill använda ett befintligt XDM-schema för den nya datauppsättningen som skapas av CTAS-frågan.
- `rowvalidation`: (Valfritt) Anger om användaren vill validera radnivån för alla nya batchar som hämtas för den nya datauppsättningen. Standardvärdet är `true`.
- `select_query`: En  `SELECT` programsats. Syntaxen för `SELECT`-frågan finns i [SELECT-frågeavsnittet](#select-queries).

**Exempel**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>Programsatsen `SELECT` måste ha ett alias för de sammanställningsfunktioner som `COUNT`, `SUM`, `MIN` och så vidare. Dessutom kan `SELECT`-satsen anges med eller utan parenteser (). Du kan ange en `SNAPSHOT`-sats för att läsa inkrementella deltas i måltabellen.

## INFOGA I

Kommandot `INSERT INTO` definieras så här:

```sql
INSERT INTO table_name select_query
```

**Parametrar**

- `table_name`: Namnet på tabellen som du vill infoga frågan i.
- `select_query`: En  `SELECT` programsats. Syntaxen för `SELECT`-frågan finns i [SELECT-frågeavsnittet](#select-queries).

**Exempel**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> `SELECT`-satsen **får inte** omges av parenteser (). Schemat för resultatet av `SELECT`-satsen måste dessutom överensstämma med schemat för tabellen som definieras i `INSERT INTO`-satsen. Du kan ange en `SNAPSHOT`-sats för att läsa inkrementella deltas i måltabellen.

## DROP TABLE

Kommandot `DROP TABLE` släpper en befintlig tabell och tar bort katalogen som är associerad med tabellen från filsystemet om den inte är en extern tabell. Om tabellen inte finns inträffar ett undantag.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Parametrar**

- `IF EXISTS`: Om detta anges genereras inget undantag om tabellen inte  **** innehåller någon text.

## SKAPA VY

Följande syntax definierar en `CREATE VIEW`-fråga:

```sql
CREATE VIEW view_name AS select_query
```

**Parametrar**

- `view_name`: Namnet på den vy som ska skapas.
- `select_query`: En  `SELECT` programsats. Syntaxen för `SELECT`-frågan finns i [SELECT-frågeavsnittet](#select-queries).

**Exempel**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

Följande syntax definierar en `DROP VIEW`-fråga:

```sql
DROP VIEW [IF EXISTS] view_name
```

**Parameter**

- `IF EXISTS`: Om detta anges genereras inget undantag om vyn  **** inte innehåller någon text.
- `view_name`: Namnet på den vy som ska tas bort.

**Exempel**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL-kommandon

Underavsnittet nedan beskriver Spark SQL-kommandon som stöds av Query Service.

### ANGE

Kommandot `SET` anger en egenskap och returnerar antingen värdet för en befintlig egenskap eller visar alla befintliga egenskaper. Om ett värde anges för en befintlig egenskapsnyckel åsidosätts det gamla värdet.

```sql
SET property_key = property_value
```

**Parametrar**

- `property_key`: Namnet på den egenskap som du vill visa eller ändra.
- `property_value`: Värdet som du vill att egenskapen ska anges som.

Om du vill returnera värdet för en inställning använder du `SET [property key]` utan `property_value`.

## PostgreSQL-kommandon

Underavsnitten nedan täcker de PostgreSQL-kommandon som stöds av Query Service.

### BÖRJA

Kommandot `BEGIN`, eller alternativt kommandot `BEGIN WORK` eller `BEGIN TRANSACTION`, initierar ett transaktionsblock. Alla programsatser som infogas efter kommandot begin körs i en enda transaktion tills ett explicit COMMIT- eller ROLLBACK-kommando anges. Det här kommandot är samma som `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### STÄNG

Kommandot `CLOSE` frigör resurser som är kopplade till en öppen markör. När markören har stängts tillåts inga efterföljande åtgärder på den. En markör bör stängas när den inte längre behövs.

```sql
CLOSE name
CLOSE ALL
```

Om `CLOSE name` används representerar `name` namnet på en öppen markör som måste stängas. Om `CLOSE ALL` används stängs alla öppna markörer.

### DEALOCATE

Med kommandot `DEALLOCATE` kan du frigöra en tidigare förberedd SQL-sats. Om du inte uttryckligen frigör en förberedd sats, frigörs den när sessionen avslutas. Mer information om förberedda satser finns i avsnittet [PREPARE command](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Om `DEALLOCATE name` används representerar `name` namnet på den förberedda satsen som behöver frigöras. Om `DEALLOCATE ALL` används kommer alla förberedda satser att frigöras.

### DEKLARERA

Med kommandot `DECLARE` kan en användare skapa en markör som kan användas för att hämta ett litet antal rader från en större fråga. När markören har skapats hämtas rader från den med `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

**Parametrar**

- `name`: Namnet på den markör som ska skapas.
- `query`: Ett  `SELECT` eller  `VALUES` kommando som innehåller de rader som markören ska returnera.

### KÖR

Kommandot `EXECUTE` används för att köra en tidigare förberedd sats. Eftersom förberedda satser bara finns under en session måste den förberedda satsen ha skapats av en `PREPARE`-sats som kördes tidigare i den aktuella sessionen. Mer information om hur du använder förberedda satser finns i avsnittet [`PREPARE` command](#prepare).

Om `PREPARE`-satsen som skapade satsen angav vissa parametrar måste en kompatibel uppsättning parametrar skickas till `EXECUTE`-satsen. Om de här parametrarna inte skickas visas ett fel.

```sql
EXECUTE name [ ( parameter ) ]
```

**Parametrar**

- `name`: Namnet på den förberedda sats som ska köras.
- `parameter`: Det faktiska värdet för en parameter till den förberedda programsatsen. Det här måste vara ett uttryck som ger ett värde som är kompatibelt med den här parameterns datatyp, vilket bestämdes när den förberedda satsen skapades.  Om det finns flera parametrar för den förberedda programsatsen avgränsas de med kommatecken.

### FÖRKLARA

Kommandot `EXPLAIN` visar körningsplanen för den angivna programsatsen. Körningsplanen visar hur tabellerna som programsatsen refererar till skannas.  Om flera tabeller refereras visas vilka kopplingsalgoritmer som används för att sammanfoga de rader som krävs från varje indatatabell.

```sql
EXPLAIN option statement
```

Där `option` kan vara något av:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Parametrar**

- `ANALYZE`: Om det  `option` finns  `ANALYZE`en lista visas körtider och annan statistik.
- `FORMAT`: Om filen  `option` innehåller  `FORMAT`anger den utdataformatet, som kan vara  `TEXT` eller  `JSON`. Utdata som inte är text innehåller samma information som textutdataformatet, men är enklare att tolka i program. Parametern är som standard `TEXT`.
- `statement`: Alla  `SELECT`,  `INSERT`,  `UPDATE`,  `DELETE`,  `VALUES`,  `EXECUTE`,  `DECLARE`,  `CREATE TABLE AS` eller  `CREATE MATERIALIZED VIEW AS` programsatser vars körningsplan du vill se.

>[!IMPORTANT]
>
>Kom ihåg att satsen faktiskt körs när alternativet `ANALYZE` används. Även om `EXPLAIN` ignorerar utdata som returneras av en `SELECT`, inträffar andra biverkningar av satsen som vanligt.

**Exempel**

I följande exempel visas planen för en enkel fråga i en tabell med en enda `integer`-kolumn och 10 000 rader:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

Kommandot `FETCH` hämtar rader med en markör som skapats tidigare.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Parametrar**

- `num_of_rows`: Antalet rader som ska hämtas.
- `cursor_name`: Namnet på den markör som du hämtar information från.

### FÖRBERED {#prepare}

Med kommandot `PREPARE` kan du skapa en förberedd programsats. En förberedd programsats är ett objekt på serversidan som kan användas för att mallatisera liknande SQL-programsatser.

Förberedda programsatser kan innehålla parametrar, som är värden som ersätts med programsatsen när den körs. Parametrar refereras efter position, med $1, $2 osv., när förberedda satser används.

Du kan också ange en lista med parameterdatatyper. Om en parameters datatyp inte finns med i listan kan typen härledas från kontexten.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Parametrar**

- `name`: Namnet på den förberedda satsen.
- `data_type`: Datatyperna för den förberedda satsens parametrar. Om en parameters datatyp inte finns med i listan kan typen härledas från kontexten. Om du behöver lägga till flera datatyper kan du lägga till dem i en kommaseparerad lista.

### ROLLBACK

Kommandot `ROLLBACK` ångrar den aktuella transaktionen och tar bort alla uppdateringar som gjorts av transaktionen.

```sql
ROLLBACK
ROLLBACK WORK
```

### MARKERA I

Kommandot `SELECT INTO` skapar en ny tabell och fyller den med data som beräknas av en fråga. Data returneras inte till klienten, vilket är fallet med ett vanligt `SELECT`-kommando. Den nya tabellens kolumner har de namn och datatyper som är associerade med utdatakolumnerna för kommandot `SELECT`.

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

**Parametrar**

Mer information om SELECT-frågeparametrarna finns i [SELECT query section](#select-queries). I det här avsnittet visas endast parametrar som är exklusiva för kommandot `SELECT INTO`.

- `TEMPORARY` eller  `TEMP`: En valfri parameter. Om det anges blir det register som skapas ett temporärt register.
- `UNLOGGED`: En valfri parameter. Om det anges kommer tabellen som skapas att vara en ologgad tabell. Mer information om ologgade tabeller finns i [PostgreSQL-dokumentationen](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: Namnet på tabellen som ska skapas.

**Exempel**

Följande fråga skapar en ny tabell `films_recent` som endast består av de senaste posterna från tabellen `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### VISA

Kommandot `SHOW` visar den aktuella inställningen för körningsparametrar. Dessa variabler kan ställas in med programsatsen `SET` genom att redigera konfigurationsfilen `postgresql.conf`, via miljövariabeln `PGOPTIONS` (när du använder libpq eller ett libpq-baserat program) eller via kommandoradsflaggor när Postgres-servern startas.

```sql
SHOW name
SHOW ALL
```

**Parametrar**

- `name`: Namnet på körningsparametern som du vill ha information om. Möjliga värden för körningsparametern är följande värden:
   - `SERVER_VERSION`: Den här parametern visar serverns versionsnummer.
   - `SERVER_ENCODING`: Den här parametern visar kodningen för teckenuppsättningen på serversidan.
   - `LC_COLLATE`: Den här parametern visar databasens språkområdesinställning för sortering (textordning).
   - `LC_CTYPE`: Den här parametern visar databasens språkområdesinställning för teckenklassificering.
      `IS_SUPERUSER`: Den här parametern visar om den aktuella rollen har superanvändarbehörighet.
- `ALL`: Visa värdena för alla konfigurationsparametrar med beskrivningar.

**Exempel**

Följande fråga visar den aktuella inställningen för parametern `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### COPY

Kommandot `COPY` dumpar utdata från en `SELECT`-fråga till en angiven plats. Användaren måste ha åtkomst till den här platsen för att det här kommandot ska lyckas.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Parametrar**

- `query`: Frågan som du vill kopiera.
- `format_name`: Det format som du vill kopiera frågan i. `format_name` kan vara en av `parquet`, `csv` eller `json`. Som standard är värdet `parquet`.

>[!NOTE]
>
>Den fullständiga utdatasökvägen är `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

Med kommandot `ALTER TABLE` kan du lägga till eller ta bort primära eller externa nyckelbegränsningar samt lägga till kolumner i tabellen.

#### LÄGG TILL ELLER SLÄPP BEGRÄNSNINGAR

Följande SQL-frågor visar exempel på hur du lägger till eller släpper begränsningar i en tabell.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Parametrar**

- `table_name`: Namnet på tabellen som du redigerar.
- `constraint_name`: Namnet på begränsningen som du vill lägga till eller ta bort.
- `column_name`: Namnet på den kolumn som du lägger till en begränsning i.
- `referenced_table_name`: Namnet på tabellen som refereras av sekundärnyckeln.
- `primary_column_name`: Namnet på den kolumn som refereras av sekundärnyckeln.

>[!NOTE]
>
>Tabellschemat ska vara unikt och inte delas mellan flera tabeller. Dessutom är namnutrymmet obligatoriskt för begränsningar för primärnycklar.

#### LÄGG TILL KOLUMN

Följande SQL-frågor visar exempel på hur du lägger till kolumner i en tabell.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Parametrar**

- `table_name`: Namnet på tabellen som du redigerar.
- `column_name`: Namnet på den kolumn som du vill lägga till.
- `data_type`: Datatypen för den kolumn som du vill lägga till. Följande datatyper stöds: bigint, char, string, date, datetime, double, double precision, integer, smallint, tinyint, varchar.

### VISA PRIMÄRNYCKLAR

Kommandot `SHOW PRIMARY KEYS` visar alla primärnyckelbegränsningar för den angivna databasen.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### VISA FRÄMSTA TANGENTER

Kommandot `SHOW FOREIGN KEYS` visar alla begränsningar för främmande nycklar för den angivna databasen.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
