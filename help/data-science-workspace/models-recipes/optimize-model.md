---
keywords: Experience Platform;optimera;modell;Data Science Workspace;populära ämnen;modellinsikter
solution: Experience Platform
title: Optimera en modell med Model Insights Framework
topic: tutorial
type: Tutorial
description: Model Insights Framework förser datavetenskaparen med verktyg i Data Science Workspace som gör snabba och välgrundade val för optimala maskininlärningsmodeller baserade på experiment.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# Optimera en modell med Model Insights-ramverket

Model Insights Framework ger datavetenskaparen verktyg i [!DNL Data Science Workspace] för att göra snabba och välgrundade val för optimala maskininlärningsmodeller baserade på experiment. Ramverket kommer att förbättra snabbheten och effektiviteten i maskininlärningsarbetsflödet samt förbättra användarvänligheten för datavetare. Det gör du genom att ange en standardmall för varje maskininlärningsalgoritmtyp som ska vara till hjälp vid modelljustering. Slutresultatet gör att datavetare och datavetare kan fatta bättre modelloptimeringsbeslut för sina slutkunder.

## Vad är mätvärden?

Efter att ha implementerat och utbildat en modell är nästa steg som en datavetare skulle göra att hitta hur bra modellen kommer att fungera. Olika mätvärden används för att hitta hur effektiv en modell är jämfört med andra. Några exempel på mätvärden är:
- Klassificeringsnoggrannhet
- Område under kurva
- Sammanställningsmatris
- Klassificeringsrapport

## Konfigurera receptkod

Model Insights Framework har för närvarande stöd för följande körningsmiljöer:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

Exempelkod för recept finns i [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference)-databasen under `recipes`. Specifika filer från den här databasen kommer att refereras i den här självstudiekursen.

### Scala {#scala}

Det finns två sätt att hämta in mätvärden till recepten. Den ena är att använda standardmåtten för utvärdering som tillhandahålls av SDK och den andra är att skriva anpassade mått för utvärdering.

#### Standardmått för utvärdering av Scala

Standardutvärderingar beräknas som en del av klassificeringsalgoritmerna. Här är några standardvärden för utvärderare som för närvarande är implementerade:

| Utvärderarklass | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

Utvärderaren kan definieras i receptet i filen [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) i mappen `recipe`. Exempelkod som aktiverar `DefaultBinaryClassificationEvaluator` visas nedan:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

När en utvärderingsklass har aktiverats beräknas ett antal värden som standard under kursen. Standardvärden kan deklareras explicit genom att lägga till följande rad i `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Om måttet inte är definierat aktiveras standardmåtten.

Du kan aktivera ett specifikt mått genom att ändra värdet för `evaluation.metrics.com`. I följande exempel är F-poängmåttet aktiverat.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

I följande tabell anges standardmåtten för varje klass. En användare kan också använda värdena i kolumnen `evaluation.metric` för att aktivera ett specifikt mått.

| `evaluator.class` | Standardmått | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Properties <br>-Area under the Receiver Operating Characproperties | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Properties <br>-Area under the Receiver Operating Characproperties | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Medelvärde för genomsnittlig precision (MAP) <br>-Normaliserad rabatterad kumulativ vinst <br>-Medelvärde för lutning <br>-Mätvärde K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Anpassade utvärderingsmått för Scala

Den anpassade utvärderaren kan fås genom att utöka gränssnittet för `MLEvaluator.scala` i din `Evaluator.scala`-fil. I exemplet [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala)-fil definierar vi anpassade `split()`- och `evaluate()`-funktioner. Vår `split()`-funktion delar upp våra data slumpmässigt med förhållandet 8:2 och vår `evaluate()`-funktion definierar och returnerar 3 mätvärden: MAPPA, MAE och RMSE.

>[!IMPORTANT]
>
>Använd inte `"measures"` för `valueType` när du skapar en ny `MLMetric` för klassen `MLMetric`, annars fylls inte måttet i i tabellen för anpassade utvärderingsmått.
>  
> Gör så här: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Inte detta: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


När det är definierat i receptet är nästa steg att aktivera det i recepten. Detta görs i filen [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) i projektets `resources`-mapp. Här är `evaluation.class` inställt på klassen `Evaluator` som definieras i `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

I [!DNL Data Science Workspace] kan användaren se insikterna på fliken &quot;Evaluation Metrics&quot; på sidan för experiment.

### [!DNL Python/Tensorflow] {#pythontensorflow}

För närvarande finns det inga standardmått för utvärdering för [!DNL Python] eller [!DNL Tensorflow]. Om du vill hämta utvärderingsmåtten för [!DNL Python] eller [!DNL Tensorflow] måste du skapa ett anpassat utvärderingsmått. Detta kan du göra genom att implementera klassen `Evaluator`.

