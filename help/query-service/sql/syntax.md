---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Frågetjänst;SQL-syntax;sql;ctas;CTAS;Skapa tabell som markerad
solution: Experience Platform
title: SQL-syntax i frågetjänst
description: I det här dokumentet visas SQL-syntax som stöds av Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 3907efa2e8c20671e283c1e5834fc7224ee12f9e
workflow-type: tm+mt
source-wordcount: '3406'
ht-degree: 2%

---

# SQL-syntax i Query Service

Adobe Experience Platform Query Service ger möjlighet att använda ANSI SQL av standardtyp för `SELECT` -programsatser och andra begränsade kommandon. Det här dokumentet innehåller SQL-syntaxen som stöds av [!DNL Query Service].

## SELECT-frågor {#select-queries}

Följande syntax definierar en `SELECT` fråga som stöds av [!DNL Query Service]:

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

där `from_item` kan vara något av följande:

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

och `grouping_element` kan vara något av följande:

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

Den här satsen kan användas för att stegvis läsa data i en tabell baserat på ID:n för ögonblicksbilder. Ett ID för en ögonblicksbild är en kontrollpunktsmarkör som representeras av ett Long-typnummer som används på en datarintabell varje gång data skrivs till den. The `SNAPSHOT` -satsen kopplar sig till den registerrelation som den används bredvid.

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

Observera att `SNAPSHOT` -satsen fungerar med en tabell eller ett tabellalias men inte ovanpå en underfråga eller vy. A `SNAPSHOT` -satsen fungerar var som helst `SELECT` fråga i en tabell kan tillämpas.

Dessutom kan du använda `HEAD` och `TAIL` som särskilda förskjutningsvärden för ögonblicksbildssatser. Använda `HEAD` refererar till en förskjutning före den första ögonblicksbilden, medan `TAIL` refererar till en förskjutning efter den sista ögonblicksbilden.

>[!NOTE]
>
>Om du frågar mellan två ögonblicksbild-ID:n och startögonblicksbilden har gått ut kan följande två scenarier inträffa, beroende på om den valfria reservbeteendeflaggan (`resolve_fallback_snapshot_on_failure`) är inställt:
>
>- Om den valfria reservbeteendeflaggan är inställd väljer frågetjänsten den tidigaste tillgängliga ögonblicksbilden, anger den som startögonblicksbild och returnerar data mellan den tidigaste tillgängliga ögonblicksbilden och den angivna slutögonblicksbilden. Dessa data **inkluderande** av den tidigaste tillgängliga ögonblicksbilden.
>
>- Om den valfria reservbeteendeflaggan inte är inställd returneras ett fel.


### WHERE-sats

Som standard används matchningar som skapats av en `WHERE` -sats på en `SELECT` -frågan är skiftlägeskänslig. Om du vill att matchningar ska vara skiftlägeskänsliga kan du använda nyckelordet `ILIKE` i stället för `LIKE`.

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

A `SELECT` fråga som använder kopplingar har följande syntax:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT, and EXCEPT

The `UNION`, `INTERSECT`och `EXCEPT` -satser används för att kombinera eller exkludera liknande rader från två eller flera tabeller:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### SKAPA TABELL SOM MARKERAD {#create-table-as-select}

