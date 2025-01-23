---
title: Rotfiltrering med statistik och maskininlärning
description: Lär dig använda statistik från Data Distiller och maskininlärning för att identifiera och filtrera robotaktiviteter för att säkerställa korrekt analys och förbättrad dataintegritet.
source-git-commit: a8abbf61bdc646c0834c296a64b27c71c98ea1d3
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# Filtrera snabbt med statistik och maskininlärning

De praktiska tillämpningarna av robotfiltrering omfattar olika branscher. Inom e-handeln förbättras tillförlitligheten i mätvärden för konverteringsgrader, nyhetswebbplatser kan dra nytta av att minska falska interaktionsvärden och annonsnätverk kan säkerställa rättvis fakturering. För att kunna upprätthålla korrekt analys och säkerställa dataintegritet i klientströmmar eller webbtrafikdata måste ni ta itu med båda aktiviteterna. Ni kan säkerställa högkvalitativa analysdata genom att använda Data Distiller för att implementera effektiv robotfiltrering och eliminera oönskad trafik.

Det här dokumentet innehåller en omfattande guide för att identifiera och filtrera robotaktiviteter med hjälp av SQL- och maskininlärningstekniker. Det presenterar en utveckling av komplementära strategier, som börjar med grundläggande filtrering och går vidare till maskininlärningsbaserad detektering och utvärdering. Använd det här robusta ramverket för att förbättra din robotidentifiering och bevara dataintegriteten.

## Förstå robotaktivitet {#understand-bot-activity}

Rotaktiviteten kan identifieras genom att man upptäcker toppar i användarens åtgärder inom specifika tidsintervall. Om en enskild användare till exempel klickar för mycket på en gång under en kort tid kan det tyda på båda beteendena. De två nyckelattributen som används vid båda filtreringen är:

- **ECID (Experience Cloud Visitor-ID):** Ett universellt, beständigt ID som identifierar besökare.
- **Tidsstämpel:** Tid och datum då en aktivitet inträffar på webbplatsen.

Exemplen nedan visar hur du använder SQL- och maskininlärningstekniker för att identifiera, förfina och förutse båda aktiviteterna. Använd dessa metoder för att förbättra dataintegriteten och säkerställa användbar analys.

## SQL-baserad robotfiltrering {#sql-based-bot-filtering}

Det här SQL-baserade robotfiltreringsexemplet visar hur du använder SQL-frågor för att definiera tröskelvärden och identifiera robotaktivitet baserat på fördefinierade regler. Detta grundläggande tillvägagångssätt hjälper till att identifiera avvikelser i webbtrafiken genom att eliminera ovanlig aktivitet. Genom att anpassa identifieringsregler med definierade trösklar och intervall kan du effektivt anpassa robotfiltreringen så att den passar dina specifika trafikmönster.

### Definiera tröskelvärden för robotaktivitet {#define-thresholds}

Börja med att analysera datauppsättningen för att identifiera och kategorisera användarbeteendet. Fokusera på attribut som ECID, tidsstämpel och `webPageDetails.name` (namnet på den webbsida som besöktes) för att gruppera användaråtgärder och upptäcka mönster som indikerar båda aktiviteterna.

SQL-frågan nedan visar hur du använder tröskelvärdet på mer än 60 klick på en minut för att identifiera misstänkt aktivitet:

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### Utöka till flera intervall {#expand-to-multiple-intervals}

Definiera sedan olika tidsintervall för tröskelvärden. Dessa intervall kan omfatta:

- **1-minutersintervall:** Upp till 60 klick.
- **5-minutersintervall:** Upp till 300 klick.
- **30-minutersintervall:** Upp till 1 800 klick.

Följande SQL-fråga skapar en vy med namnet `analytics_events_clicks_count_criteria` som hanterar tröskelvärden över flera intervall. Programsatsen konsoliderar klickantal i intervaller om 1 minut, 5 minuter och 30 minuter till en strukturerad datamängd och flaggar potentiell robotaktivitet baserat på fördefinierade tröskelvärden.

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

Programsatsen sammanfogar data från `table_count_1_min`, `table_count_5_mins` och `table_count_30_mins` med hjälp av värdet `mcid` och webbsidan. Sedan konsolideras antalet klick för varje användare med flera tidsintervall för att ge en fullständig bild av användaraktiviteten. Slutligen identifierar flaggningslogiken användare som överskrider 50 klick på en minut och markerar dem som&quot;bots&quot; (`isBot = 1`).

### Struktur för utdatauppsättning

