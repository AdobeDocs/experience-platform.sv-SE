---
title: Regressionsalgoritmer
description: Lär dig hur du konfigurerar och optimerar olika regressionsalgoritmer med hjälp av nyckelparametrar, beskrivningar och exempelkod för att implementera avancerade statistiska modeller.
role: Developer
exl-id: d38733bb-0420-40bf-a70b-19e0e0e58730
source-git-commit: 8b9cfb48a11701f0e4b358416c6b627bedf1db8b
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 2%

---

# Regressionsalgoritmer {#regression-algorithms}

Detta dokument ger en översikt över olika regressionsalgoritmer, med fokus på deras konfiguration, nyckelparametrar och praktiska användning i avancerade statistiska modeller. Regressionsalgoritmer används för att modellera förhållandet mellan beroende och oberoende variabler, och förutsäga kontinuerliga utfall baserat på observerade data. Varje avsnitt innehåller parameterbeskrivningar och exempelkod som hjälper dig att implementera och optimera dessa algoritmer för uppgifter som linjära, slumpmässiga skogar och överlevnadsregression.

## [!DNL Decision Tree]-regression {#decision-tree-regression}

[!DNL Decision Tree]-inlärning är en övervakad inlärningsmetod som används i statistik, datautvinning och maskininlärning. I detta tillvägagångssätt används ett klassificerings- eller regressionsbeslutsträd som en prediktiv modell för att dra slutsatser om en uppsättning observationer.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfiguration och optimering av prestanda för beslutsträdsmodeller.

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Den här parametern anger det maximala antalet behållare som används för att diskretisera kontinuerliga funktioner och bestämma delningar vid varje nod. Fler behållare ger finare granularitet och detaljskärpa. | 32 | Måste vara minst 2 och minst antalet kategorier i någon kategorifunktion. |
| `CACHE_NODE_IDS` | Den här parametern avgör om nod-ID:n för varje instans ska cachelagras. Om det är `false` skickar algoritmen träd till exekverare för att matcha instanser med noder. Om `true` cachelagras nod-ID:n för varje instans, vilket kan snabba upp träningen av djupare träd. Användare kan konfigurera hur ofta cachen ska kontrolleras eller inaktivera den genom att ställa in `CHECKPOINT_INTERVAL`. | false | `true` eller `false` |
| `CHECKPOINT_INTERVAL` | Den här parametern anger hur ofta de cachelagrade nod-ID:n ska kontrolleras. Om du till exempel anger `10` kontrolleras cachen var 10:e iteration. Detta gäller endast om `CACHE_NODE_IDS` är inställt på `true` och kontrollpunktskatalogen är konfigurerad i `org.apache.spark.SparkContext`. | 10 | (>=1) |
| `IMPURITY` | Den här parametern anger det kriterium som används för att beräkna informationsökning. Värden som stöds är `entropy` och `gini`. | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Den här parametern anger trädets maximala djup. Ett djup på `0` betyder till exempel 1 lövnod, medan ett djup på `1` betyder 1 intern nod och 2 lövnoder. Djupet måste ligga inom intervallet `[0, 30]`. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Den här parametern anger den minsta informationsökning som krävs för att en delning ska anses giltig i en trädnod. | 0,0 | (>=0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Den här parametern anger den minsta delen av det viktade samplingsantalet som varje underordnad nod måste ha efter en delning. Om någon av de underordnade noderna har en bråkdel som är mindre än det här värdet ignoreras delningen. | 0,0 | [0.0, 0.5] |
| `MIN_INSTANCES_PER_NODE` | Den här parametern anger det minsta antal instanser som varje underordnad nod måste ha efter en delning. Om en delning resulterar i färre instanser än det här värdet ignoreras delningen som ogiltig. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Den här parametern anger det maximala minne (i MB) som tilldelats för histogramaggregering. Om minnet är för litet delas bara en nod per iteration, och dess aggregat kan överskrida den här storleken. | 256 | Valfritt positivt heltalsvärde |
| `PREDICTION_COL` | Den här parametern anger namnet på den kolumn som används för att lagra förutsägelser. | &quot;förutsägelse&quot; | Valfri sträng |
| `SEED` | Den här parametern anger det slumpmässiga startvärde som används i modellen. | Ingen | Valfritt 64-bitars tal |
| `WEIGHT_COL` | Den här parametern anger namnet på viktkolumnen. Om den här parametern inte har angetts eller är tom behandlas alla instansvikter som `1.0`. | Ej angiven | Valfri sträng |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Factorization Machines]-regression {#factorization-machines-regression}

[!DNL Factorization Machines] är en algoritm för regressionsinlärning som stöder normal övertoningsnedbrytning och AdamW-lösaren. Algoritmen baseras på papperet från S. Rendle (2010), [!DNL Factorization Machines].

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestandan för regressionen [!DNL Factorization Machines].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|------------------------|-------------------------------------------------------------------------------------------------|---------------|-----------------------|
| `TOL` | Den här parametern anger algoritmens konverteringstolerans. Högre värden kan ge snabbare konvergens men mindre precision. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Den här parametern definierar faktorernas dimensionalitet. Högre värden ökar modellens komplexitet. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Den här parametern anger om modellen ska innehålla en spärrterm. | `true` | `true`, `false` |
| `FIT_LINEAR` | Den här parametern anger om en linjär term (kallas även 1-vägsterm) ska inkluderas i modellen. | `true` | `true`, `false` |
| `INIT_STD` | Den här parametern definierar standardavvikelsen för de ursprungliga koefficienterna som används i modellen. | 0,01 | (>= 0) |
| `MAX_ITER` | Den här parametern anger det maximala antalet iterationer som algoritmen ska köras. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Den här parametern ställer in minibatchfraktionen, som bestämmer den del av data som används i varje sats. Det måste vara inom intervallet `(0, 1]`. | 1,0 | `(0, 1]` |
| `REG_PARAM` | Den här parametern ställer in regulariseringsparametern för att förhindra överpassning. | 0,0 | (>= 0) |
| `SEED` | Den här parametern anger det slumpmässiga startvärde som används för modellinitiering. | Ingen | Valfritt 64-bitars tal |
| `SOLVER` | Den här parametern anger den lösaralgoritm som används för optimering. | &quot;adamW&quot; | `gd` (övertoningsdescent), `adamW` |
| `STEP_SIZE` | Den här parametern anger den inledande stegstorleken (eller inlärningsgraden) för det första optimeringssteget. | 1,0 | Valfritt positivt värde |
| `PREDICTION_COL` | Den här parametern anger namnet på kolumnen där förutsägelser lagras. | &quot;förutsägelse&quot; | Valfri sträng |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Generalized Linear]-regression {#generalized-linear-regression}

Till skillnad från linjär regression, som förutsätter att resultatet följer en normal (Gaussisk) fördelning, tillåter [!DNL Generalized Linear] modeller (GLM) att resultatet följer olika typer av distributioner, som [!DNL Poisson] eller binomial, beroende på datatypen.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestandan för regressionen [!DNL Generalized Linear].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Anger maximalt antal iterationer (kan användas när lösaren `irls` används). | 25 | (>= 0) |
| `REG_PARAM` | Parametern för reglering. | INTE ANGIVEN | (>= 0) |
| `TOL` | Konvergenstoleransen. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Det föreslagna djupet för `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | Family-parametern som beskriver felfördelningen som används i modellen. De alternativ som stöds är `gaussian`, `binomial`, `poisson`, `gamma` och `tweedie`. | &quot;gaussian&quot; | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | Om en spärrterm ska passas in. | `true` | `true`, `false` |
| `LINK` | Länk-funktionen som definierar relationen mellan den linjära prediktorn och fördelningsfunktionens medelvärde. De alternativ som stöds är `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog` och `sqrt`. | INTE ANGIVEN | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | Den här parametern anger indexvärdet i funktionen för strömlänk. Parametern gäller bara för familjen [!DNL Tweedie]. Om den inte anges är den som standard `1 - variancePower`, vilket justeras mot R `statmod`-paketet. Specifika länkkrafter på 0, 1, -1 och 0,5 motsvarar länkarna Log, Identity, Inverse och Sqrt. | 1 | Valfritt numeriskt värde |
| `SOLVER` | Den lösaralgoritm som används för optimering. Alternativ som stöds: `irls` (iterativt omviktade minst fyrkanter). | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | Den här parametern anger kraften i variansfunktionen för distributionen [!DNL Tweedie], vilket definierar relationen mellan variansen och medelvärdet. Värden som stöds är 0 och `[1, inf)`. Varianseffekterna 0, 1 och 2 motsvarar familjerna Gaussian, Poisson och Gamma. | 0,0 | 0, `[1, inf)` |
| `LINK_PREDICTION_COL` | Kolumnnamnet för länkförutsägelse (linjär prediktor). | INTE ANGIVEN | Valfri sträng |
| `OFFSET_COL` | Förskjutningskolumnens namn. Om den inte anges behandlas alla förekomstförskjutningar som 0,0. Förskjutningsfunktionen har en konstant koefficient på 1,0. | INTE ANGIVEN | Valfri sträng |
| `WEIGHT_COL` | Namnet på viktkolumnen. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. I Binomialfamiljen motsvarar vikter antalet försök och vikter som inte är heltal avrundas vid AIC-beräkning. | INTE ANGIVEN | Valfri sträng |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree]-regression {#gradient-boosted-tree-regression}

Övertoningsdrivna träd (GBT) är en effektiv metod för klassificering och regression som kombinerar förutsägelser från flera beslutsträd för att förbättra prediktiv precision och modellprestanda.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestandan för regressionen [!DNL Gradient Boosted Tree].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Det maximala antalet behållare som används för att dela upp kontinuerliga funktioner i diskreta intervall, vilket hjälper till att avgöra hur funktioner delas vid varje beslutsträdsnod. Fler behållare ger högre granularitet. | 32 | Måste vara minst 2 och lika med eller större än antalet kategorier i någon kategorifunktion. |
| `CACHE_NODE_IDS` | Om det är `false` skickar algoritmen träd till exekverare för att matcha instanser med noder. Om det är `true` cachelagrar algoritmen nod-ID:n för varje instans. Cachelagring kan påskynda utbildningen av djupare träd. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Anger hur ofta cachelagrade nod-ID:n ska kontrolleras. `10` betyder till exempel att cachen är kontrollerad var 10:e iteration. | 10 | (>= 1) |
| `MAX_DEPTH` | Trädets maximala djup (icke-negativt). Djup `0` betyder till exempel 1 lövnod och djup `1` betyder 1 intern nod med 2 lövnoder. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Den minsta informationsökning som krävs för att en delning ska kunna beaktas vid en trädnod. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Den minsta fraktionen av det viktade antalet sampel som varje underordnad måste ha efter en delning. Om en delning gör att den totala viktdelen i något av de underordnade blir mindre än det här värdet, tas den bort. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Det minsta antalet instanser som varje underordnad måste ha efter en delning. Om en delning resulterar i färre instanser än det här värdet ignoreras delningen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Det maximala minne (i MB) som allokeras till histogramaggregering. Om det här värdet är för litet delas endast en nod per iteration, och dess aggregat kan överskrida den här storleken. | 256 | Valfritt positivt heltalsvärde |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `VALIDATION_INDICATOR_COL` | Kolumnnamnet anger om varje rad används för utbildning eller validering. `false` för utbildning och `true` för validering. | INTE ANGIVEN | Valfri sträng |
| `LEAF_COL` | Kolumnnamnet för bladindex. Det förväntade lövindexvärdet för varje instans i varje träd, som genereras av förorderbläddring. | &quot;&quot; | Valfri sträng |
| `FEATURE_SUBSET_STRATEGY` | Den här parametern anger hur många funktioner som ska användas för delning vid varje trädnod. | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2` eller ett bråk mellan 0 och 1.0 |
| `SEED` | Det slumpmässiga utsädet. | INTE ANGIVEN | Valfritt 64-bitars tal |
| `WEIGHT_COL` | Kolumnnamnet, till exempel, vikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN | Valfri sträng |
| `LOSS_TYPE` | Den här parametern anger den förlustfunktion som modellen [!DNL Gradient Boosted Tree] minimerar. | &quot;fyrkant&quot; | `squared` (L2) och `absolute` (L1). Obs! Värdena är skiftlägeskänsliga. |
| `STEP_SIZE` | Stegstorleken (kallas även inlärningsgrad) i intervallet `(0, 1]`, som används för att minska bidraget från varje uppskattare. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Maximalt antal iterationer för algoritmen. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Den del av utbildningsdata som används för att lära sig varje beslutsträd, i intervallet `(0, 1]`. | 1,0 | `(0, 1]` |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Isotonic]-regression {#isotonic-regression}

[!DNL Isotonic Regression] är en algoritm som används för att iterativt justera avstånd samtidigt som den relativa ordningen för skillnader i data bevaras.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för [!DNL Isotonic Regression].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Anger om utdatasekvensen ska vara isoton (ökas) när `true` eller antitonisk (minskas) när `false`. | `true` | `true`, `false` |
| `WEIGHT_COL` | Kolumnnamnet, till exempel, vikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN | Valfri sträng |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `FEATURE_INDEX` | Indexvärdet för funktionen, som används när `featuresCol` är en vektorkolumn. Om det inte anges är standardvärdet `0`. Annars har det ingen effekt. | 0 | Valfritt icke-negativt heltal |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Linear]-regression {#linear-regression}

[!DNL Linear Regression] är en maskininlärningsalgoritm som övervakas och som passar en linjär ekvation till data för att modellera relationen mellan en beroende variabel och oberoende funktioner.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för [!DNL Linear Regression].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Det maximala antalet iterationer. | 100 | (>= 0) |
| `REGPARAM` | Den regulariseringsparameter som används för att kontrollera modellens komplexitet. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Blandningsparametern ElasticNet, som kontrollerar balansen mellan straffen L1 (Lasso) och L2 (Ridge). Värdet 0 ger L2-straffet, medan värdet 1 ger L1-straffet. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] är en ensemble-algoritm som bygger flera beslutsträd under träningen och returnerar den genomsnittliga prognosen för dessa träd för regressionsuppgifter, vilket bidrar till att förhindra överpassning.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för [!DNL Random Forest Regression].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Det högsta antalet behållare som används för att diskretisera kontinuerliga funktioner och avgöra hur funktioner delas vid varje nod. Fler behållare ger högre granularitet. | 32 | Måste vara minst 2 och minst lika med antalet kategorier i någon kategorifunktion. |
| `CACHE_NODE_IDS` | Om det är `false` skickar algoritmen träd till exekverare för att matcha instanser med noder. Om `true` cachelagras nod-ID:n för varje instans, vilket snabbar upp utbildningen av djupare träd. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Anger hur ofta cachelagrade nod-ID:n ska kontrolleras. `10` betyder till exempel att cachen är kontrollerad var 10:e iteration. | 10 | (>= 1) |
| `IMPURITY` | Det kriterium som används för beräkning av informationsvinst (skiftlägesokänslig). | &quot;entropi&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Trädets maximala djup (icke-negativt). Djup `0` betyder till exempel 1 lövnod och djup `1` betyder 1 intern nod och 2 lövnoder. | 5 | Valfritt icke-negativt heltal |
| `MIN_INFO_GAIN` | Den minsta informationsökning som krävs för att en delning ska kunna beaktas vid en trädnod. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Den minsta fraktionen av det viktade antalet sampel som varje underordnad måste ha efter en delning. Om en delning gör att andelen av den totala vikten i något av de underordnade blir mindre än det här värdet, tas den bort. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Det minsta antalet instanser som varje underordnad måste ha efter en delning. Om en delning resulterar i färre instanser än det här värdet ignoreras delningen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Det maximala minne (i MB) som allokeras till histogramaggregering. Om det här värdet är för litet delas endast en nod per iteration, och dess aggregat kan överskrida den här storleken. | 256 | (>= 1) |
| `BOOTSTRAP` | Om bootstrap-prover ska användas när träd byggs. | TRUE | `true`, `false` |
| `NUM_TREES` | Antalet träd som ska tränas (minst 1). Om `1` används ingen startspärr. Om det är större än `1` används startspärr. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Den del av utbildningsdata som används för att utbilda varje beslutsträd, i intervallet `(0, 1]`. | 1,0 | (>= 0.0, &lt;= 1) |
| `LEAF_COL` | Kolumnnamnet för bladindex, som är det förväntade lövindexet för varje instans i varje träd, som genereras av förordertraversal. | &quot;&quot; | Valfri sträng |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `SEED` | Det slumpmässiga utsädet. | INTE ANGIVEN | Valfritt 64-bitars tal |
| `WEIGHT_COL` | Kolumnnamnet, till exempel, vikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN | Ett giltigt kolumnnamn eller lämna tomt. |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] används för att passa en parametrisk överlevnadsregressionsmodell, som kallas [!DNL Accelerated Failure Time] (AFT)-modellen, baserat på [!DNL Weibull distribution]. Den kan stapla instanser i block för bättre prestanda.

