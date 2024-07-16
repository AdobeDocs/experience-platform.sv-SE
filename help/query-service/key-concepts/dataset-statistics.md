---
title: Dataset Statistik - beräkning
description: I det här dokumentet beskrivs hur du beräknar kolumnnivåstatistik för ADLS-datauppsättningar (Azure Data Lake Storage) med SQL-kommandon.
exl-id: 66f11cd4-b115-40b8-ba8a-c4bb3606bbbf
source-git-commit: 37aeff5131b9f67dbc99f6199918403e699478c8
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Datauppsättningsstatistikberäkning

Du kan nu beräkna kolumnnivåstatistik för [!DNL Azure Data Lake Storage] (ADLS) datauppsättningar med SQL-kommandot `COMPUTE STATISTICS`. SQL-kommandona som beräknar datauppsättningsstatistik är ett tillägg till kommandot `ANALYZE TABLE`. Fullständig information om kommandot `ANALYZE TABLE` finns i [SQL-referensdokumentationen](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Beräknad statistik lagras i temporära tabeller som har beständighet på sessionsnivå. Du kommer åt resultatet av beräkningarna när som helst under sessionen. De kan inte nås över olika PSQL-sessioner.

Om du vill visa statistik som har beräknats med kommandot `ANALYZE TABLE COMPUTE STATISTICS` kan du använda en SELECT-fråga för aliasnamnet eller Statistik-ID:t. Du kan också begränsa omfattningen av den statistiska analysen till antingen hela datauppsättningen, en deluppsättning av en datauppsättning, alla kolumner eller en deluppsättning av kolumner.

>[!IMPORTANT]
>
>Kommandona `COMPUTE STATISTICS`, `FILTERCONTEXT` och `FOR COLUMNS` stöds inte i tabeller med accelererade arkiv. Dessa tillägg för kommandot `ANALYZE TABLE` stöds för närvarande bara för ADLS-tabeller. Mer information finns i avsnittet [ANALYZE TABLE](../sql/syntax.md#analyze-table) i SQL-syntaxguiden.

Den här guiden hjälper dig att strukturera dina frågor så att du kan beräkna kolumnstatistiken för en ADLS-datauppsättning. Med dessa kommandon kan du se statistik som genererats under sessionen via en PSQL-klient med hjälp av en SQL-fråga.

## Beräkningsstatistik {#compute-statistics}

Ytterligare konstruktioner har lagts till i kommandot `ANALYZE TABLE` som gör att du kan **beräkna statistik för en delmängd av en datauppsättning och för vissa kolumner**. Om du vill beräkna datauppsättningsstatistik måste du använda formatet `ANALYZE TABLE <tableName> COMPUTE STATISTICS`.

>[!IMPORTANT]
>
>Standardbeteendet beräknar statistik för **hela datauppsättningen** och för **alla kolumner**. Om du vill beräkna statistik för alla kolumner använder du frågeformatet `ANALYZE TABLE COMPUTE STATISTICS`. Du rekommenderas **inte** att använda kommandot `COMPUTE STATISTICS` utan filter på en ADLS-datauppsättning, eftersom datamängden kan vara mycket stor (eventuellt antal databyte). I stället bör du alltid överväga att köra analyskommandot med `FILTERCONTEXT` och en angiven lista med kolumner. Mer information finns i avsnitten [Begränsa analyserade kolumner](#limit-included-columns) och [lägga till ett filtervillkor](#filter-condition).

I exemplet nedan beräknas statistik för datamängden `adc_geometric` och för **alla** kolumner i datamängden.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>Kommandot `COMPUTE STATISTICS` stöder inte datatyperna array eller map. Du kan ange en `skip_stats_for_complex_datatypes`-flagga som ska meddelas eller som ett felmeddelande om indatabildrutan innehåller kolumner med arrayer och mappningsdatatyper. Som standard är flaggan inställd på true. Använd följande kommando om du vill aktivera meddelanden eller fel: `SET skip_stats_for_complex_datatypes = false`.

## Skapa ett aliasnamn {#alias-name}

Eftersom resultatet av beräkningarna kan vara en stor mängd data är det orimligt att returnera beräknade data direkt i konsolutdata. Även om aliasnamn är valfria bör du använda dem som bästa praxis när du beräknar statistik. Ange ett aliasnamn i satsen för att beskriva resultaten i dina SQL-frågor. Ett annat alternativ är att en automatiskt genererad `Statistics ID` genereras och används för att lagra den beräknade informationen.

Exemplet nedan lagrar utdata för beräknad statistik i `alias_name` för senare referens. Aliasnamnet som används i frågan är tillgängligt för referens så snart kommandot `ANALYZE TABLE` har körts.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

Utdata för exemplet ovan är `SUCCESSFULLY COMPLETED, alias_name`. Konsolutdata visar inte statistik som svar på kommandot för att analysera tabellberäkningsstatistik. Om du vill se de detaljerade resultaten måste du använda en SELECT-fråga för aliasnamnet eller Statistik-ID:t.

## Visa utdata för beräknad statistik {#view-output-of-computed-statistics}

Om du inte anger ett aliasnamn i förväg genererar frågetjänsten automatiskt ett namn för `Statistics ID` som följer formatet för `<tableName_stats_{incremental_number}>`. Om ett aliasnamn anges visas det i kolumnen `Statistics ID`.

Ett exempel på utdata för en `COMPUTE STATISTICS`-fråga är följande:

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

Du kan sedan **fråga den beräknade statistiken direkt** genom att referera till `Statistics ID`. Med exempelprogramsatsen nedan kan du visa utdata fullständigt när den används med `Statistics ID` eller aliasnamnet.

```sql
SELECT * FROM adc_geometric_stats_1; 
```

Den beräknade statistiken kan se ut ungefär som i exemplet nedan.

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(12 rows)
```

## Visa metadata för statistisk analys {#show-statistics}

Du kan använda kommandot `SHOW STATISTICS` för att visa metadata för all temporär statistik som genereras i sessionen. Det här kommandot kan hjälpa dig att förfina omfattningen av din statistiska analys.

Ett exempel på `SHOW STATISTICS` visas nedan.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

En beskrivning av metadatakolumnnamnen ges nedan.

| Kolumnnamn | Beskrivning |
|---|---|
| `statsId` | Detta ID refererar till den temporära statistiktabellen som genereras av kommandot `COMPUTE STATISTICS`. |
| `tableName` | Den ursprungliga tabell som användes för analysen. |
| `columnSet` | En lista med kolumner som valts ut särskilt för analys. Ett tomt värde anger att alla kolumner analyserades. Mer information finns i avsnittet [Begränsa kolumner](#limit-included-columns). |
| `filterContext` | En lista över eventuella filter som använts på analysen. |
| `timestamp` | Alla kronologiska filter som tillämpas på dataanalysen för att fokusera på en viss period. Mer information finns i avsnittet [villkor för tidsstämpelfilter](#filter-condition). |

Du kan använda statistikens ID eller aliasnamnet för att söka efter den beräknade statistiken med en SELECT-sats när som helst under sessionen. Statistik-ID:t och den genererade statistiken är bara giltiga för den aktuella sessionen och kan inte nås mellan olika PSQL-sessioner. Den beräknade statistiken är för närvarande inte beständig. Mer information finns i avsnittet [Visa utdata för din beräknade statistik](#view-output-of-computed-statistics).

## Begränsa de inkluderade kolumnerna {#limit-included-columns}

Om du vill fokusera analysen kan du beräkna statistik för särskilda datauppsättningskolumner genom att referera till dem efter namn. Använd syntaxen `FOR COLUMNS (<col1>, <col2>)` för att ange specifika kolumner som mål. I exemplet nedan beräknas statistik för kolumnerna `commerce`, `id` och `timestamp` för datamängden `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Du kan beräkna statistik för alla rotnivåer eller kapslade kolumner. I följande exempel visas dessa referenser.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Lägga till ett tidsstämpelfiltervillkor {#filter-condition}

Om du vill fokusera analysen av kolumnerna baserat på kronologi kan du lägga till ett tidsstämpelfiltervillkor. Det här villkoret kan användas för att filtrera bort historiska data eller fokusera dataanalysen på en viss period. Kommandot `FILTERCONTEXT` beräknar statistik på en delmängd av datauppsättningen baserat på det filtervillkor som du anger.

I exemplet nedan beräknas statistik för alla kolumner för datamängden `tableName`, där kolumntidsstämpeln har värden mellan det angivna intervallet `2023-04-01 00:00:00` och `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Du kan kombinera kolumngränsen och filtret för att skapa mycket specifika datorfrågor för dina datauppsättningskolumner. Följande fråga beräknar till exempel statistik för kolumnerna `commerce`, `id` och `timestamp` för datauppsättningen `tableName`, där kolumnens tidsstämpel har värden mellan det angivna intervallet `2023-04-01 00:00:00` och `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Nästa steg {#next-steps}

Genom att läsa det här dokumentet får du nu en bättre förståelse för hur du genererar kolumnnivåstatistik från en ADLS-datauppsättning med hjälp av en SQL-fråga. Du rekommenderas att läsa [SQl-syntaxguiden](../sql/syntax.md) för att upptäcka fler funktioner i Adobe Experience Platform Query Service.