Utdatadatauppsättningen är strukturerad med både platta och kapslade fält. Strukturen ger flexibilitet vid identifiering av onormal trafik och stöder avancerade filterstrategier som använder SQL och maskininlärning. De kapslade fälten innehåller `count` och `web` som kapslar in detaljerad information om aktivitetströsklar och webbsidor. Att hämta in dessa mätvärden innebär att funktioner enkelt kan extraheras för utbildnings- och förutsägelseuppgifter.

I följande schema visas strukturen för den resulterande datauppsättningen och hur kapslade och platta fält kan användas för effektiv bearbetning och robotidentifiering.

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### Den utdatauppsättning som ska användas för utbildning

Resultatet av det här uttrycket kan se ut ungefär som tabellen nedan. I tabellen fungerar kolumnen `isBot` som en etikett som skiljer mellan både robot- och icke-robotaktivitet.

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## Avancerade statistiska funktioner för robotfiltrering {#statistical-functions-for-bot-filtering}

Det andra exemplet bygger på grundläggande SQL-filtrering genom att inkludera maskininlärningstekniker för att förfina tröskelvärden och förbättra filtreringens precision. Genom att använda avancerade statistiska funktioner, som regressionsanalys eller klusteralgoritmer, introducerar det här tillvägagångssättet prediktiva funktioner som du kan använda för att utveckla modeller för att hantera komplexa datauppsättningar med större precision.

### Bygg en utbildningsdatamängd {#build-a-training-dataset}

Förbered först en datauppsättning med platta och kapslade strukturer som maskininlärningsmodellen kan använda (enligt beskrivningen ovan). Mer information om hur du gör detta finns i [Arbeta med kapslade datastrukturers dokumentation](../../key-concepts/nested-data-structures.md). Gruppera data efter tidsstämpel, användar-ID och webbsidesnamn för att identifiera mönster i båda aktiviteterna.

### Använd TRANSFORM- och OPTIONS-satser för att skapa modeller {#transform-and-preprocess}

Följ stegen nedan för att omvandla din datauppsättning och konfigurera din maskininlärningsmodell effektivt. Stegen visar hur du hanterar null-värden, förbereder funktioner och definierar modellens parametrar för optimala prestanda.

>[!TIP]
>
>Mer information om hur du använder omformningar och förbearbetar data finns i [dokumentationen om funktionsomformningstekniker](../feature-transformation.md).

1. Om du vill fylla null-värden i numeriska kolumner, strängkolumner och booleska kolumner använder du funktionerna `numeric_imputer`, `string_imputer` och `boolean_imputer`. Detta steg säkerställer att maskininlärningsalgoritmen kan bearbeta data utan fel.
2. Använd funktionsomformningar för att förbereda data för modellering. Använd `binarized`, `quantile_discretizer` eller `string_indexer` för att kategorisera eller standardisera kolumnerna. Därefter matar du in utdata från imputerarna (`numeric_imputer` och `string_imputer`) i efterföljande omformare som `string_indexer` eller `quantile_discretizer` för att skapa meningsfulla funktioner.
3. Använd funktionen `vector_assembler` för att kombinera de omformade kolumnerna till en enda funktionskolumn. Skala sedan funktionerna med `min_max_scaler` för att normalisera värdena för bättre modellprestanda. Obs! I SQL-exemplet blir den senaste omformningen som omnämns i TRANSFORM-satsen den funktionskolumn som används av maskininlärningsmodellen.
4. Ange modelltypen och eventuella andra hyperparametrar i OPTIONS-satsen. Till exempel valdes `decision_tree_classifier` här eftersom det här är ett klassificeringsproblem. Andra parametrar som `max_depth` har justerats (`MAX_DEPTH=4`) för att trimma modellen för bättre prestanda.
5. Kombinera funktioner och etikettera utdata. Använd SELECT-satsen för att ange datauppsättningen för utbildning. Den här satsen ska innehålla både funktionskolumner (`count_per_id`, `web`, `id`) och etikettkolumnen (`isBot`), som anger om en åtgärd troligtvis är en robot.

Programsatsen kan se ut ungefär som i exemplet nedan.

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**Resultat**

I resultaten som visas nedan har modellen `bot_filtering_model` skapats med ett unikt ID, namn och version. Dessa utdata fungerar som referens för att spåra och hantera modeller. Använd dessa referenser för att identifiera exakt den konfiguration och version som krävs för förutsägelser eller utvärderingar.