Följande syntax definierar en `CREATE TABLE AS SELECT` (CTAS) fråga:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE') ] AS (select_query)
```

| Parametrar | Beskrivning |
| ----- | ----- |
| `schema` | Titeln på XDM-schemat. Använd bara den här satsen om du vill använda ett befintligt XDM-schema för den nya datauppsättningen som skapas av CTAS-frågan. |
| `rowvalidation` | (Valfritt) Anger om användaren vill validera radnivån för alla nya batchar som hämtas för den nya datauppsättningen. Standardvärdet är `true`. |
| `label` | När du skapar en datauppsättning med en CTAS-fråga använder du den här etiketten med värdet `profile` för att märka datauppsättningen som aktiverad för profilen. Det innebär att din datauppsättning automatiskt markeras för profil när den skapas. Mer information om hur du använder finns i det härledda attributtilläggsdokumentet `label`. |
| `select_query` | A `SELECT` -programsats. Syntaxen för `SELECT` frågan finns i [SELECT Queries section](#select-queries). |

**Exempel**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title', label='PROFILE') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>The `SELECT` -programsats måste ha ett alias för sammanställningsfunktioner som `COUNT`, `SUM`, `MIN`och så vidare. Dessutom finns `SELECT` kan anges med eller utan parenteser (). Du kan ange en `SNAPSHOT` -sats för att läsa inkrementella deltas i måltabellen.

## INFOGA I

The `INSERT INTO` kommandot definieras enligt följande:

```sql
INSERT INTO table_name select_query
```

| Parametrar | Beskrivning |
| ----- | ----- |
| `table_name` | Namnet på tabellen som du vill infoga frågan i. |
| `select_query` | A `SELECT` -programsats. Syntaxen för `SELECT` frågan finns i [SELECT Queries section](#select-queries). |

**Exempel**

>[!NOTE]
>
>Följande är ett intressant exempel som bara är till för instruktionsändamål.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> The `SELECT` programsats **får inte** omges av parenteser (). Dessutom är schemat för resultatet av `SELECT` -programsatsen måste överensstämma med den tabell som definieras i `INSERT INTO` -programsats. Du kan ange en `SNAPSHOT` -sats för att läsa inkrementella deltas i måltabellen.

De flesta fält i ett riktigt XDM-schema finns inte på rotnivå och SQL tillåter inte användning av punktnotation. För att få ett realistiskt resultat med kapslade fält måste du mappa varje fält i `INSERT INTO` bana.

Till `INSERT INTO` kapslade sökvägar använder du följande syntax:

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**Exempel**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## DROP TABLE

The `DROP TABLE` kommandot släpper en befintlig tabell och tar bort katalogen som är associerad med tabellen från filsystemet om den inte är en extern tabell. Om tabellen inte finns inträffar ett undantag.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `IF EXISTS` | Om detta anges genereras inget undantag om tabellen gör det **not** finns. |

## SKAPA DATABAS

The `CREATE DATABASE` skapar en ADLS-databas.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## DROP DATABASE

The `DROP DATABASE` kommandot tar bort databasen från en instans.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `IF EXISTS` | Om detta anges genereras inget undantag om databasen gör det **not** finns. |

## DROP SCHEMA

The `DROP SCHEMA` kommandot släpper ett befintligt schema.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `IF EXISTS` | Om detta anges genereras inget undantag om schemat gör det **not** finns. |
| `RESTRICT` | Standardvärde för läget. Om detta anges kommer schemat endast att tas bort om det **inte** innehåller alla tabeller. |
| `CASCADE` | Om detta anges kommer schemat att tas bort tillsammans med alla tabeller som finns i schemat. |

## SKAPA VY

Följande syntax definierar en `CREATE VIEW` fråga:

```sql
CREATE VIEW view_name AS select_query
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `view_name` | Namnet på den vy som ska skapas. |
| `select_query` | A `SELECT` -programsats. Syntaxen för `SELECT` frågan finns i [SELECT Queries section](#select-queries). |

**Exempel**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

Följande syntax definierar en `DROP VIEW` fråga:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `IF EXISTS` | Om detta anges genereras inget undantag om vyn gör det **not** finns. |
| `view_name` | Namnet på den vy som ska tas bort. |

**Exempel**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Anonymt block

Ett anonymt block består av två avsnitt: körbara avsnitt och avsnitt för undantagshantering. I ett anonymt block är det körbara avsnittet obligatoriskt. Avsnittet om undantagshantering är dock valfritt.

I följande exempel visas hur du skapar ett block med en eller flera programsatser som ska köras tillsammans:

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Nedan visas ett exempel med anonym blockering.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### Auto till JSON {#auto-to-json}

Frågetjänsten stöder en valfri inställning på sessionsnivå för att returnera komplexa fält på den översta nivån från interaktiva SELECT-frågor som JSON-strängar. The `auto_to_json` Med den här inställningen kan data från komplexa fält returneras som JSON och sedan tolkas till JSON-objekt med hjälp av standardbibliotek.

ANGE funktionsflagga `auto_to_json` till true innan SELECT-frågan som innehåller komplexa fält körs.

```sql
set auto_to_json=true; 
```

#### Innan du anger `auto_to_json` flagga

Följande tabell innehåller ett exempel på frågeresultat före `auto_to_json` inställningen används. Samma SELECT-fråga (se nedan) som avser en tabell med komplexa fält användes i båda scenarierna.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

Resultatet är följande:

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### Efter inställning av `auto_to_json` flagga

I följande tabell visas skillnaden i resultat som `auto_to_json` -inställningen har på den resulterande datauppsättningen. Samma SELECT-fråga användes i båda scenarierna.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Lös reservögonblicksbild vid fel {#resolve-fallback-snapshot-on-failure}

The `resolve_fallback_snapshot_on_failure` används för att lösa problemet med ett ögonblicksbilds-ID som har gått ut. Metadata för ögonblicksbilder går ut efter två dagar och en ögonblicksbild som gått ut kan göra skriptets logik ogiltig. Detta kan vara ett problem när anonyma block används.

Ange `resolve_fallback_snapshot_on_failure` true om du vill åsidosätta en ögonblicksbild med ett tidigare ID för ögonblicksbild.

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

Följande kodrad åsidosätter `@from_snapshot_id` med tidigast tillgängliga `snapshot_id` från metadata.

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```


## Dataresursorganisation

Det är viktigt att logiskt organisera era datatillgångar inom Adobe Experience Platform dataresa när de växer. Med frågetjänsten utökas SQL-konstruktioner som gör att du logiskt kan gruppera dataresurser i en sandlåda. Med den här organisationsmetoden kan du dela datatillgångar mellan scheman utan att behöva flytta dem fysiskt.

Följande SQL-konstruktioner som använder standard-SQL-syntax stöds så att du kan organisera dina data logiskt.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Se guiden [logisk organisation av datatillgångar](../best-practices/organize-data-assets.md) om du vill ha mer detaljerad information om hur frågetjänsten fungerar.

## Tabellen finns

The `table_exists` SQL-kommandot används för att bekräfta om en tabell finns i systemet eller inte. Kommandot returnerar ett booleskt värde: `true` om tabellen **gör** finns, och `false` om tabellen **not** finns.

Genom att validera om en tabell finns innan programsatserna körs, kan `table_exists` förenklar processen att skriva ett anonymt block som omfattar både `CREATE` och `INSERT INTO` användningsfall.

Följande syntax definierar `table_exists` kommando:

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## Textbunden {#inline}

The `inline` -funktionen separerar elementen i en array med strukturer och genererar värdena i en tabell. Den kan bara placeras i `SELECT` lista eller en `LATERAL VIEW`.

The `inline` function **inte** placeras i en urvalslista där det finns andra generatorfunktioner.

Som standard får kolumnerna som skapas namnen &quot;col1&quot;, &quot;col2&quot; och så vidare. Om uttrycket är `NULL` så skapas inga rader.

>[!TIP]
>
>Du kan byta namn på kolumnnamnen med `RENAME` -kommando.

**Exempel**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

Exemplet returnerar följande:

```text
1  a Spark SQL
2  b Spark SQL
```

I det andra exemplet demonstreras konceptet och tillämpningen av `inline` funktion. Datamodellen för exemplet illustreras i bilden nedan.

![Ett schemadiagram för productListItems.](../images/sql/productListItems.png)

**Exempel**

```sql
select inline(productListItems) from source_dataset limit 10;
```

De värden som hämtas från `source_dataset` används för att fylla i måltabellen.

| SKU | upplevelse | kvantitet | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot;)&quot; | 5 | 10.5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;)&quot;)&quot;) |  |  |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA,NULL)&quot;)&quot;)&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] SQL-kommandon

Underavsnittet nedan beskriver Spark SQL-kommandon som stöds av Query Service.

### ANGE

The `SET` anger du en egenskap och returnerar värdet för en befintlig egenskap eller visar alla befintliga egenskaper. Om ett värde anges för en befintlig egenskapsnyckel åsidosätts det gamla värdet.

```sql
SET property_key = property_value
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `property_key` | Namnet på den egenskap som du vill visa eller ändra. |
| `property_value` | Värdet som du vill att egenskapen ska anges som. |

Om du vill returnera värdet för en inställning använder du `SET [property key]` utan `property_value`.

## [!DNL PostgreSQL] kommandon

Underavsnitten nedan täcker [!DNL PostgreSQL] kommandon som stöds av frågetjänsten.

### ANALYSERA TABELL

The `ANALYZE TABLE` kommandot beräknar statistik för en tabell på den accelererade lagringsplatsen. Statistiken beräknas på utförda CTAS- eller ITAS-frågor för en given tabell på accelererad butik.

**Exempel**

```sql
ANALYZE TABLE <original_table_name>
```

Nedan följer en lista över statistiska beräkningar som är tillgängliga efter användning av `ANALYZE TABLE` kommando:-

| Beräknade värden | Beskrivning |
|---|---|
| `field` | Namnet på kolumnen i en tabell. |
| `data-type` | Godtagbar datatyp för varje kolumn. |
| `count` | Antalet rader som innehåller ett värde som inte är null för det här fältet. |
| `distinct-count` | Antalet unika eller distinkta värden för det här fältet. |
| `missing` | Antalet rader som har ett null-värde för det här fältet. |
| `max` | Det högsta värdet från den analyserade tabellen. |
| `min` | Det minsta värdet från den analyserade tabellen. |
| `mean` | Genomsnittsvärdet för den analyserade tabellen. |
| `stdev` | Standardavvikelsen för den analyserade tabellen. |

### BÖRJA

The `BEGIN` eller `BEGIN WORK` eller `BEGIN TRANSACTION` , initierar ett transaktionsblock. Alla programsatser som infogas efter kommandot begin körs i en enda transaktion tills ett explicit COMMIT- eller ROLLBACK-kommando anges. Det här kommandot är detsamma som `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### STÄNG

The `CLOSE` frigör resurser som är kopplade till en öppen markör. När markören har stängts tillåts inga efterföljande åtgärder på den. En markör bör stängas när den inte längre behövs.

```sql
CLOSE name
CLOSE ALL
```

If `CLOSE name` används, `name` representerar namnet på en öppen markör som måste stängas. If `CLOSE ALL` används stängs alla öppna markörer.

### DEALOCATE

The `DEALLOCATE` kan du frigöra en tidigare förberedd SQL-sats. Om du inte uttryckligen frigör en förberedd sats, frigörs den när sessionen avslutas. Mer information om förberedda satser finns i [FÖRBERED, kommando](#prepare) -avsnitt.

```sql
DEALLOCATE name
DEALLOCATE ALL
```

If `DEALLOCATE name` används, `name` representerar namnet på den förberedda sats som behöver frigöras. If `DEALLOCATE ALL` används kommer alla förberedda utdrag att frigöras.

### DEKLARERA

The `DECLARE` kan användaren skapa en markör som kan användas för att hämta ett litet antal rader från en större fråga. När markören har skapats hämtas rader från den med `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `name` | Namnet på den markör som ska skapas. |
| `query` | A `SELECT` eller `VALUES` som anger de rader som markören ska returnera. |

### KÖR

The `EXECUTE` -kommandot används för att köra en tidigare förberedd sats. Eftersom förberedda satser bara finns under en session måste den förberedda satsen ha skapats av en `PREPARE` -programsatsen utfördes tidigare i den aktuella sessionen. Mer information om hur du använder förberedda satser finns i [`PREPARE` kommando](#prepare) -avsnitt.

Om `PREPARE` -programsats som skapade programsatsen specificerade vissa parametrar, måste en kompatibel uppsättning parametrar skickas till `EXECUTE` -programsats. Om de här parametrarna inte skickas visas ett fel.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `name` | Namnet på den förberedda sats som ska köras. |
| `parameter` | Det faktiska värdet för en parameter till den förberedda programsatsen. Det här måste vara ett uttryck som ger ett värde som är kompatibelt med den här parameterns datatyp, vilket bestämdes när den förberedda satsen skapades.  Om det finns flera parametrar för den förberedda programsatsen avgränsas de med kommatecken. |

### FÖRKLARA

The `EXPLAIN` -kommandot visar körningsplanen för den angivna programsatsen. Körningsplanen visar hur tabellerna som programsatsen refererar till skannas.  Om flera tabeller refereras visas vilka kopplingsalgoritmer som används för att sammanfoga de rader som krävs från varje indatatabell.

```sql
EXPLAIN statement
```

Använd `FORMAT` nyckelord med `EXPLAIN` för att definiera svarsformatet.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `FORMAT` | Använd `FORMAT` för att ange utdataformat. De tillgängliga alternativen är `TEXT` eller `JSON`. Utdata som inte är text innehåller samma information som textutdataformatet, men är enklare att tolka i program. Parametern är som standard `TEXT`. |
| `statement` | Alla `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`, eller `CREATE MATERIALIZED VIEW AS` -programsats vars körningsplan du vill se. |

>[!IMPORTANT]
>
>Alla utdata som `SELECT` programsatsen kan returneras om den körs med `EXPLAIN` nyckelord. Andra biverkningar av satsen inträffar som vanligt.

**Exempel**

I följande exempel visas planen för en enkel fråga i en tabell med en enda `integer` kolumn och 10000 rader:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### FETCH

The `FETCH` hämtar rader med hjälp av en markör som skapats tidigare.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `num_of_rows` | Antalet rader som ska hämtas. |
| `cursor_name` | Namnet på den markör som du hämtar information från. |

### FÖRBEREDA {#prepare}

The `PREPARE` kan du skapa en förberedd programsats. En förberedd programsats är ett objekt på serversidan som kan användas för att mallatisera liknande SQL-programsatser.

Förberedda programsatser kan innehålla parametrar, som är värden som ersätts med programsatsen när den körs. Parametrar refereras efter position, med $1, $2 osv., när förberedda satser används.

Du kan också ange en lista med parameterdatatyper. Om en parameters datatyp inte finns med i listan kan typen härledas från kontexten.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `name` | Namnet på den förberedda satsen. |
| `data_type` | Datatyperna för den förberedda satsens parametrar. Om en parameters datatyp inte finns med i listan kan typen härledas från kontexten. Om du behöver lägga till flera datatyper kan du lägga till dem i en kommaseparerad lista. |

### ROLLBACK

The `ROLLBACK` kommandot ångrar den aktuella transaktionen och tar bort alla uppdateringar som gjorts av transaktionen.

```sql
ROLLBACK
ROLLBACK WORK
```

### MARKERA I

The `SELECT INTO` skapar en ny tabell och fyller den med data som beräknas av en fråga. Data returneras inte till klienten, vilket är fallet med en normal `SELECT` -kommando. Den nya tabellens kolumner har de namn och datatyper som är associerade med utdatakolumnerna för `SELECT` -kommando.

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

Mer information om SELECT-standardfrågeparametrarna finns i [SELECT-frågesektion](#select-queries). I det här avsnittet listas endast parametrar som är exklusiva för `SELECT INTO` -kommando.

| Parametrar | Beskrivning |
| ------ | ------ |
| `TEMPORARY` eller `TEMP` | En valfri parameter. Om det anges blir det register som skapas ett temporärt register. |
| `UNLOGGED` | En valfri parameter. Om det anges kommer tabellen som skapas att vara en ologgad tabell. Mer information om ologgade tabeller finns i [[!DNL PostgreSQL] dokumentation](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | Namnet på tabellen som ska skapas. |

**Exempel**

Följande fråga skapar en ny tabell `films_recent` bestående av endast de senaste posterna från tabellen `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### VISA

The `SHOW` -kommandot visar den aktuella inställningen för körningsparametrar. Dessa variabler kan ställas in med `SET` genom att redigera `postgresql.conf` konfigurationsfil via `PGOPTIONS` miljövariabel (när libpq används eller ett libpq-baserat program) eller via kommandoradsflaggor när Postgres-servern startas.

```sql
SHOW name
SHOW ALL
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `name` | Namnet på körningsparametern som du vill ha information om. Möjliga värden för körningsparametern är följande värden:<br>`SERVER_VERSION`: Den här parametern visar serverns versionsnummer.<br>`SERVER_ENCODING`: Den här parametern visar kodningen för teckenuppsättningen på serversidan.<br>`LC_COLLATE`: Den här parametern visar databasens språkområdesinställning för sortering (textordning).<br>`LC_CTYPE`: Den här parametern visar databasens språkområdesinställning för teckenklassificering.<br>`IS_SUPERUSER`: Den här parametern visar om den aktuella rollen har superanvändarbehörighet. |
| `ALL` | Visa värdena för alla konfigurationsparametrar med beskrivningar. |

**Exempel**

Följande fråga visar parameterns aktuella inställning `DateStyle`.

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

The `COPY` kommandot duplicerar utdata från alla `SELECT` fråga till en angiven plats. Användaren måste ha åtkomst till den här platsen för att det här kommandot ska lyckas.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `query` | Frågan som du vill kopiera. |
| `format_name` | Det format som du vill kopiera frågan i. The `format_name` kan vara en av `parquet`, `csv`, eller `json`. Som standard är värdet `parquet`. |

>[!NOTE]
>
>Den fullständiga utdatasökvägen `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE {#alter-table}

The `ALTER TABLE` kan du lägga till eller ta bort begränsningar för primär eller extern nyckel samt lägga till kolumner i tabellen.


#### LÄGG TILL ELLER SLÄPP BEGRÄNSNINGAR

Följande SQL-frågor visar exempel på hur du lägger till eller släpper begränsningar i en tabell.

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| Parametrar | Beskrivning |
| ------ | ------ |
| `table_name` | Namnet på tabellen som du redigerar. |
| `column_name` | Namnet på den kolumn som du lägger till en begränsning i. |
| `referenced_table_name` | Namnet på tabellen som refereras av sekundärnyckeln. |
| `primary_column_name` | Namnet på den kolumn som refereras av sekundärnyckeln. |


>[!NOTE]
>
>Tabellschemat ska vara unikt och inte delas mellan flera tabeller. Dessutom är namnutrymmet obligatoriskt för begränsningarna primär nyckel, primär identitet och identitet.

#### Lägga till eller släppa primära och sekundära identiteter

The `ALTER TABLE` kan du lägga till eller ta bort begränsningar för både primära och sekundära identitetstabellkolumner direkt via SQL.

I följande exempel läggs en primär identitet och en sekundär identitet till genom att begränsningar läggs till.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Identiteter kan också tas bort genom att begränsningar släpps, vilket visas i exemplet nedan.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Visa dokumentet på [ange identiteter i en ad hoc-datauppsättning](../data-governance/ad-hoc-schema-identities.md) för mer detaljerad information.

#### LÄGG TILL KOLUMN

Följande SQL-frågor visar exempel på hur du lägger till kolumner i en tabell.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Datatyper som stöds

I följande tabell visas godkända datatyper för att lägga till kolumner i en tabell med [!DNL Postgres SQL], XDM och [!DNL Accelerated Database Recovery] (ADR) i Azure SQL.

| — | PSQL-klient | XDM | ADR. | Beskrivning |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | En numerisk datatyp som används för att lagra stora heltal mellan -9 223 372 036 854 775 807 och 9 223 372 036 854 775 807 i 8 byte. |
| 2 | `integer` | `int4` | `integer` | En numerisk datatyp som används för att lagra heltal mellan -2 147 483 648 och 2 147 483 647 i 4 byte. |
| 3 | `smallint` | `int2` | `smallint` | En numerisk datatyp som används för att lagra heltal mellan -32 768 och 215-1 32 767 i 2 byte. |
| 4 | `tinyint` | `int1` | `tinyint` | En numerisk datatyp som används för att lagra heltal mellan 0 och 255 i 1 byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | En teckendatatyp med variabel storlek. `varchar` används bäst när kolumndatainmatningarnas storlek varierar avsevärt. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` och `FLOAT` är giltiga synonymer för `DOUBLE PRECISION`. `double precision` är en flyttalsdatatyp. Flyttalsvärden sparas i 8 byte. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` är en giltig synonym för `double precision`.`double precision` är en flyttalsdatatyp. Flyttalsvärden sparas i 8 byte. |
| 8 | `date` | `date` | `date` | The `date` datatypen är 4 byte-lagrade kalenderdatumvärden utan tidsstämpelinformation. Giltiga datum är från 01-01-0001 till 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | En datatyp som används för att lagra en instans i tid uttryckt som ett kalenderdatum och en tidpunkt på dagen. `datetime` omfattar kvalificerare för år, månad, dag, timme, sekund och bråk. A `datetime` -deklarationen kan innehålla alla delmängder av dessa tidsenheter som är förenade i den sekvensen, eller till och med bara en enda tidsenhet. |
| 10 | `char(len)` | `string` | `char(len)` | The `char(len)` nyckelord används för att ange att objektet är ett tecken med fast längd. |

#### LÄGG TILL SCHEMA

Följande SQL-fråga visar ett exempel på hur du lägger till en tabell i en databas/ett schema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Det går inte att lägga till ADLS-tabeller och -vyer i DWH-databaser/scheman.


#### TA BORT SCHEMA

Följande SQL-fråga visar ett exempel på hur du tar bort en tabell från en databas/ett schema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> DWH-tabeller och -vyer kan inte tas bort från fysiskt länkade DWH-databaser/DWH-scheman.


**Parametrar**

| Parametrar | Beskrivning |
| ------ | ------ |
| `table_name` | Namnet på tabellen som du redigerar. |
| `column_name` | Namnet på den kolumn som du vill lägga till. |
| `data_type` | Datatypen för den kolumn som du vill lägga till. Följande datatyper stöds: bigint, char, string, date, datetime, double, double precision, integer, smallint, tinyint, varchar. |

### VISA PRIMÄRNYCKLAR

The `SHOW PRIMARY KEYS` -kommandot listar alla primärnyckelbegränsningar för den angivna databasen.

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

The `SHOW FOREIGN KEYS` -kommandot listar alla begränsningar för främmande nycklar för den angivna databasen.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### VISA DATAGROUPS

The `SHOW DATAGROUPS` returnerar en tabell med alla associerade databaser. För varje databas innehåller tabellen schema, grupptyp, underordnad typ, underordnat namn och underordnat ID.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### VISA DATAGROUPS FÖR register

The `SHOW DATAGROUPS FOR` Kommandot table_name returnerar en tabell med alla associerade databaser som innehåller parametern som underordnad. För varje databas innehåller tabellen schema, grupptyp, underordnad typ, underordnat namn och underordnat ID.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parametrar**

- `table_name`: Namnet på den tabell som du vill söka efter associerade databaser för.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
