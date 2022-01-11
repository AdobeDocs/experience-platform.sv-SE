---
title: Exempel på anonyma blockfrågor
description: Det anonyma blocket är en SQL-syntax som stöds av Adobe Experience Platform Query Service, som gör att du effektivt kan köra en sekvens med frågor
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 9f4e34edc47a333aa88153529d0af6a10f189a15
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Exempelfrågor för anonymt block

Adobe Experience Platform Query Service stöder anonyma block. Med den anonyma blockfunktionen kan du kedja en eller flera SQL-satser som körs i sekvens. De gör det även möjligt att hantera undantag.

Den anonyma blockfunktionen är ett effektivt sätt att utföra en sekvens av åtgärder eller frågor. Frågekedjan inom blocket kan sparas som en mall och schemaläggas för att köras vid en viss tidpunkt eller ett visst intervall. Dessa frågor kan användas för att skriva och lägga till data för att skapa en ny datauppsättning och används vanligtvis där du har ett beroende.

Tabellen innehåller en beskrivning av blockets huvudavsnitt: exekvering och undantagshantering. Avsnitten definieras av nyckelorden `BEGIN`, `END`och `EXCEPTION`.

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
BEGIN
     
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
     
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
     
END;
```

<!-- The block below uses `SET` to persist the result of a select query with a variable. It is used in the anonymous block to store the response from a query as a local variable for use with the `SNAPSHOT` feature. -->

I exemplet nedan `SET` kvarstår resultatet av `SELECT` -frågan i den angivna lokala variabeln. Variabeln omfångas av det anonyma blocket.

ID för ögonblicksbilden lagras som en lokal variabel (`@current_sid`). Den används sedan i nästa fråga för att returnera resultat baserat på SNAPSHOT från samma datauppsättning/tabell.

En databasögonblicksbild är en skrivskyddad, statisk vy av en SQL Server-databas. Mer [information om snapshot-satsen](../sql/syntax.md#SNAPSHOT-clause) finns i SQL-syntaxdokumentationen.

```SQL
BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                                     
END;
```

## Nästa steg

Genom att läsa det här dokumentet har du nu en tydlig förståelse för anonyma block och hur de är strukturerade. [Mer information om frågekörning](./writing-queries.md), läs guiden om frågekörning i Query Service.

Fler exempel på frågor som kan användas i frågetjänsten finns i [Adobe Analytics exempelfrågor](./adobe-analytics.md), [Adobe Target exempelfrågor](./adobe-target.md), eller [Exempelfrågor för ExperienceEvent](./experience-event-queries.md).