```console
           Created Model ID           |       Created Model       | Version
--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### Utvärdera den utbildade modellen {#evaluate-trained-model}

När du har skapat modellen använder du kommandot `MODEL_EVALUATE` för att utvärdera dess prestanda. Detta steg säkerställer att modellen uppfyller kraven på precision och prestanda för att upptäcka robotaktivitet.

Använd följande argument i SQL-kommandot för att utvärdera modellen:

1. Ange modellnamnet (`bot_filtering_model`) för att ange vilken modell som ska utvärderas. Namnet måste matcha det du skapade tidigare med kommandot `CREATE MODEL`.
2. Ange modellversionen (`1`) i det andra argumentet för att ange vilken version av modellen du vill utvärdera. Om det finns flera versioner ser det till att rätt version används.
3. Inkludera utvärderingsdatauppsättningen för att definiera datauppsättningen för utvärdering. Kontrollera att datauppsättningen innehåller samma funktionskolumner (`count_per_id`, `web`, `id`) och den etikettkolumn (`isBot`) som används under utbildning.

>[!NOTE]
>
>De omformningar som tillämpas under modellutbildning tillämpas automatiskt under utvärderingen.

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**Resultat**

Svaret innehåller mätvärden som precision, precision, återkallande och AUC-ROC. Resultaten bekräftar om modellen fungerade bra eller inte.

>[!NOTE]
>
>Värden i intervallet 0-1 representerar proportioner eller sannolikheter, där 1,0 anger perfekt prestanda.

```console
auc_roc | accuracy | precision | recall
---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **Mått** | **Beskrivning** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | Den här mätningen visar hur effektivt din modell kan klassificera både bågar och andra. Det används ofta för att utvärdera klassificeringsmodeller. |
| `accuracy` | Procentandelen korrekta prognoser som modellen gör. |
| `precision` | Andelen sanna robotprognoser bland alla förutspådda robotar. |
| `recall` | Andelen äkta bots som upptäckts av alla verkliga bots. |

>[!TIP]
>
>För användning i produktionssandlådor bör du överväga att utvärdera modellen på testdatamängder för att se till att den generaliseras effektivt.

### Prediktion av robotaktivitet {#predict-bot-activity}

Använd kommandot `MODEL_PREDICT` med den tränade modellen för att identifiera vilka användare (`id`) som är robotar. Följ stegen nedan för att generera prognoser för identifiering av robotaktivitet:

1. Använd modellnamnet (`bot_filtering_model`) i det första argumentet för att ange vilken modell som ska användas för förutsägelser.
2. Ange modellversionen (`1`) i det andra argumentet för att säkerställa att rätt version av modellen används.
3. Använd en SELECT-sats för att ange funktionskolumnerna (`count_per_id`, `web`, `id`) om du vill ange rätt data för förutsägelser. Inkludera inte etikettkolumnen (`isBot`) eftersom modellen genererar prognoser för det här fältet.

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**Resultat**

Svaret innehåller prognoser för varje användare (`id`) tillsammans med information om deras aktivitet och modellens klassificeringsresultat. Detta ger möjlighet till en detaljerad granskning av användarbeteende och modellens klassificering av båda aktiviteterna.

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

I tabellen nedan förklaras varje mätvärde:

| Kolumnnamn | Beskrivning |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | Unik identifierare för varje användare. |
| `count.one_minute` | De sammanlagda klickningarna räknas med 1 minuters intervall. |
| `count.five_minute` | De sammanlagda klickningarna räknas för 5 minuters intervall. |
| `count.thirty_minute` | De sammanlagda klickningarna räknas för 30-minutersintervall. |
| `web.webpagedetails.name` | Namnet på den besökta webbsidan. Detta ger kontext för användaraktivitet. |
| `prediction` | Modellens förutsägelse. Ett `1.0`-resultat indikerar att användaren har flaggats som en robot baserat på deras aktivitetsmönster. |

## Hantera dina modeller {#manage-models}

Om du vill hantera maskininlärningsmodeller använder du de SQL-nyckelord som listas i avsnittet nedan.

### Visa tillgängliga modeller {#list-available-models}

Hantera och granska modellerna effektivt med kommandot `SHOW MODELS;`. Det här kommandot visar alla maskininlärningsmodeller som har skapats på den aktuella arbetsytan. Utdata ger en översikt över tillgängliga modeller och innehåller namn, versioner och andra metadata.

```sql
SHOW MODELS;
```

### Ta bort modeller {#delete-models}

Om du vill frigöra resurser och se till att endast relevanta modeller behålls använder du kommandot `DROP MODEL` för att ta bort gamla eller onödiga modeller. Det här kommandot tar bort alla maskininlärningsmodeller som har angetts efter nyckelorden. I exemplet nedan har `bot_filtering_model` tagits bort från systemet.

```sql
DROP MODEL bot_filtering_model;
```

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig att identifiera och filtrera startaktivitet med hjälp av SQL- och maskininlärningstekniker med Data Distiller-metoder. Därefter kan du tillämpa dessa koncept på dina datauppsättningar och automatisera omskolning av modeller för kontinuerlig förbättring.
