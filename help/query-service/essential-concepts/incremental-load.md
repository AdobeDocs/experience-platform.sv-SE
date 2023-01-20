---
title: Inkrementell inläsning i frågetjänsten
description: Funktionen för inkrementell inläsning använder både anonyma funktioner för block och ögonblicksbilder för att ge en nästan realtidslösning för att flytta data från datasjön till data warehouse samtidigt som matchande data ignoreras.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Inkrementell inläsning i frågetjänsten

Designmönstret för inkrementell belastning är en lösning för datahantering. Mönstret bearbetar bara information i datauppsättningen som har skapats eller ändrats sedan den senaste inläsningen.

Inkrementell belastning använder olika funktioner i Adobe Experience Platform Query Service, till exempel anonyma block och ögonblicksbilder. Det här designmönstret ökar bearbetningseffektiviteten eftersom data som redan har bearbetats från källan hoppas över. Den kan användas med både direktuppspelning och batchdatabearbetning.

Det här dokumentet innehåller en serie instruktioner om hur du skapar ett designmönster för stegvis bearbetning. Dessa steg kan användas som mall för att skapa egna inkrementella datainläsningsfrågor.

## Komma igång

SQL-exemplen i det här dokumentet kräver att du har en förståelse för de anonyma funktionerna för block och ögonblicksbilder. Vi rekommenderar att du läser [exempel på anonyma blockfrågor](./anonymous-block.md) dokumentation och även [snapshot-sats](../sql/syntax.md#snapshot-clause) dokumentation.

Anvisningar om vilka termer som används i den här handboken finns i [SQL-syntaxguide](../sql/syntax.md).

## Inläsning av data inkrementellt

Stegen nedan visar hur du skapar och läser in data stegvis med hjälp av ögonblicksbilder och den anonyma blockfunktionen. Designmönstret kan användas som mall för en egen frågesekvens.

1 Skapa en `checkpoint_log` för att spåra den senaste ögonblicksbilden som använts för att bearbeta data. Spårningstabellen (`checkpoint_log` i det här exemplet) måste först initieras till `null` för att stegvis bearbeta en datauppsättning.

```SQL
DROP TABLE IF EXISTS checkpoint_log;
CREATE TABLE  checkpoint_log AS
SELECT
   cast(NULL AS string) process_name,
   cast(NULL AS string) process_status,
   cast(NULL AS string) last_snapshot_id,
   cast(NULL AS TIMESTAMP) process_timestamp
   WHERE false;
```

2 Fyll i `checkpoint_log` tabell med en tom post för den datauppsättning som behöver inkrementell bearbetning. `DIM_TABLE_ABC` är den datauppsättning som ska bearbetas i exemplet nedan. Vid det första tillfället av bearbetning `DIM_TABLE_ABC`, `last_snapshot_id` initieras som `null`. Detta gör att du kan bearbeta hela datauppsättningen vid första tillfället och stegvis efter detta.

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

3 Nästa, initiera `DIM_TABLE_ABC_Incremental` som innehåller bearbetade utdata från `DIM_TABLE_ABC`. Det anonyma blocket i **obligatoriskt** körningsavsnittet i SQL-exemplet nedan, som beskrivs i steg ett till fyra, körs sekventiellt för att bearbeta data stegvis.

1. Ange `from_snapshot_id` som anger var bearbetningen börjar. The `from_snapshot_id` i exemplet frågas från `checkpoint_log` tabell för användning med `DIM_TABLE_ABC`. Vid den första körningen kommer ID:t för ögonblicksbilden att `null` vilket innebär att hela datauppsättningen kommer att bearbetas.
2. Ange `to_snapshot_id` som det aktuella ögonblicksbild-ID:t för källtabellen (`DIM_TABLE_ABC`). I exemplet hämtas detta från källtabellens metadatatabell.
3. Använd `CREATE` nyckelord som ska skapas `DIM_TABLE_ABC_Incremenal` som måltabell. Måltabellen består av bearbetade data från källdatauppsättningen (`DIM_TABLE_ABC`). Detta tillåter att bearbetade data från källtabellen mellan `from_snapshot_id` och `to_snapshot_id`, som läggs till stegvis i måltabellen.
4. Uppdatera `checkpoint_log` tabellen med `to_snapshot_id` för källdata som `DIM_TABLE_ABC` har bearbetats.
5. Om någon av de sekventiellt utförda frågorna i det anonyma blocket misslyckas, **valfri** undantagsavsnitt körs. Detta returnerar ett fel och avslutar processen.

>[!NOTE]
>
>The `history_meta('source table name')` är en praktisk metod som används för att få åtkomst till tillgängliga ögonblicksbilder i en datauppsättning.

```SQL
$$ BEGIN
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                ON a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    CREATE TABLE DIM_TABLE_ABC_Incremental AS
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
 
INSERT INTO
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

4 Använd logiken för inkrementell datainläsning i exemplet med anonyma block nedan för att tillåta att nya data från källdatauppsättningen (sedan den senaste tidsstämpeln) bearbetas och läggs till i måltabellen vid en vanlig gräns. I exemplet ändras data till `DIM_TABLE_ABC` bearbetas och läggs till `DIM_TABLE_ABC_incremental`.

>[!NOTE]
>
> `_ID` är primärnyckeln i båda `DIM_TABLE_ABC_Incremental` och `SELECT history_meta('DIM_TABLE_ABC')`.

```SQL
$$ BEGIN
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                ON a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
INSERT INTO
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

Denna logik kan tillämpas på alla tabeller för att utföra inkrementella inläsningar.

## Utgångna ögonblicksbilder

>[!IMPORTANT]
>
>Metadata för ögonblicksbilder förfaller efter **två** dagar. En ögonblicksbild som har gått ut gör logiken i skriptet ovan ogiltig.

För att lösa problemet med att ett ögonblicksbild-ID har gått ut infogar du följande kommando i början av det anonyma blocket. Följande kodrad åsidosätter `@from_snapshot_id` med tidigast tillgängliga `snapshot_id` från metadata.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

Hela kodblocket ser ut så här:

```SQL
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

## Nästa steg

Genom att läsa det här dokumentet bör du få en bättre förståelse för hur du använder anonyma funktioner för block och ögonblicksbilder för att utföra inkrementella inläsningar och kan använda den här logiken för dina egna specifika frågor. Allmänna riktlinjer för frågekörning finns i [guide för frågekörning i frågetjänsten](../best-practices/writing-queries.md).
