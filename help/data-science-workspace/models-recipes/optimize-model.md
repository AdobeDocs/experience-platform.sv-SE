---
keywords: Experience Platform;optimera;modell;Data Science Workspace;populära ämnen;modellinsikter
solution: Experience Platform
title: Optimera en modell med Model Insights Framework
type: Tutorial
description: Model Insights Framework förser datavetenskaparen med verktyg i Data Science Workspace som gör snabba och välgrundade val för optimala maskininlärningsmodeller baserade på experiment.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Optimera en modell med Model Insights-ramverket

Model Insights Framework förser datavetenskaparen med verktyg i [!DNL Data Science Workspace] att göra snabba och välgrundade val för optimala maskininlärningsmodeller baserade på experiment. Ramverket kommer att förbättra snabbheten och effektiviteten i maskininlärningsarbetsflödet samt förbättra användarvänligheten för datavetare. Det gör du genom att ange en standardmall för varje maskininlärningsalgoritmtyp som ska vara till hjälp vid modelljustering. Slutresultatet gör att datavetare och datavetare kan fatta bättre modelloptimeringsbeslut för sina slutkunder.

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

Exempelkod för recept finns i [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) databas under `recipes`. Specifika filer från den här databasen kommer att refereras i den här självstudiekursen.

### Scala {#scala}

Det finns två sätt att hämta in mätvärden till recepten. Den ena är att använda standardmåtten för utvärdering som tillhandahålls av SDK och den andra är att skriva anpassade mått för utvärdering.

#### Standardmått för utvärdering av Scala

Standardutvärderingar beräknas som en del av klassificeringsalgoritmerna. Här är några standardvärden för utvärderare som för närvarande är implementerade:

| Utvärderarklass | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

Utvärderaren kan definieras i receptet i [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) i `recipe` mapp. Exempelkod som aktiverar `DefaultBinaryClassificationEvaluator` visas nedan:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

När en utvärderingsklass har aktiverats beräknas ett antal mätvärden under utbildning som standard. Standardvärden kan deklareras explicit genom att lägga till följande rad i `application.properties`.

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

I följande tabell anges standardmåtten för varje klass. En användare kan också använda värdena i `evaluation.metric` -kolumn för att aktivera ett specifikt mått.

| `evaluator.class` | Standardmått | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Återkalla <br>-Matrix för konfusion <br>-F-poäng <br>-Accuracy <br>-Mottagarens driftsegenskaper <br>-Område under mottagarens driftsegenskaper | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Återkalla <br>-Matrix för konfusion <br>-F-poäng <br>-Accuracy <br>-Mottagarens driftsegenskaper <br>-Område under mottagarens driftsegenskaper | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | - Genomsnittlig genomsnittlig precision (MAP) <br>-Normaliserat rabatterat kumulativt resultat <br>- Medelvärde för lutning <br>-Metrisk K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Anpassade utvärderingsmått för Scala

Den anpassade utvärderaren kan fås genom att utöka gränssnittet för `MLEvaluator.scala` i `Evaluator.scala` -fil. I exemplet [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) fil, vi definierar anpassad `split()` och `evaluate()` funktioner. Våra `split()` delar data slumpmässigt med förhållandet 8:2 och `evaluate()` funktionen definierar och returnerar 3 mått: MAPPA, MAE och RMSE.

>[!IMPORTANT]
>
>För `MLMetric` klass, använd inte `"measures"` for `valueType` när du skapar en ny `MLMetric` i annat fall fylls inte måttet i i tabellen för anpassade utvärderingsmått.
>  
> Gör så här: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Inte detta: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


