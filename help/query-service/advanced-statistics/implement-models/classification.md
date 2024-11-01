---
title: Klassificeringsalgoritmer
description: Lär dig hur du konfigurerar och optimerar olika klassificeringsalgoritmer med nyckelparametrar, beskrivningar och exempelkod som hjälper dig att implementera avancerade statistiska modeller.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---

# Klassificeringsalgoritmer {#classification-algorithms}

Detta dokument ger en översikt över olika klassificeringsalgoritmer, med fokus på deras konfiguration, nyckelparametrar och praktiska användning i avancerade statistiska modeller. Klassificeringsalgoritmer används för att tilldela kategorier till datapunkter baserat på indatafunktioner. Varje avsnitt innehåller parameterbeskrivningar och exempelkod som hjälper dig att implementera och optimera dessa algoritmer för uppgifter som beslutsträd, slumpmässig skog och inbyggd Bayes-klassificering.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] är en övervakad inlärningsmetod som används för statistik, datautvinning och maskininlärning. I detta tillvägagångssätt används ett beslutsträd som en prediktiv modell för klassificeringsuppgifter, som bygger på slutsatser från en uppsättning observationer.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för en [!DNL Decision Tree Classifier].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | Det maximala antalet behållare avgör hur kontinuerliga funktioner delas upp i diskreta intervall. Detta påverkar hur funktioner delas vid varje beslutsträdsnod. Fler behållare ger högre granularitet. | 32 | Måste vara minst 2 och minst lika med antalet kategorier i någon kategorifunktion. |
| `CACHE_NODE_IDS` | Om det är `false` skickar algoritmen träd till exekverare för att matcha instanser med noder. Om `true` cachelagras nod-ID:n för varje instans, vilket snabbar upp utbildningen av djupare träd. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Anger hur ofta cachelagrade nod-ID:n ska kontrolleras. `10` betyder till exempel att cachen är kontrollpunkt var 10:e iteration. | 10 | (>= 1) |
| `IMPURITY` | Det kriterium som används för beräkning av informationsvinst (skiftlägesokänslig). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Trädets maximala djup (icke-negativt). Djup `0` betyder till exempel 1 lövnod och djup `1` betyder 1 intern nod och 2 lövnoder. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Den minsta informationsökning som krävs för att en delning ska kunna beaktas vid en trädnod. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Den minsta fraktionen av det viktade antalet sampel som varje underordnad måste ha efter en delning. Om en delning gör att andelen av den totala vikten i något av de underordnade blir mindre än det här värdet, tas den bort. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Det minsta antalet instanser som varje underordnad måste ha efter en delning. Om en delning resulterar i färre instanser än det här värdet ignoreras delningen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Det maximala minne (i MB) som allokeras till histogramaggregering. Om det här värdet är för litet delas endast en nod per iteration, och dess aggregat kan överskrida den här storleken. | 256 |                    |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `SEED` | Det slumpmässiga utsädet. | INTE ANGIVEN | Valfritt 64-bitars tal |
| `WEIGHT_COL` | Kolumnnamnet, till exempel, vikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN | Valfri sträng |
| `ONE_VS_REST` | Aktiverar eller inaktiverar radbrytning av den här algoritmen med ett mot ett, som används för klassproblem i flera klasser. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exempel**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

[!DNL Factorization Machine Classifier] är en klassificeringsalgoritm som stöder normal övertoningsnedbrytning och AdamW-lösaren. I klassificeringsmodellen för Factorization Machine används logistiska förluster som kan optimeras via övertoningsnedstaplar och ofta omfattar regulariseringsvillkor som L2 för att förhindra överpassning.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för [!DNL Factorization Machine Classifier].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | Konvergenstoleransen, som styr noggrannheten för optimeringen. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Faktorernas dimensionalitet. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Anger om en spärrterm ska passas in. | `true` | `true`, `false` |
| `FIT_LINEAR` | Anger om den linjära termen ska passas in (kallas även envägsperioden). | `true` | `true`, `false` |
| `INIT_STD` | Standardavvikelsen för initieringskoefficient. | 0,01 | (>= 0) |
| `MAX_ITER` | Maximalt antal iterationer som algoritmen ska köras. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Den del av data som ska användas i minibatchar under utbildning. Måste vara i intervallet `(0, 1]`. | 1,0 | `(0, 1]` |
| `REG_PARAM` | Parametern för reglering, som hjälper till att kontrollera modellens komplexitet och förhindra överpassning. | 0,0 | (>= 0) |
| `SEED` | Det slumpmässiga startvärdet för styrning av slumpmässiga processer i algoritmen. | INTE ANGIVEN | Valfritt 64-bitars tal |
| `SOLVER` | Den lösaralgoritm som används för optimering. De alternativ som stöds är `gd` (övertoningsfall) och `adamW`. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | Den inledande stegstorleken för optimering, som ofta tolkas som inlärningsgraden. | 1,0 | > 0 |
| `PROBABILITY_COL` | Kolumnnamnet för villkorliga klasssannolikheter. Obs! Alla modeller ger inte upphov till väl kalibrerade sannolikheter, utan bör behandlas som konfidensgrader i stället för som exakta sannolikheter. | &quot;sannolikhet&quot; | Valfri sträng |
| `PREDICTION_COL` | Kolumnnamnet för förväntade klassetiketter. | &quot;förutsägelse&quot; | Valfri sträng |
| `RAW_PREDICTION_COL` | Kolumnnamnet för råa förutsägelsevärden (kallas även konfidensvärden). | &quot;rawPredication&quot; | Valfri sträng |
| `ONE_VS_REST` | Anger om One-vs-Rest ska aktiveras för multiclass-klassificering. | FALSE | `true`, `false` |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

