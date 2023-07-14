---
title: Dataset Statistik - beräkning
description: I det här dokumentet beskrivs hur du beräknar kolumnnivåstatistik för ADLS-datauppsättningar (Azure Data Lake Storage) med SQL-kommandon.
source-git-commit: c7bc395038906e27449c82c518bd33ede05c5691
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Datauppsättningsstatistikberäkning

Nu kan du beräkna kolumnnivåstatistik för [!DNL Azure Data Lake Storage] (ADLS) datauppsättningar med `COMPUTE STATISTICS` och `SHOW STATISTICS` SQL-kommandon. SQL-kommandona som beräknar datauppsättningsstatistik är ett tillägg till `ANALYZE TABLE` -kommando. Fullständig information om `ANALYZE TABLE` finns i [SQL-referensdokumentation](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>För närvarande gäller den genererade statistiken endast för den sessionen och är inte beständig mellan sessionerna. De kan inte nås över olika PSQL-sessioner.

Med `SHOW STATISTICS FOR <alias_name>` kan du se statistik som har beräknats med `ANALYZE TABLE COMPUTE STATISTICS` -kommando. Genom att kombinera dessa kommandon kan du nu beräkna kolumnstatistik för antingen hela datauppsättningen, en deluppsättning av en datauppsättning, alla kolumner eller en deluppsättning av kolumner.

>[!IMPORTANT]
>
>The `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`och `SHOW STATISTICS` -kommandon stöds inte i data warehouse-tabeller. Dessa tillägg för `ANALYZE TABLE` -kommandon stöds för närvarande bara för ADLS-tabeller. Mer information finns i [ANALYSERA TABELLavsnittet](../sql/syntax.md#analyze-table) i SQL-syntaxguiden.

Den här guiden hjälper dig att strukturera dina frågor så att du kan beräkna kolumnstatistiken för en ADLS-datauppsättning. Med dessa kommandon kan du se statistik som genererats under sessionen via en PSQL-klient med hjälp av en SQL-fråga.

## Beräkningsstatistik {#compute-statistics}

Ytterligare konstruktioner har lagts till i `ANALYZE TABLE` kommando som gör att du kan **Beräkna statistik för en delmängd av en datauppsättning och för vissa kolumner**. För att göra detta måste du använda `ANALYZE TABLE <tableName> COMPUTE STATISTICS` format.

>[!IMPORTANT]
>
>Standardbeteendet beräknar statistik för **hel datauppsättning** och for **alla kolumner**. Om du vill beräkna statistik för alla kolumner använder du frågeformatet `ANALYZE TABLE COMPUTE STATISTICS`. Du är **not** rekommenderas att använda detta på en ADLS-datauppsättning, eftersom datauppsättningens storlek kan vara mycket stor (potentiellt antal databyte). I stället bör du alltid överväga att köra analyskommandot med `FILTERCONTEXT` och en angiven lista med kolumner. Se avsnitten om [begränsa analyserade kolumner](#limit-included-columns) och [lägga till ett filtervillkor](#filter-condition) för mer information.

Exemplet nedan beräknar statistik för `adc_geometric` datauppsättning och för **alla** -kolumner i datauppsättningen.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` stöder inte datatyperna array eller map. Du kan ange en `skip_stats_for_complex_datatypes` flagga som ska meddelas eller felas om indatabildrutan har kolumner med arrayer och mappningsdatatyper. Som standard är flaggan inställd på true. Använd följande kommando om du vill aktivera meddelanden eller fel: `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

Konsolutdata visar inte statistik som svar på kommandot för att analysera tabellberäkningsstatistik. Istället visas en radkolumn i konsolen `Statistics ID` med en unik identifierare som refererar till resultaten. Du kan också välja att **fråga direkt på`Statistics ID`**. När en `COMPUTE STATISTICS` -frågan, visas resultaten enligt följande:

```console
| Statistics ID    | 
| ---------------- |
| adc_geometric_stats_1 |
(1 row)
```

Du kan fråga statistikutdata direkt genom att referera till `Statistics ID` enligt nedan:

```sql
SELECT * FROM adc_geometric_stats_1; 
```

Med den här programsatsen kan du visa utdata på ungefär samma sätt som kommandot VISA STATISTIK när det används med `Statistics ID`.

Du kan visa en lista med all beräknad statistik i sessionen genom att köra kommandot VISA STATISTIK. Ett exempel på hur kommandot VISA STATISTIK visas nedan.

```console
statsId | tableName | columnSet | filterContext | timestamp
-----------+---------------+-----------+---------------------------------------+---------------
adc_geometric_stats_1 |adc_geometric | (age) | | 25/06/2023 09:22:26
demo_table_stats_1 | demo_table | (*) | ((age > 25)) | 25/06/2023 12:50:26
```

<!-- Commented out until the <alias_name> feature is released.

To see the output, you must use the `SHOW STATISTICS` command. Instructions on [how to show the statistics](#show-statistics) are provided later in the document. 

-->

## Begränsa de inkluderade kolumnerna {#limit-included-columns}

Du kan beräkna statistik för särskilda datauppsättningskolumner genom att referera till dem efter namn. Använd `FOR COLUMNS (<col1>, <col2>)` syntax för att ange specifika kolumner som mål. Exemplet nedan beräknar statistik för kolumnerna  `commerce`, `id`och `timestamp` för datauppsättningen `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Du kan beräkna statistik för alla rotnivåer eller kapslade kolumner. I följande exempel visas dessa referenser.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Lägga till ett tidsstämpelfiltervillkor {#filter-condition}

Du kan lägga till ett tidsstämpelfiltervillkor för att fokusera analysen av kolumnerna. Detta kan användas för att filtrera bort historiska data eller fokusera dataanalysen på en viss period. The `FILTERCONTEXT` kommandot beräknar statistik på en delmängd av datauppsättningen baserat på det filtervillkor du anger.

I exemplet nedan beräknas statistik för alla kolumner för datauppsättningen `tableName`, där kolumntidsstämpeln har värden mellan det angivna intervallet för `2023-04-01 00:00:00` och `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Du kan kombinera kolumngränsen och filtret för att skapa mycket specifika datorfrågor för dina datauppsättningskolumner. Följande fråga beräknar till exempel statistik för kolumnerna `commerce`, `id`och `timestamp` för datauppsättningen `tableName`, där kolumntidsstämpeln har värden mellan det angivna intervallet för `2023-04-01 00:00:00` och `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

<!-- Commented out until the <alias_name> feature is released.
## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. 
-->

<!-- Commented out until the <alias_name> feature is released.

## Show the statistics {#show-statistics}

The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  

Even with a filter condition and a column list, the computation can target a large amount of data. Query Service generates a universally unique identifier for the statistics ID to store this calculated information. You can then use this statistics ID to look up the computed statistics with the `SHOW STATISTICS` command at any time within that session. 

The statistics ID and the statistics generated are only valid for this particular session and cannot be accessed across different PSQL sessions. The computed statistics are not currently persistent. To display the statistics, use the command seen below.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

An output might look similar to the example below. 

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
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

-->

## Nästa steg {#next-steps}

Genom att läsa det här dokumentet får du nu en bättre förståelse för hur du genererar kolumnnivåstatistik från en ADLS-datauppsättning med en SQL-fråga. Du rekommenderas att läsa [SQl syntaxguide](../sql/syntax.md) om du vill veta mer om Adobe Experience Platform Query Service.
