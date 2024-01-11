---
title: Anonymt block i frågetjänsten
description: Det anonyma blocket är en SQL-syntax som stöds av Adobe Experience Platform Query Service, som gör att du effektivt kan köra en sekvens med frågor
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 9193ba821409806cd7b4667c5de73a0cf2660c66
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Anonymt block i frågetjänsten

Adobe Experience Platform Query Service stöder anonyma block. Med den anonyma blockfunktionen kan du kedja en eller flera SQL-satser som körs i sekvens. De gör det även möjligt att hantera undantag.

Den anonyma blockfunktionen är ett effektivt sätt att utföra en sekvens av åtgärder eller frågor. Frågekedjan inom blocket kan sparas som en mall och schemaläggas för att köras vid en viss tidpunkt eller ett visst intervall. Dessa frågor kan användas för att skriva och lägga till data för att skapa en ny datauppsättning och används vanligtvis där du har ett beroende.

Tabellen innehåller en beskrivning av blockets huvudavsnitt: körning och undantagshantering. Avsnitten definieras av nyckelorden `BEGIN`, `END`och `EXCEPTION`.

| section | description |
|---|---|
| körning | Ett körbart avsnitt börjar med nyckelordet `BEGIN` och slutar med nyckelordet `END`. Alla programsatser som ingår i `BEGIN` och `END` nyckelord kommer att köras i sekvens och säkerställer att efterföljande frågor inte körs förrän den föregående frågan i sekvensen har slutförts. |
| undantagshantering | Det valfria avsnittet för undantagshantering börjar med nyckelordet `EXCEPTION`. Den innehåller koden som fångar upp och hanterar undantag om någon av SQL-satserna i körningsavsnittet misslyckas. Om någon av frågorna misslyckas stoppas hela blocket. |

Det är värt att notera att ett block är en körbar programsats och därför kan kapslas i andra block.

>[!NOTE]
>
> Vi rekommenderar att du testar dina frågor med mindre datauppsättningar och ser till att de fungerar som förväntat. Om en fråga har ett syntaxfel genereras undantaget och hela blocket avbryts. När du har verifierat frågeintegriteten kan du börja kedja dem. Detta garanterar att blocket fungerar som väntat innan du sätter i det.

## Exempel på anonyma blockfrågor

Följande fråga visar ett exempel på hur du kedjer SQL-satser. Se [SQL-syntax i Query Service](../sql/syntax.md) -dokument om du vill ha mer information om någon av de SQL-syntaxer som används.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

I exemplet nedan `SET` kvarstår resultatet av en `SELECT` -frågan i den angivna lokala variabeln. Variabeln omfångas av det anonyma blocket.

ID för ögonblicksbilden lagras som en lokal variabel (`@current_sid`). Den används sedan i nästa fråga för att returnera resultat baserat på SNAPSHOT från samma datauppsättning/tabell.

En databasögonblicksbild är en skrivskyddad, statisk vy av en SQL Server-databas. Mer [information om snapshot-satsen](../sql/syntax.md#SNAPSHOT-clause) finns i SQL-syntaxdokumentationen.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Anonym blockering med tredjepartsklienter {#third-party-clients}

Vissa tredjepartsklienter kan kräva en separat identifierare före och efter ett SQL-block för att ange att en del av skriptet ska hanteras som en enskild sats. Om du får ett felmeddelande när du använder frågetjänsten med en tredjepartsklient bör du läsa tredjepartsklientens dokumentation om användningen av ett SQL-block.

Till exempel: **DbVisualizer** kräver att avgränsaren måste vara den enda texten på raden. I DbVisualizer är standardvärdet för Begin Identifier `--/` och för End Identifier är det `/`. Ett exempel på ett anonymt block i DbVisualizer visas nedan:

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

I synnerhet för DbVisualizer finns det också ett alternativ i användargränssnittet att &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. Se [Dokumentation för DbVisualizer](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) för mer information.

## Nästa steg

Genom att läsa det här dokumentet har du nu en tydlig förståelse för anonyma block och hur de är strukturerade. Läs [guide för frågekörning](../best-practices/writing-queries.md) för mer information om hur du skriver frågor.

Du bör även läsa om [hur anonyma block används med det inkrementella lastdesignmönstret](./incremental-load.md) för att öka frågans effektivitet.