I [!DNL Gradient Boosted Tree Classifier] används en enda kombination av beslutsträd för att förbättra exaktheten i klassificeringsuppgifter, vilket kombinerar flera träd för att förbättra modellens prestanda.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för [!DNL Gradient Boosted Tree Classifier].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Det maximala antalet behållare avgör hur kontinuerliga funktioner delas upp i diskreta intervall. Detta påverkar hur funktioner delas vid varje beslutsträdsnod. Fler behållare ger högre granularitet. | 32 | Måste vara minst 2 och lika med eller större än antalet kategorier i någon kategorifunktion. |
| `CACHE_NODE_IDS` | Om det är `false` skickar algoritmen träd till exekverare för att matcha instanser med noder. Om `true` cachelagras nod-ID:n för varje instans, vilket snabbar upp utbildningen av djupare träd. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Anger hur ofta cachelagrade nod-ID:n ska kontrolleras. `10` betyder till exempel att cachen är kontrollpunkt var 10:e iteration. | 10 | (>= 1) |
| `MAX_DEPTH` | Trädets maximala djup (icke-negativt). Djup `0` betyder till exempel 1 lövnod och djup `1` betyder 1 intern nod och 2 lövnoder. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Den minsta informationsökning som krävs för att en delning ska kunna beaktas vid en trädnod. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Den minsta fraktionen av det viktade antalet sampel som varje underordnad måste ha efter en delning. Om en delning gör att andelen av den totala vikten i något av de underordnade blir mindre än det här värdet, tas den bort. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Det minsta antalet instanser som varje underordnad måste ha efter en delning. Om en delning resulterar i färre instanser än det här värdet ignoreras delningen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Det maximala minne (i MB) som allokeras till histogramaggregering. Om det här värdet är för litet delas endast en nod per iteration, och dess aggregat kan överskrida den här storleken. | 256 |                                                                                                      |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `VALIDATION_INDICATOR_COL` | Kolumnnamnet anger om varje rad används för utbildning eller validering. `false` för utbildning och `true` för validering. | INTE ANGIVEN | Valfri sträng |
| `RAW_PREDICTION_COL` | Kolumnnamnet för råa förutsägelsevärden (kallas även konfidensvärden). | &quot;rawPredication&quot; | Valfri sträng |
| `LEAF_COL` | Kolumnnamnet för bladindex, som är det förväntade lövindexet för varje instans i varje träd, som genereras av förordertraversal. | &quot;&quot; | Valfri sträng |
| `FEATURE_SUBSET_STRATEGY` | Antalet funktioner som kan delas vid varje trädnod. Alternativ som stöds: `auto`, `all`, `onethird`, `sqrt`, `log2` och `n` (för en del funktioner). | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` (där `n` är ett bråk mellan 0 och 1.0) |
| `WEIGHT_COL` | Kolumnnamnet, till exempel, vikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN |                                                                                                      |
| `LOSS_TYPE` | Förlustfunktionen som modellen [!DNL Gradient Boosted Tree] försöker minimera. Alternativ som stöds: `logistic`. | &quot;logistik&quot; | `logistic` |
| `STEP_SIZE` | Stegstorleken (kallas även inlärningsgrad) i intervallet `(0, 1]`, som används för att minska bidraget från varje uppskattare. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Maximalt antal iterationer för algoritmen. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Den del av utbildningsdata som används för att utbilda varje beslutsträd, i intervallet `(0, 1]`. | 1,0 | `(0, 1]` |
| `PROBABILITY_COL` | Kolumnnamnet för villkorliga klasssannolikheter. Obs! Alla modeller ger inte upphov till väl kalibrerade sannolikheter, utan bör behandlas som konfidensgrader i stället för som exakta sannolikheter. | &quot;sannolikhet&quot; | Valfri sträng |
| `ONE_VS_REST` | Aktiverar eller inaktiverar kapsling av den här algoritmen med One-vs-Rest för klassificering i flera klasser. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exempel**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (LinearSVC) {#linear-support-vector-classifier}

[!DNL Linear Support Vector Classifier] (LinearSVC) konstruerar ett hyperplan för att klassificera data i ett högdimensionellt rum. Du kan använda den för att maximera marginalen mellan klasser för att minimera klassificeringsfel.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för [!DNL Linear Support Vector Classifier (LinearSVC)].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | Maximalt antal iterationer som algoritmen ska köras. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | Det föreslagna djupet för trädaggregering. | 2 |                                                                                                      |
| `FIT_INTERCEPT` | Om en spärrterm ska passas in. | `true` | `true`, `false` |
| `TOL` | Konvergenstoleransen för optimering. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Maximalt minne i MB för att stapla indata i block. Data lagras inom partitioner och om den återstående datastorleken i en partition är mindre justeras det här värdet därefter. | 0,0 | (>= 0) |
| `REG_PARAM` | Parametern för reglering, som hjälper till att kontrollera modellens komplexitet och förhindra överpassning. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Om utbildningsfunktionerna ska standardiseras innan modellen anpassas. | `true` | `true`, `false` |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `RAW_PREDICTION_COL` | Kolumnnamnet för råa förutsägelsevärden (kallas även konfidensvärden). | &quot;rawPredication&quot; | Valfri sträng |
| `ONE_VS_REST` | Aktiverar eller inaktiverar kapsling av den här algoritmen med One-vs-Rest för klassificering i flera klasser. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exempel**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] är en övervakad algoritm som används för binär klassificering. Den modellerar sannolikheten för att en instans tillhör en klass med hjälp av logistikfunktionen, vilket gör den lämplig för uppgifter där målet är att klassificera instanser i en av två kategorier.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för [!DNL Logistic Regression].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | Maximalt antal iterationer som algoritmen körs. | 100 | (>= 0) |
| `REGPARAM` | Parametern för reglering används för att kontrollera modellens komplexitet. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Blandningsparametern `ElasticNet` styr balansen mellan straffen L1 (Lasso) och L2 (Ridge). Värdet 0 ger L2-straffet (Ridge, vilket minskar koefficienternas storlek), medan värdet 1 ger L1-straffet (Lasso, vilket uppmuntrar till glans genom att ställa in vissa koefficienter på noll). | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Exempel**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

[!DNL Multilayer Perceptron Classifier] är en artificiell neuralnätverksklassificerare som består av flera fullständigt anslutna lager av noder. Varje nod i ett lager mappar indata till utdata med en viktad linjär kombination av indata, med nodvikter (`w`) och avvikelse (`b`), följt av en aktiveringsfunktion. Denna process hjälper till att konfigurera och optimera avancerade statistiska modeller genom att justera nyckelparametrar, med kodexempel som ger ytterligare vägledning. —>

**Parametrar**

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Maximalt antal iterationer som algoritmen ska köras. | 100 | (>= 0) |
| `BLOCK_SIZE` | Blockstorleken för stapling av indata i matriser inom partitioner. Om blockstorleken överskrider de återstående data som finns i en partition justeras den därefter. | 128 | (>= 0) |
| `STEP_SIZE` | Stegstorleken som används för varje upprepning av optimeringen (gäller endast för lösaren `gd`). | 0,03 | (> 0) |
| `TOL` | Konvergenstoleransen för optimering. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `SEED` | Det slumpmässiga startvärdet för styrning av slumpmässiga processer i algoritmen. | INTE ANGIVEN | Valfritt 64-bitars tal |
| `PROBABILITY_COL` | Kolumnnamnet för villkorliga klasssannolikheter. Dessa bör behandlas som konfidensgrader i stället för som exakta sannolikheter. | &quot;sannolikhet&quot; | Valfri sträng |
| `RAW_PREDICTION_COL` | Kolumnnamnet för råa förutsägelsevärden (kallas även konfidensvärden). | &quot;rawPredication&quot; | Valfri sträng |
| `ONE_VS_REST` | Aktiverar eller inaktiverar kapsling av den här algoritmen med One-vs-Rest för klassificering i flera klasser. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] är en enkel sannolikhetsklassificerare i flera klasser som baseras på Bayes&#39; sats med starka (naiva) antaganden om oberoende mellan funktioner. Det är mycket effektivt i utbildningen och kräver endast en överföring av utbildningsdata för att beräkna den villkorliga sannolikhetsfördelningen för varje egenskap som anges på respektive etikett. För förutsägelser använder den Bayes teori för att beräkna den villkorliga sannolikhetsfördelningen för varje etikett utifrån en observation.

**Parametrar**

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Anger modelltypen. De alternativ som stöds är `"multinomial"`, `"complement"`, `"bernoulli"` och `"gaussian"`. Modelltypen är skiftlägeskänslig. | &quot;multi omial&quot; | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | Parametern smoothing, som används för att jämna ut kategoriserade data och hantera osynliga funktioner. | 1,0 | (>= 0) |
| `PROBABILITY_COL` | Kolumnnamnet för villkorliga klasssannolikheter. Dessa bör behandlas som konfidensgrader i stället för som exakta sannolikheter. | &quot;sannolikhet&quot; | Valfri sträng |
| `WEIGHT_COL` | Kolumnnamnet för instansvikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN | Valfri sträng |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `RAW_PREDICTION_COL` | Kolumnnamnet för råa förutsägelsevärden (kallas även konfidensvärden). | &quot;rawPredication&quot; | Valfri sträng |
| `ONE_VS_REST` | Anger om One-vs-Rest ska aktiveras för multiclass-klassificering. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] är en enastående inlärningsalgoritm som bygger flera beslutsträd under utbildning. Det minskar överpassningen genom att man beräknar medelvärdet och väljer den klass som valts av de flesta träd för klassificeringsuppgifter.

**Parametrar**

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Det maximala antalet behållare avgör hur kontinuerliga funktioner delas upp i diskreta intervall. Detta påverkar hur funktioner delas vid varje beslutsträdsnod. Fler behållare ger högre granularitet. | 32 | Måste vara minst 2 och lika med eller större än antalet kategorier i någon kategorifunktion. |
| `CACHE_NODE_IDS` | Om det är `false` skickar algoritmen träd till exekverare för att matcha instanser med noder. Om `true` cachelagras nod-ID:n för varje instans, vilket snabbar upp utbildningsprocessen. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Anger hur ofta cachelagrade nod-ID:n ska kontrolleras. `10` betyder till exempel att cachen är kontrollpunkt var 10:e iteration. | 10 | (>= 1) |
| `IMPURITY` | Det kriterium som används för beräkning av informationsvinst (skiftlägesokänslig). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Trädets maximala djup (icke-negativt). Djup `0` betyder till exempel 1 lövnod och djup `1` betyder 1 intern nod och 2 lövnoder. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Den minsta informationsökning som krävs för att en delning ska kunna beaktas vid en trädnod. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Den minsta fraktionen av det viktade antalet sampel som varje underordnad måste ha efter en delning. Om en delning gör att andelen av den totala vikten i något av de underordnade blir mindre än det här värdet, tas den bort. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Det minsta antalet instanser som varje underordnad måste ha efter en delning. Om en delning resulterar i färre instanser än det här värdet ignoreras delningen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Det maximala minne (i MB) som allokeras till histogramaggregering. Om det här värdet är för litet delas endast en nod per iteration, och dess aggregat kan överskrida den här storleken. | 256 | (>= 1) |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `WEIGHT_COL` | Kolumnnamnet, till exempel, vikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN | Valfri sträng |
| `SEED` | Det slumpmässiga startvärde som används för att styra slumpmässiga processer i algoritmen. | -1689246527 | Valfritt 64-bitars tal |
| `BOOTSTRAP` | Anger om bootstrap-prover ska användas när träd byggs. | `true` | `true`, `false` |
| `NUM_TREES` | Antalet träd som ska tränas. Om `1` används ingen startspärr. Om det är större än `1` används startspärr. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Den del av utbildningsdata som används för inlärning av varje beslutsträd. | 1,0 | (> 0, &lt;= 1) |
| `LEAF_COL` | Kolumnnamnet för bladindexen, som innehåller det förväntade bladindexet för varje instans i varje träd efter förordning. | &quot;&quot; | Valfri sträng |
| `PROBABILITY_COL` | Kolumnnamnet för villkorliga klasssannolikheter. Dessa bör behandlas som konfidensgrader i stället för som exakta sannolikheter. | &quot;sannolikhet&quot; | Valfri sträng |
| `RAW_PREDICTION_COL` | Kolumnnamnet för råa förutsägelsevärden (kallas även konfidensvärden). | &quot;rawPredication&quot; | Valfri sträng |
| `ONE_VS_REST` | Anger om One-vs-Rest ska aktiveras för multiclass-klassificering. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exempel**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Nästa steg

När du har läst det här dokumentet vet du nu hur du konfigurerar och använder olika klassificeringsalgoritmer. Läs sedan dokumenten om [regression](./regression.md) och [klustring](./clustering.md) om du vill veta mer om andra typer av avancerade statistiska modeller.