#### Anpassade utvärderingsmått för [!DNL Python]

För anpassade utvärderingsvärden finns det två huvudmetoder som måste implementeras för utvärderaren: `split()` och `evaluate()`.

För [!DNL Python] skulle dessa metoder definieras i [utvärderator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) för klassen `Evaluator`. Följ länken [utvärderator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) för ett exempel på `Evaluator`.

Om du skapar utvärderingsmått i [!DNL Python] måste användaren implementera metoderna `evaluate()` och `split()`.

Metoden `evaluate()` returnerar det metriska objektet som innehåller en array med metriska objekt med egenskaperna `name`, `value` och `valueType`.

Syftet med metoden `split()` är att mata in data och att ta fram en utbildning och en testdatamängd. I vårt exempel matar metoden `split()` in data med hjälp av SDK:n `DataSetReader` och rensar sedan data genom att ta bort icke-relaterade kolumner. Därifrån skapas ytterligare funktioner från befintliga Raw-funktioner i data.

Metoden `split()` bör returnera en utbildnings- och testdatabildruta som sedan används av metoderna `pipeline()` för att träna och testa ML-modellen.

#### Anpassade utvärderingsmått för tensorflow

För [!DNL Tensorflow], liknande [!DNL Python], måste metoderna `evaluate()` och `split()` i klassen `Evaluator` implementeras. För `evaluate()` ska mätvärdena returneras medan `split()` returnerar tåget och testdata.

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

Från och med nu finns det inga standardmått för utvärdering för R. Om du vill hämta utvärderingsmåtten för R måste du definiera klassen `applicationEvaluator` som en del av receptet.

#### Anpassade bedömningsvärden för R

Huvudsyftet med `applicationEvaluator` är att returnera ett JSON-objekt som innehåller nyckelvärdepar med mätvärden.

Denna [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) kan användas som exempel. I det här exemplet delas `applicationEvaluator` upp i tre välkända avsnitt:
- Läs in data
- Datakivering/funktionsutveckling
- Hämta sparad modell och utvärdera

Data läses först in till en datauppsättning från en källa enligt definitionen i [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Därifrån rensas och konstrueras data för att passa maskininlärningsmodellen. Slutligen används modellen för att göra en förutsägelse med hjälp av vår datamängd och med utgångspunkt från de förväntade värdena och faktiska värdena beräknas mätvärdena. I det här fallet definieras MAPE, MAE och RMSE och returneras i `metrics`-objektet.

## Använda fördefinierade mätvärden och visualiseringsdiagram

[!DNL Sensei Model Insights Framework] stöder en standardmall för varje typ av maskininlärningsalgoritm. Tabellen nedan visar vanliga maskininlärningsalgoritmklasser på hög nivå och motsvarande utvärderingsmått och visualiseringar.

| ML-algoritmtyp | Mätvärden för utvärdering | Visualiseringar |
--- | --- | ---
| Regression | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Förutsedd kontra faktisk värdesövertäckningskurva |
| Binär klassificering | - Konfusionsmatris<br>- Precision-revansch<br>- Accuracy<br>- F-score (specifikt F1,F2)<br>- AUC<br>- ROC | ROC-kurva och förvirringsmatris |
| Klassificering i flera klasser | -Konfusionsmatris <br>- För varje klass: <br>- precision-/återkallelseprecision <br>- F-poäng (specifikt F1, F2) | ROC-kurva och förvirringsmatris |
| Klustring (med jordsanning) | - NMI (normaliserat ömsesidigt informationsresultat), AMI (justerat ömsesidigt informationsresultat)<br>- RI (Rand index), ARI (justerat Rand-index)<br> - homogenitetspoäng, fullständighetsresultat och V- measure<br>- FMI (Fowlkes-Mallows index)<br>- Renhet<br> - Jaccard index | Kluster med kluster och centroider med relativa klusterstorlekar som återspeglar de datapunkter som ingår i klustret |
| Klustring (ej jordsanning) | - Inertia<br>- Silhouette-koefficient<br>- CHI (Calinski-Harabaz index)<br>- DBI (Davies-Bouldin index)<br>- Dunn index | Kluster med kluster och centroider med relativa klusterstorlekar som återspeglar de datapunkter som ingår i klustret |
| Rekommendation | -Medelvärde för genomsnittlig precision (MAP) <br>-Normaliserad rabatterad kumulativ vinst <br>-Medelvärde för lutning <br>-Mätvärde K | TBD |
| Användningsexempel för TensorFlow | TensorFlow Model Analysis (TFMA) | Deepcompare neural network model comparison/visualization |
| Andra/felsökningsfunktioner | Anpassad metrisk logik (och motsvarande utvärderingskartor) som definieras av modellförfattaren. Fantastisk felhantering om mallen inte matchar | Tabell med nyckelvärdepar för mätvärden |