**Parametrar**

Tabellen nedan visar nyckelparametrar för konfigurering och optimering av prestanda för [!DNL Survival Regression].

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Det maximala antalet iterationer som algoritmen ska köras. | 100 | (>= 0) |
| `TOL` | Konvergenstoleransen. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Det föreslagna djupet för `treeAggregate`. Om funktionsdimensionerna eller antalet partitioner är stora kan den här parametern anges till ett större värde. | 2 | (>= 2) |
| `FIT_INTERCEPT` | Om en spärrterm ska passas in. | TRUE | `true`, `false` |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |
| `CENSOR_COL` | Kolumnnamnet för censoring. Värdet `1` anger att händelsen har inträffat (utan censur), medan `0` betyder att händelsen har censur. | &quot;censor&quot; | 0, 1 |
| `MAX_BLOCK_SIZE_IN_MB` | Maximalt minne i MB för att stapla indata i block. Om den återstående datastorleken i en partition är mindre justeras värdet därefter. Värdet `0` tillåter automatisk justering. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Nästa steg

När du har läst det här dokumentet vet du nu hur du konfigurerar och använder olika regressionsalgoritmer. Läs sedan dokumenten om [klassificering](./classification.md) och [klustring](./clustering.md) om du vill veta mer om andra typer av avancerade statistiska modeller.