När det är definierat i receptet är nästa steg att aktivera det i recepten. Detta görs i [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) fil i projektets `resources` mapp. Här är `evaluation.class` är inställt på `Evaluator` klass definierad i `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

I [!DNL Data Science Workspace], skulle användaren kunna se insikterna på fliken &quot;Evaluation Metrics&quot; på sidan med experiment.

### [!DNL Python/Tensorflow] {#pythontensorflow}

För närvarande finns det inga standardmått för utvärdering för [!DNL Python] eller [!DNL Tensorflow]. Så här hämtar du utvärderingsstatistik för [!DNL Python] eller [!DNL Tensorflow]måste du skapa ett anpassat utvärderingsmått. Detta kan du göra genom att implementera `Evaluator` klassen.

#### Anpassade utvärderingsvärden för [!DNL Python]

För anpassade utvärderingsvärden finns det två huvudmetoder som måste implementeras för utvärderaren: `split()` och `evaluate()`.

För [!DNL Python]skulle dessa metoder definieras i [utvärderare.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) för `Evaluator` klassen. Följ [utvärderare.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) länk för ett exempel på `Evaluator`.

Skapa utvärderingsmått i [!DNL Python] kräver att användaren implementerar `evaluate()` och `split()` metoder.

The `evaluate()` metoden returnerar metric-objektet som innehåller en array med metriska objekt med egenskaperna för `name`, `value`och `valueType`.

Syftet med `split()` metoden är att mata in data och att ta fram en utbildning och en testdatamängd. I vårt exempel `split()` metodindata med `DataSetReader` SDK och rensar sedan data genom att ta bort orelaterade kolumner. Därifrån skapas ytterligare funktioner från befintliga Raw-funktioner i data.

The `split()` ska returnera en utbildnings- och testdatabildruta som sedan används av `pipeline()` metoder för att träna och testa ML-modellen.

#### Anpassade utvärderingsmått för tensorflow

För [!DNL Tensorflow], liknar [!DNL Python], metoderna `evaluate()` och `split()` i `Evaluator` måste implementeras. För `evaluate()`, ska mätvärdena returneras medan `split()` returnerar tåget och provningsdata.

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

Från och med nu finns det inga standardmått för utvärdering för R. För att få fram mätvärdena för R måste du definiera `applicationEvaluator` som en del av receptet.

#### Anpassade bedömningsvärden för R

Huvudsyftet med `applicationEvaluator` är att returnera ett JSON-objekt som innehåller nyckelvärdepar med mätvärden.

Detta [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) kan användas som exempel. I det här exemplet `applicationEvaluator` är uppdelad i tre välkända avsnitt:
- Läs in data
- Datakivering/funktionsutveckling
- Hämta sparad modell och utvärdera

Data läses först in till en datauppsättning från en källa enligt definitionen i [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Därifrån rensas och konstrueras data för att passa maskininlärningsmodellen. Slutligen används modellen för att göra en förutsägelse med hjälp av vår datamängd, och med utgångspunkt i de förväntade värdena och de faktiska värdena beräknas mätvärdena. I det här fallet definieras MAPE, MAE och RMSE och returneras i `metrics` -objekt.

## Använda fördefinierade mätvärden och visualiseringsdiagram

The [!DNL Sensei Model Insights Framework] har stöd för en standardmall för varje typ av maskininlärningsalgoritm. Tabellen nedan visar vanliga maskininlärningsalgoritmklasser på hög nivå och motsvarande utvärderingsmått och visualiseringar.

| ML-algoritmtyp | Mätvärden för utvärdering | Visualiseringar |
| --- | --- | --- |
| Regression | - RMSE<br>- BILD<br>- MASE<br>- MAE | Förutsedd kontra faktisk värdesövertäckningskurva |
| Binär klassificering | - Konfusionsmatris<br>- Precision-återkallning<br>- Exakthet<br>- F-poäng (specifikt F1, F2)<br>- AUC<br>- ROC | ROC-kurva och förvirringsmatris |
| Klassificering i flera klasser | -Confusion matrix <br>- För varje klass: <br>- exakthet vid precisionsåterkallning <br>- F-poäng (specifikt F1, F2) | ROC-kurva och förvirringsmatris |
| Klustring (med jordsanning) | - NMI (normaliserat poängvärde för ömsesidig information), AMI (justerat poängvärde för<br>- RI (Rand-index), ARI (justerat Rand-index)<br>- homogenitetspoäng, fullständighetspoäng och V-mått<br>- FMI (Fowlkes-Mallows index)<br>- Renhet<br>- Jaccard-index | Kluster med kluster och centroider med relativa klusterstorlekar som återspeglar de datapunkter som ingår i klustret |
| Klustring (ej jordsanning) | - Tröghet<br>- Silhuettkoefficient<br>- CHI (index Calinski-Harabaz)<br>- DBI (Davies-Bouldin-index)<br>- Dunn-index | Kluster med kluster och centroider med relativa klusterstorlekar som återspeglar de datapunkter som ingår i klustret |
| Rekommendation | - Genomsnittlig genomsnittlig precision (MAP) <br>-Normaliserat rabatterat kumulativt resultat <br>- Medelvärde för lutning <br>-Metrisk K | TBD |
| Användningsexempel för TensorFlow | TensorFlow Model Analysis (TFMA) | Deepcompare neural network model comparison/visualization |
| Andra/felsökningsfunktioner | Anpassad metrisk logik (och motsvarande utvärderingskartor) som definieras av modellförfattaren. Fantastisk felhantering om mallen inte matchar | Tabell med nyckelvärdepar för mätvärden |
