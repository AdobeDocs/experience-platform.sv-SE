---
title: Klusteralgoritmer
description: Lär dig hur du konfigurerar och optimerar olika klusteralgoritmer med hjälp av nyckelparametrar, beskrivningar och exempelkod för att implementera avancerade statistiska modeller.
role: Developer
source-git-commit: 4d4e9ae527deb149f02edb39716851e995c23d21
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---

# Klusteralgoritmer {#clustering-algorithms}

Klusteralgoritmer grupperar datapunkter i distinkta kluster baserat på deras likheter, vilket gör det möjligt för oövervakad inlärning att identifiera mönster i data. Om du vill skapa en klustringsalgoritm använder du parametern `type` i `OPTIONS` -satsen för att ange den algoritm som du vill använda för modellutbildning. Därefter definierar du de relevanta parametrarna som nyckelvärdepar för att finjustera modellen.

>[!NOTE]
>
>Kontrollera att du förstår parameterkraven för den valda algoritmen. Vissa parametrar kan vara positionerade och kräver att alla föregående parametrar anges om anpassade värden anges. Om du väljer att inte anpassa vissa parametrar används standardinställningarna. Läs den relevanta dokumentationen för att förstå de olika parametrarnas funktion och standardvärden.

## [!DNL K-Means] {#kmeans}

`K-Means` är en klusteralgoritm som partitionerar datapunkter till ett fördefinierat antal kluster (k). Det är en av de vanligaste algoritmerna för klustring på grund av dess enkelhet och effektivitet.

**Parametrar**

