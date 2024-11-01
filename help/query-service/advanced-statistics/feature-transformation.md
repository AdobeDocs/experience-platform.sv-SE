---
title: Funktionsomformningstekniker
description: Lär dig mer om viktiga förbehandlingstekniker som dataomvandling, kodning och funktionsskalning, som förbereder data för utbildning i statistiska modeller. Det täcker vikten av att hantera saknade värden och konvertera kategoriserade data för att förbättra modellens prestanda och precision.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '3437'
ht-degree: 5%

---

# Funktionsomvandlingstekniker

Transformeringar är viktiga förbearbetningssteg som konverterar eller skalar data till ett format som är lämpligt för modellutbildning och -analys, vilket ger optimala prestanda och precision. Det här dokumentet fungerar som en extra syntaxresurs och innehåller detaljerad information om viktiga funktionsomformningstekniker för förbearbetning av data.

Maskinininlärningsmodeller kan inte direkt bearbeta strängvärden eller null-värden, vilket gör dataförbearbetning nödvändig. I den här guiden beskrivs hur du använder olika omformningar för att imputera saknade värden, konvertera kategoriserade data till numeriska format och tillämpa funktionens skalningstekniker, till exempel kodning och vektorisering med en aktivering. Dessa metoder gör det möjligt för modeller att tolka och lära sig effektivt av data, vilket i slutänden förbättrar deras prestanda.

## Automatisk funktionsomformning {#automatic-transformations}

Om du väljer att hoppa över `TRANSFORM`-satsen i ditt `CREATE MODEL`-kommando utförs funktionsomformningen automatiskt. Automatisk förbearbetning av data inkluderar null-ersättning och standardfunktionsomvandlingar (baserat på datatypen). Numeriska kolumner och textkolumner imputeras automatiskt, och funktionsomformningar utförs för att säkerställa att data har ett lämpligt format för maskininlärningsmodellutbildning. Den här processen inkluderar dataimputering som saknas samt kategoriserade, numeriska och booleska omformningar.

>[!IMPORTANT]
>
>Den funktionsomvandling som används vid tidpunkten för utbildningen kommer också att användas för funktionsomformning vid tidpunkten för förutsägelse och utvärdering.

I följande tabeller beskrivs hur olika datatyper hanteras när satsen `TRANSFORM` utelämnas under kommandot `CREATE MODEL`.

### Null-ersättning {#automatic-null-replacement}

| Datatyp | Null-ersättning |
|-----------------|-----------------------------------------------------|
| Numeriskt | Nuller ersätts med kolumnens medelvärde. |
| Kategorisisk | Nuller ersätts med nyckelordet `ml_unknown`. |
| Boolean | Nulls ersätts med ett `FALSE`-värde. |
| Tidsstämpel | Det här förväntas vara ett kontinuerligt fält. |
| Kapslad/STRUKTUR | Ersättningen beror på bladnodens datatyp. |

### Omvandling av funktioner {#automatic-feature-transformation}

| Datatyp | Funktionsomvandling |
|-----------------|-----------------------------------------------------|
| Numeriskt | INTE OBLIGATORISKT - Eftersom den här datatypen tolkas av maskininlärningsalgoritmer. |
| Sträng | Strängindexering sker. |
| Boolean | Strängindexering sker. |
| Tidsstämpel | Ingen åtgärd utförs. |
| STRUCT | Värdet expanderas till sin lövnod. Omvandlingen sker baserat på lövnodens datatyp. |