När du använder `K-Means` kan följande parametrar anges i `OPTIONS` -satsen:

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITERATIONS` | Antalet iterationer som algoritmen ska köras. | `20` | (>= 0) |
| `TOL` | Konvergenstoleransnivån. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | Antalet kluster som ska skapas (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | Den algoritm som används för att beräkna avståndet mellan två punkter. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | Initieringsalgoritmen för klustercentren. | `k-means` | `random`, `k-means` |
| `INIT_STEPS` | Antalet steg för initieringsläget `k-means`. | `2` | (>0) |
| `PREDICTION_COL` | Namnet på den kolumn där förutsägelser ska lagras. | `prediction` | Valfri sträng |
| `SEED` | Ett slumpmässigt utsäde för reproducerbarhet. | `-1689246527` | Valfritt 64-bitars tal |
| `WEIGHT_COL` | Namnet på den kolumn som används för instansvikter. Om inget anges vägs alla instanser lika. | `not set` | N/A |

{style="table-layout:auto"}

**Exempel**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means] är en hierarkisk klusteralgoritm som använder en delande (eller&quot;top-down&quot;) metod. Alla observationer börjar i ett enda kluster och delas rekursivt allt eftersom hierarkin byggs. [!DNL Bisecting K-means] kan ofta vara snabbare än vanliga K-means, men ger vanligtvis olika klusterresultat.

**Parametrar**

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | Maximalt antal iterationer som algoritmen körs. | 20 | (>= 0) |
| `WEIGHT_COL` | Kolumnnamnet för instansvikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN | Valfri sträng |
| `NUM_CLUSTERS` | Önskat antal bladkluster. Det faktiska talet kan vara mindre om inga delbara kluster finns kvar. | 4 | (> 1) |
| `SEED` | Det slumpmässiga startvärde som används för att styra slumpmässiga processer i algoritmen. | INTE ANGIVEN | Valfritt 64-bitars tal |
| `DISTANCE_MEASURE` | Avståndsmåttet som används för att beräkna likheter mellan punkter. | &quot;euclidean&quot; | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | Det minsta antalet punkter (om >= 1.0) eller den minsta andelen punkter (om &lt; 1.0) som krävs för att ett kluster ska kunna delas upp. | 1,0 | (>= 0) |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |

{style="table-layout:auto"}

**Exempel**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] representerar en sammansatt fördelning där datapunkter hämtas från en av k Gaussisk delfördelningar, där var och en har sin egen sannolikhet. Den används för att modellera datauppsättningar som antas genereras från en blandning av flera Gaussisk-fördelningar.

**Parametrar**

| Parameter | Beskrivning | Standardvärde | Möjliga värden |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Maximalt antal iterationer som algoritmen ska köras. | 100 | (>= 0) |
| `WEIGHT_COL` | Kolumnnamnet, till exempel, vikter. Om den inte anges eller är tom behandlas alla instansvikter som `1.0`. | INTE ANGIVEN | Valfri sträng |
| `NUM_CLUSTERS` | Antalet oberoende Gaussisk-fördelningar i blandningsmodellen. | 2 | (> 1) |
| `SEED` | Det slumpmässiga startvärde som används för att styra slumpmässiga processer i algoritmen. | INTE ANGIVEN | Valfritt 64-bitars tal |
| `AGGREGATION_DEPTH` | Det djup som används för aggregering under beräkning. | 2 | (>= 1) |
| `PROBABILITY_COL` | Kolumnnamnet för villkorliga klasssannolikheter. Dessa bör behandlas som konfidensgrader i stället för som exakta sannolikheter. | &quot;sannolikhet&quot; | Valfri sträng |
| `TOL` | Konvergenstoleransen för iterativa algoritmer. | 0,01 | (>= 0) |
| `PREDICTION_COL` | Kolumnnamnet för förutsägelseutdata. | &quot;förutsägelse&quot; | Valfri sträng |

{style="table-layout:auto"}

**Exempel**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) är en sannolikhetsmodell som hämtar den underliggande ämnesstrukturen från en dokumentsamling. Det är en hierarkisk bayesisk modell på tre nivåer med ord-, ämne- och dokumentlager. LDA använder dessa lager tillsammans med de observerade dokumenten för att skapa en latent ämnesstruktur.

**Parametrar**

| Parameter | Beskrivning | Standardvärde | Möjliga värden |                                                                                                                                                                  | Standardvärde | Möjliga värden |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Maximalt antal iterationer som algoritmen körs. | 20 | (>= 0) |
| `OPTIMIZER` | Optimeraren eller härledningsalgoritmen som används för att beräkna LDA-modellen. De alternativ som stöds är `"online"` (Online Variational Bayes) och `"em"` (Expectation-Maximization). | online | `online`, `em` |
| `NUM_CLUSTERS` | Antalet kluster som ska skapas (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Anger hur ofta cachelagrade nod-ID:n ska kontrolleras. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | Koncentrationsparameter (&quot;alfa&quot;) för föregående placering på dokumentets distributioner över ämnen. Kontrollerar regularisering (utjämning). | Automatisk | Ett enda värde eller en vektor med längden k |
| `KEEP_LAST_CHECKPOINT` | Anger om den sista kontrollpunkten ska behållas när optimeraren för `em` används. | `true` | `true`, `false` |
| `LEARNING_DECAY` | Inlärningsfrekvens för optimeraren `online`, angiven som en exponentiell minskningsgrad mellan `(0.5, 1.0]`. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | En inlärningsparameter för optimeraren `online` som minskar vikten av tidiga iterationer så att antalet tidiga iterationer minskar. | 1024 | (> 0) |
| `SEED` | Slumpmässigt startvärde för styrning av slumpmässiga processer i algoritmen. | INTE ANGIVEN | Valfritt 64-bitars tal |
| `OPTIMIZE_DOC_CONCENTRATION` | För optimeraren `online`: Anger om `docConcentration` (Dirichlet-parametern för dokumentämnesdistribution) ska optimeras under utbildning. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | För optimeraren för `online`: den del av korpus som provats och som används i varje iteration av övertoningsdescent för minibatteri, i intervallet `(0, 1]`. | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | Koncentrationsparameter (&quot;beta&quot; eller&quot;eta&quot;) för tidigare versioner av ämnesdistributioner över villkor. | Automatisk | (>= 0) |
| `TOPIC_DISTRIBUTION_COL` | Utdatakolumn med uppskattningar av ämnesblandningsfördelningen för varje dokument. | INTE ANGIVEN | Valfri sträng |

**Exempel**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Nästa steg

När du har läst det här dokumentet vet du nu hur du konfigurerar och använder olika klusteralgoritmer. Läs sedan dokumenten om [klassificering](./classification.md) och [regression](./regression.md) om du vill veta mer om andra typer av avancerade statistiska modeller.