**exempel**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Manuella funktionsomvandlingar {#manual-transformations}

Om du vill definiera anpassad förbearbetning av data i `CREATE MODEL`-satsen använder du `TRANSFORM`-satsen i kombination med valfritt antal tillgängliga omformningsfunktioner. Dessa manuella förbearbetningsfunktioner kan också användas utanför `TRANSFORM`-satsen. Alla omformningar som beskrivs i avsnittet [transformator nedan](#available-transformations) kan användas för att förbearbeta data manuellt.

### Viktiga egenskaper

Följande är viktiga egenskaper i funktionsomformningen som du bör tänka på när du definierar förbearbetningsfunktionerna:

- **Syntax**: `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - Aliasnamnet är obligatoriskt i syntaxen. Du måste ange ett aliasnamn, annars misslyckas frågan.

- **Parametrar**: Parametrarna är positioneringsargument. Det innebär att varje parameter bara kan ta vissa värden. Mer information om vilken funktion som tar vilket argument finns i respektive dokumentation.

- **Klinande transformatorer**: Utdata från en transformator kan bli indata till en annan transformator.

- **Funktionsanvändning**: Den senaste funktionsomvandlingen används som en funktion i maskininlärningsmodellen.

**Exempel**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## Tillgängliga omformningar {#available-transformations}

Det finns 19 tillgängliga omformningar. Dessa omformningar delas upp i [Allmänna omformningar](#general-transformations), [Numeriska omformningar](#numeric-transformations), [Kategoriomformningar](#categorical-transformations) och [Textuella omformningar](#textual-transformations).

### Allmänna omformningar {#general-transformations}

I det här avsnittet finns mer information om de transformatorer som används för ett stort antal datatyper. Den här informationen är viktig om du behöver använda omformningar som inte är specifika för kategoriserade data eller textdata.

>[!NOTE]
>
>Datatypen input avser den kolumn som imputation tillämpas på. Datatypen output avser den kolumn som skapas som utdata när omformningen har börjat gälla.

#### Numerisk imputer {#numeric-imputer}

Transformeraren **Numerisk imputer** slutför saknade värden i en datauppsättning. Detta använder antingen medelvärdet, medianen eller läget för de kolumner där de saknade värdena finns. Indatakolumnerna ska vara antingen `DoubleType` eller `FloatType`. Mer information och exempel finns i dokumentationen för [Spark-algoritmen](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer).

>[!NOTE]
>
>Alla null-värden i indatakolumner behandlas som saknade och därför också imputerade.

**Datatyper**

- Indatatyp: Numerisk
- Datatyp för utdata: Numerisk

**Definition**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | En imputeringsstrategi. De tillgängliga värdena är: [`mean`, `median`, `mode`]. | string | medelvärde | valfri |

{style="table-layout:auto"}

**Exempel före imputation**

| id | timme |
|---|---|
| 0 | 18,0 |
| 1 | noll |
| 2 | 8,0 |

**Exempel efter imputation (med medelstrategi)**

| id | timme |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Strängimputer {#string-imputer}

Transformeraren **String imputer** slutför saknade värden i en datauppsättning med en sträng som anges av användaren som ett funktionsargument. Indata- och utdatakolumnerna ska vara datatypen `string`.

>[!NOTE]
>
>Alla null-värden i indatakolumner behandlas som saknade och ersätts med den angivna strängen.

**Datatyper**

- Indatatyp: String
- Datatyp för utdata: String

**Definition**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Värdet som ersätter null-värden. | string | ml_unknown | valfri |

{style="table-layout:auto"}

**Exempel före imputation**

| id | name |
|---|---|
| 0 | John |
| 1 | noll |
| 2 | Alice |

**Exempel efter imputation (använder &#39;ml_unknown&#39; som ersättning)**

| id | name |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Boolean imputer {#imputer}

Transformeraren **Boolean imputer** slutför saknade värden i en datauppsättning för en boolesk kolumn. Indata- och utdatakolumnerna ska vara av typen `Boolean`.

>[!NOTE]
>
>Alla null-värden i indatakolumner behandlas som saknade och ersätts med det angivna booleska värdet.

**Datatyper**

- Indatatyp: Boolean
- Datatyp för utdata: Boolean

**Definition**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Boolean imputer. Tillåt värden: [`true`, `false`]. | boolesk | false | valfri |

**Exempel före imputation**

| id | flagga |
|---|---|
| 0 | true |
| 1 | noll |
| 2 | false |

**Exempel efter imputation (använder &#39;true&#39; som ersättning)**

| id | flagga |
|---|---|
| 0 | true |
| 1 | true |
| 2 | false |

#### Vektormonterare {#vector-assembler}

Transformatorn `VectorAssembler` kombinerar en angiven lista med indatakolumner till en enda vektorkolumn, vilket gör det enklare att hantera flera funktioner i maskininlärningsmodeller. Detta är särskilt användbart när du vill sammanfoga råfunktioner och funktioner som genererats av olika funktionstransformerare i en enda funktionsvektor. `VectorAssembler` accepterar indatakolumner av numeriska, booleska och vektortyper. I varje rad sammanfogas värdena för indatakolumnerna till en vektor i den angivna ordningen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Datatyper**

- Indatatatyp: `array[string]` (kolumnnamn med numeriska värden/matrisvärden [numeriska värden])
- Utdatatyp: `Vector[double]`

**Definition**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
| -------- | ------------ | ----- | -------- | -------- |
| NA | Inga ytterligare parametrar krävs för den här transformatorn. | NA | NA | NA |

{style="table-layout:auto"}

**Exempel före omformning**

| id | timme | mobil | userFeatures | klickad |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1,0 | [0.0, 10.0, 0.5] | 1,0 |

{style="table-layout:auto"}

**Exempel efter omformning**

| id | timme | mobil | userFeatures | klickad | funktioner |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1,0 | [0.0, 10.0, 0.5] | 1,0 | [18.0, 1.0, 0.0, 10.0, 0.5] |

{style="table-layout:auto"}

### Numeriska omformningar {#numeric-transformations}

Läs det här avsnittet om du vill veta mer om de tillgängliga transformatorerna för bearbetning och skalning av numeriska data. Dessa transformatorer behövs för att hantera och optimera numeriska funktioner i datauppsättningarna.

#### Binarizer {#binarizer}

Transformeraren `Binarizer` konverterar numeriska funktioner till binära (0/1) funktioner via en process som kallas binarisering. Funktionsvärden som är större än det angivna tröskelvärdet konverteras till 1,0, medan värden som är lika med eller mindre än tröskelvärdet konverteras till 0,0. `Binarizer` stöder både `Vector`- och `Double`-typer för indatakolumnen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**Datatyper**

- Indatatyp: Numerisk kolumn
- Datatyp för utdata: Numerisk

**Definition**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | Param för tröskelvärdet som används för att binära kontinuerliga funktioner. Funktioner som är större än tröskelvärdet är binära till 1,0, medan funktioner som är lika med eller mindre än tröskelvärdet är binära till 0,0. | int/double | 0,0 | valfri |

{style="table-layout:auto"}

**Exempel på indata före binarisering**

| id | värdering |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**Exempelutdata efter binarisering (standardtröskelvärde 0,0)**

| id | värdering |
|---|---------|
| 0 | 0,0 |
| 1 | 1,0 |
| 2 | 1,0 |

**Definition med anpassat tröskelvärde**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**Exempelutdata efter binarisering (med tröskelvärdet 14.0)**

| id | age |
|---|-------|
| 0 | 0,0 |
| 1 | 0,0 |
| 2 | 1,0 |

#### Bucketizer {#bucketizer}

Transformeraren `Bucketizer` konverterar en kolumn med kontinuerliga funktioner till en kolumn med funktionsintervall, baserat på användardefinierade tröskelvärden. Den här processen är användbar när du vill segmentera kontinuerliga data i diskreta behållare eller fickor. `Bucketizer` kräver en `splits`-parameter som definierar gränserna för bucketerna.

**Datatyper**

- Indatatyp: Numerisk kolumn
- Datatyp för utdata: Numeriska (bundna värden)

**Definition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | En parameter för att mappa kontinuerliga funktioner till grupper. Med `n+1` delningar finns det `n` bucket. Delningar måste vara i strikt ökande ordning och intervallet (x,y) används för varje hink utom den sista, som inkluderar y. | array(double) | N/A | valfri |

{style="table-layout:auto"}

**Exempel på delningar**

- Array(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Array(0.0, 1.0, 2.0)

Delningar ska omfatta hela intervallet med dubbla värden. Annars behandlas värden utanför de angivna delningarna som fel.

**Exempelomformning**

Det här exemplet tar en kolumn med kontinuerliga funktioner (`course_duration`), binder den enligt `splits` och sätter sedan ihop de resulterande bucklarna med andra funktioner.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

Transformatorn `MinMaxScaler` skalar om varje funktion i en vektorraduppsättning till ett angivet intervall, vanligtvis [0, 1]. Detta garanterar att alla funktioner bidrar lika mycket till modellen. Det är särskilt användbart för modeller som är känsliga för funktionsskalning, till exempel övertoningsbaserade algoritmer. `MinMaxScaler` arbetar med följande parametrar:

- **min**: Omvandlingens nedre gräns, som delas av alla funktioner. Standardvärdet är `0.0`.
- **max**: Omvandlingens övre gräns, som delas av alla funktioner. Standardvärdet är `1.0`.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**Datatyper**

- Indatatyp: `Array[Double]`
- Utdatatyp: `Array[Double]`

**Definition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | Lägre gräns efter omvandling, delas av alla funktioner. | double | 0,0 | valfri |
| `max` | Övre gräns efter omvandling, delad med alla funktioner. | double | 1,0 | valfri |

**Exempelomformning**

I det här exemplet omformas en uppsättning funktioner och de skalas om till det angivna intervallet med MinMaxScaler efter att flera andra omformningar har använts.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

Transformatorn `MaxAbsScaler` skalar om varje funktion i en vektorraduppsättning till intervallet [-1, 1] genom att dividera med det maximala absoluta värdet för varje funktion. Den här omformningen är idealisk för att bevara glans i datauppsättningar med både positiva och negativa värden, eftersom data inte flyttas eller centreras. Detta gör `MaxAbsScaler` särskilt lämplig för modeller som är känsliga för skalan av indatafunktioner, t.ex. sådana som innefattar distansberäkningar.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**Datatyper**

- Indatatyp: `Array[Double]`
- Utdatatyp: `Array[Double]`

**Definition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| NA | MaxAbsScaler kräver inga ytterligare parametrar för åtgärden. | NA | NA | NA |

**Exempelomformning**

I det här exemplet används flera omformningar, inklusive `MaxAbsScaler`, för att skala om funktioner till intervallet [-1, 1].

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normaliserare {#normalizer}

`Normalizer` är en transformator som normaliserar varje vektor i en vektorraduppsättning så att den har en enhetsnorm. Denna process garanterar en konsekvent skala utan att vektorernas riktning ändras. Den här omvandlingen är särskilt användbar i maskininlärningsmodeller som bygger på avståndsmått eller andra vektorbaserade beräkningar, särskilt när vektorernas storlek varierar avsevärt.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**Datatyper**

- Indatatyp: `array[double]` / `vector[double]`
- Utdatatyp: `vector[double]`

**Definition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | Anger `p-norm` som används för normalisering (till exempel `1-norm`, `2-norm`). | heltal | 2 | valfri |

**Exempelomformning**

I det här exemplet visas hur du använder flera omformningar, inklusive `Normalizer`, för att normalisera en uppsättning funktioner med den angivna `p-norm`.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

`QuantileDiscretizer` är en transformator som konverterar en kolumn med kontinuerliga funktioner till binda kategorisiska funktioner, med det antal behållare som bestäms av parametern `numBuckets`. I vissa fall kan det faktiska antalet bucklar vara mindre än det angivna antalet om det finns för få distinkta värden för att skapa tillräckligt många kvantiteter.

Den här omvandlingen är särskilt användbar när du vill förenkla representationen av kontinuerliga data eller förbereda dem för algoritmer som fungerar bättre med kategoriserade indata.

**Datatyper**

- Indatatyp: Numerisk kolumn
- Datatyp för utdata: Numerisk kolumn (kategorisisk)

**Definition**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | Det antal grupper (kvantiteter eller kategorier) som datapunkter grupperas i. Talet måste vara större än eller lika med två. | heltal | 2 | valfri |

**Exempelomformning**

I det här exemplet visas hur `QuantileDiscretizer` binder en kolumn med kontinuerliga funktioner (`hour`) till tre kategorier.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Exempel före och efter diskretisering**

| id | timme | resultat |
|---|------|--------|
| 0 | 18,0 | 2,0 |
| 1 | 19,0 | 2,0 |
| 2 | 8,0 | 1,0 |
| 3 | 5,0 | 1,0 |
| 4 | 2,2 | 0,0 |

#### StandardScaler {#standardscaler}

`StandardScaler` är en transformator som normaliserar varje funktion i en vektorraduppsättning så att den har en enhetsstandardavvikelse och/eller nollmedelvärde. Den här processen gör data mer lämpliga för algoritmer som antar att funktioner centreras runt noll med en konsekvent skala. Omvandlingen är särskilt viktig för maskininlärningsmodeller som SVM, logistisk regression och neurala nätverk, där icke standardiserade data kan leda till konvergensproblem eller minskad precision.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**Datatyper**

- Indatatyp: Vector
- Datatyp för utdata: Vektor

**Definition**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | Skalar data så att de har enhetsstandardavvikelse. | boolesk | True | valfri |
| `withMean` | Centrerar data med medelvärdet före skalning. Det här alternativet ger täta utdata, så använd försiktighet med sparse-indata. | boolesk | Falskt | valfri |

**Exempelomformning**

I det här exemplet visas hur du använder StandardScaler på en uppsättning funktioner och normaliserar dem med enhetsstandardavvikelse och nollmedelvärde.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Kategoriserade omformningar {#categorical-transformations}

I det här avsnittet finns en översikt över de tillgängliga transformatorerna för att konvertera och förbearbeta kategoriserade data för maskininlärningsmodeller. Dessa omformningar är utformade för datapunkter som representerar distinkta kategorier eller etiketter, i stället för numeriska värden.

#### StringIndexer {#stringindexer}

`StringIndexer` är en transformator som kodar en strängkolumn med etiketter till en kolumn med numeriska index. Indexvärdena ligger mellan 0 och `numLabels` och sorteras efter etikettfrekvens (den vanligaste etiketten får indexvärdet 0). Om indatakolumnen är numerisk byts den till en sträng före indexering. Osynliga etiketter kan tilldelas indexet `numLabels` om det anges av användaren.

Den här omvandlingen är särskilt användbar när du vill konvertera kategoriserade strängdata till numeriska format, vilket gör den lämplig för maskininlärningsmodeller som kräver numeriska indata.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**Datatyper**

- Indatatyp: String
- Datatyp för utdata: Numerisk

**Definition**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------|-------------|------|---------|----------|
| NA | `StringIndexer` kräver inga ytterligare parametrar för åtgärden. | NA | NA | NA |

**Exempelomformning**

I det här exemplet visas hur du använder `StringIndexer` på en kategorisisk funktion och konverterar den till ett numeriskt index.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

`OneHotEncoder` är en transformator som konverterar en kolumn med etikettindex till en kolumn med null-optimerade binära vektorer, där varje vektor har högst ett enda värde. Den här kodningen är särskilt användbar för att tillåta att algoritmer som kräver numeriska indata, t.ex. Logistisk regression, kan införliva kategoriserade data effektivt.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**Datatyper**

- Indatatyp: Numerisk
- Datatyp för utdata: Vector[Int]

**Definition**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------|-------------|------|---------|----------|
| NA | OneHotEncoder kräver inga ytterligare parametrar för åtgärden. | NA | NA | NA |

**Exempelomformning**

I det här exemplet visas hur du först tillämpar `StringIndexer` på en kategoriseringsfunktion och sedan använder `OneHotEncoder` för att konvertera indexerade värden till en binär vektor.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Textuella omvandlingar {#textual-transformations}

I det här avsnittet finns information om de omvandlare som är tillgängliga för bearbetning och konvertering av textdata till format som kan användas i maskininlärningsmodeller. Detta avsnitt är mycket viktigt för utvecklare som arbetar med naturliga språkdata och textanalys.

#### CountVectorizer {#countvectorizer}

`CountVectorizer` är en transformator som konverterar en samling textdokument till vektorer för tokenantal, vilket skapar glesare representationer baserat på det vokabulär som extraherats från corpus. Den här omvandlingen är väsentlig för att konvertera textdata till ett numeriskt format som kan användas av maskininlärningsalgoritmer, som LDA (Latent Dirichlet Allocation), genom att representera frekvensen av tokens i varje dokument.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Datatyper**

- Indatatyp: Array[String]
- Datatyp för utdata: Tät vektor

**Definition**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Maximal storlek på språket. CountVectorizer skapar en ordbok som bara tar hänsyn till de `vocabSize` mest använda termerna som ordnas efter termfrekvens i korpus. | Int | 218 | valfri |
| `MIN_DOC_FREQ` | Anger det minsta antal olika dokument som en term måste finnas i för att inkluderas i ordlistan. Kan vara ett absolut tal eller en bråkdel av dokument (om det är en dubbel). | Dubbel | 1,0 | valfri |
| `MAX_DOC_FREQ` | Anger det maximala antalet olika dokument som en term kan finnas i för att inkluderas i ordlistan. Kan vara ett absolut tal eller en bråkdel av dokument (om det är en dubbel). | Dubbel | (263)-1 | valfri |
| `MIN_TERM_FREQ` | Filtrerar ut sällsynta ord i ett dokument. Termer med frekvens/antal som är mindre än det angivna tröskelvärdet ignoreras. Kan vara ett absolut tal eller en bråkdel av dokumentets tokenantal. | Dubbel | 1,0 | valfri |

{style="table-layout:auto"}

**Exempelomformning**

I det här exemplet visas hur CountVectorizer konverterar en samling med textarrayer till vektorer med tokenantal, vilket ger en glesare representation.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Exempel före och efter vektorisering**

| id | texter | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;) | (3,[0,1,2],[1.0,1.0,1.0]) |
| 1 | Array(&quot;a&quot;, &quot;b&quot;, &quot;b&quot;, &quot;c&quot;, &quot;a&quot;) | (3,[0,1,2],[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

`NGram` är en transformator som genererar en sekvens av n-gram, där n-gram är en sekvens av (??) tokens (vanligtvis ord) för ett heltal (`𝑛`). Utdata består av blankstegsavgränsade strängar av &#39;?&#39; på varandra följande ord, som kan användas som funktioner i maskininlärningsmodeller, särskilt sådana som är inriktade på bearbetning av naturligt språk.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Datatyper**

- Indatatyp: Array[String]
- Datatyp för utdata: Array[String]

**Definition**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | Den minsta n-gramlängden måste vara större än eller lika med 1. | heltal | 2 (funktioner i gram) | valfri |

{style="table-layout:auto"}

**Exempelomformning**

I det här exemplet visas hur NGram-transformatorn skapar en sekvens på 3 gram från en lista med tokens som härletts från textdata.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Exempel före och efter n-gram-omvandling**

| id | texter | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;this&quot;, &quot;was&quot;, &quot;an&quot;, &quot;entertaining&quot;, &quot;movie&quot;] | [&quot;this was an&quot;, &quot;was an underhållande&quot;, &quot;an underhållande movie&quot; ] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

`StopWordsRemover` är en transformator som tar bort stoppord från en strängsekvens och filtrerar bort vanliga ord som inte har någon väsentlig betydelse. Den tar en sekvens med strängar som indata (till exempel utdata från en tokeniserare) och tar bort alla stoppord som anges av parametern `stopWords`.

Den här omvandlingen är användbar för förbearbetning av textdata, vilket förbättrar effektiviteten i maskininlärningsmodeller längre fram i kedjan genom att eliminera ord som inte bidrar mycket till den övergripande innebörden.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Datatyper**

- Indatatyp: Array[String]
- Datatyp för utdata: Array[String]

**Definition**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | Orden som ska filtreras bort. | matris [sträng] | Standard: engelska stoppord | valfri |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**Exempelomformning**

I det här exemplet visas hur `StopWordsRemover` filtrerar bort vanliga engelska stoppord från en lista med tokens.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Exempel på borttagning av stoppord före och efter**

| id | råformat | filtrerad |
|----|------------------------------|--------------------------|
| 0 | [Jag, såg,,, röd, ballong] | [såg, röd, ballong] |
| 1 | [Mary, hade, ett litet lamm] | [Mary, liten, lamm] |

**Exempel med egna stoppord**

I det här exemplet visas hur du använder en anpassad lista med stoppord för att filtrera bort specifika ord från indatasekvenserna.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Exempel på borttagning av egna stoppord före och efter**

| id | råformat | filtrerad |
|----|------------------------------|--------------------------|
| 0 | [Jag, såg,,, röd, ballong] | [såg,,, ballong] |
| 1 | [Mary, hade, ett litet lamm] | [Mary, en liten, lamm] |

#### TF-IDF {#tf-idf}

`TF-IDF` (frekvens för omvänd termsekvens) är en transformator som används för att mäta vikten av ett ord i ett dokument i förhållande till ett corpus. Termfrekvens (TF) avser det antal gånger en term \(t\) visas i ett dokument \(d\), medan dokumentfrekvens (DF) anger hur många dokument i korpus \(D\) som innehåller termen \(t\). Den här metoden används ofta vid textbrytning för att minska effekten av ofta förekommande ord, som&quot;a&quot;,&quot;the&quot; och&quot;of&quot;, som innehåller lite unik information.

Den här omvandlingen är särskilt värdefull när det gäller textbrytning och bearbetning av naturliga språk eftersom den tilldelar ett numeriskt värde till varje ords betydelse i ett dokument och i hela corpus.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**Datatyper**

- Indatatyp: Array[String]
- Datatyp för utdata: Vector[Int]

**Definition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | Antalet funktioner som ska genereras. Måste vara större än 0. | Int | 262144 | valfri |
| `MIN_DOC_FREQ` | Det minsta antal dokument i vilka en term måste framstå som inkluderad i modellen. | Int | 0 | valfri |

{style="table-layout:auto"}

**Exempelomformning**

I det här exemplet visas hur du använder TF-IDF för att omvandla tokeniserade meningar till en funktionsvektor som representerar vikten av varje term i sammanhanget för hela corpus.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenior {#tokenizer}

`Tokenizer` är en transformator som delar upp text, t.ex. en mening, i enskilda termer, vanligtvis ord. Den konverterar meningar till arrayer med variabler, vilket utgör ett grundläggande steg i textförbearbetningen som förbereder data för vidare textanalys eller modelleringsprocesser.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Datatyper**

- Indatatyp: Textmening
- Datatyp för utdata: Array[String]

**Definition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|-----------|-------------|------|---------|----------|
| NA | `Tokenizer` kräver inga ytterligare parametrar för åtgärden. | NA | NA | NA |

**Exempelomformning**

I det här exemplet visas hur `Tokenizer` delar upp meningar i enskilda ord (tokens) som en del av en textbearbetningsprocess.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

`Word2Vec` är en uppskattare som bearbetar ordsekvenser som representerar dokument och utbildar en `Word2VecModel`. Den här modellen mappar varje ord till en unik vektor med fast storlek och omvandlar varje dokument till en vektor genom att beräkna ett genomsnitt för vektorerna för alla ord i dokumentet. Det används ofta i naturliga språkbehandlingsåtgärder. `Word2Vec` skapar ordinbäddningar som fångar in semantisk betydelse, konverterar textdata till numeriska vektorer som representerar relationerna mellan ord och möjliggör effektivare textanalys och maskininlärningsmodeller.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**Datatyper**

- Indatatyp: Array[String]
- Datatyp för utdata: Vector[Double]

**Definition**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Parametrar**

| Parameter | Beskrivning | Typ | Standard | Valfritt |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | Dimensionen för den vektor som varje ord omformas till. | Heltal | 100 | valfri |
| `MIN_COUNT` | Det minsta antal gånger en token måste finnas med i `Word2Vec`-modellens vokabulär. | Heltal | 5 | valfri |

{style="table-layout:auto"}

**Exempelomformning**

I det här exemplet visas hur `Word2Vec` konverterar en tokeniserad granskning till en vektor med fast storlek som representerar medelvärdet för ordvektorerna i dokumentet.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Exempel före och efter Word2Vec-omformning**

| recension | tokeniserad | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| det här var en underhållande film | [this, was, an, underhållande, movie] | [-0.02571388928294182,0.00818799751577899,0.0092235435 731709,-0.01515385233797133,0.012175946310162545,3.112906 5901041035E-4,0.002514510504261252,0.00575701978523284 3,-0.021328244300093502,0.00933587718750069] |

{style="table-layout:auto"}
