---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics;testing
solution: Experience Platform
title: Utvecklarhandbok för SDK
topic: Overview
description: Med hjälp av SDK för modellredigering kan du utveckla anpassade maskininlärningsrecept och funktionsprofiler som kan användas i Adobe Experience Platform Data Science Workspace, med implementerbara mallar i PySpark och Spark (Scala).
translation-type: tm+mt
source-git-commit: 2a528c705a7aa610f57047be39be1ce9886ce44c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---


# Utvecklarhandbok för SDK

Med SDK för modellredigering kan du utveckla anpassade maskininlärningsrecept och funktionsförbereds som kan användas i arbetsytan för [!DNL Adobe Experience Platform] datavetenskap, med implementerbara mallar i [!DNL PySpark] och [!DNL Spark (Scala)].

Det här dokumentet innehåller information om de olika klasser som finns i SDK för modellredigering.

## DataLoader {#dataloader}

Klassen DataLoader kapslar in allt som rör hämtning, filtrering och returnering av rådata. Exempel på indata är sådana som används för utbildning, poängsättning eller funktionsteknik. Datainläsare utökar den abstrakta klassen `DataLoader` och måste åsidosätta den abstrakta metoden `load`.

**PySpark**

I följande tabell beskrivs de abstrakta metoderna för en PySpark Data Loader-klass:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>Läsa in och returnera plattformsdata som en Pandas DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Mappning av konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">spark</code>: Spark-session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

I följande tabell beskrivs de abstrakta metoderna för en [!DNL Spark] Data Loader-klass:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>Läs in och returnera plattformsdata som en DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Mappning av konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Läsa in data från en [!DNL Platform] datauppsättning {#load-data-from-a-platform-dataset}

Följande exempel hämtar [!DNL Platform] data efter ID och returnerar en DataFrame, där datauppsättnings-ID (`datasetId`) är en definierad egenskap i konfigurationsfilen.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

        query_options = get_query_options(spark.sparkContext)

        pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
            .option(query_options.datasetId(), dataset_id) \
            .load()
        pd.show()

        # return as DataFrame
        return pd
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## DataSaver {#datasaver}

Klassen DataSaver kapslar in allt som rör lagring av utdata, inklusive data från poängsättning eller funktionsteknik. Datasparare utökar den abstrakta klassen `DataSaver` och måste åsidosätta den abstrakta metoden `save`.

**PySpark**

I följande tabell beskrivs de abstrakta metoderna för en [!DNL PySpark] Data Saver-klass:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>Ta emot utdata som en DataFrame och lagra dem i en plattformsdatauppsättning</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Mappning av konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">dataframe</code>: Data som ska lagras i form av en DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

I följande tabell beskrivs de abstrakta metoderna för en [!DNL Spark] Data Saver-klass:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>Ta emot utdata som en DataFrame och lagra dem i en plattformsdatauppsättning</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Mappning av konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">dataFrame</code>: Data som ska lagras i form av en DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Spara data i en [!DNL Platform] datauppsättning {#save-data-to-a-platform-dataset}

För att kunna lagra data i en [!DNL Platform] datauppsättning måste egenskaperna antingen anges eller definieras i konfigurationsfilen:

- Ett giltigt [!DNL Platform] datauppsättnings-ID som data ska lagras på
- Klient-ID som tillhör din organisation

I följande exempel lagras data (`prediction`) i en [!DNL Platform] datauppsättning där datauppsättnings-ID (`datasetId`) och klient-ID (`tenantId`) definieras i konfigurationsfilen.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## DatasetTransformer {#datasettransformer}

Klassen DatasetTransformer ändrar och omformar strukturen i en datauppsättning. Komponenten behöver [!DNL Sensei Machine Learning Runtime] inte definieras och implementeras utifrån dina krav.

När det gäller en funktionspipeline kan datauppsättningsomvandlare användas tillsammans med en rörledningsfabrik för att förbereda data för funktionskonstruktion.

**PySpark**

I följande tabell beskrivs klassmetoderna för en PySpark-datamängdstransformeringsklass:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>Tar en datauppsättning som indata och skapar en ny härledd datauppsättning</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Mappning av konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">dataset</code>: Indatauppsättningen för omvandling</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

I följande tabell beskrivs de abstrakta metoderna för en [!DNL Spark] datamängdstransformatorklass:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>Tar en datauppsättning som indata och skapar en ny härledd datauppsättning</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Mappning av konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">dataset</code>: Indatauppsättningen för omvandling</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

Klassen FeaturePipelineFactory innehåller funktionsextraheringsalgoritmer och definierar faserna i en funktionspipeline från början till slut.

**PySpark**

I följande tabell beskrivs klassmetoderna för en PySpark FeaturePipelineFactory:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>Skapa och returnera en Spark Pipeline som innehåller en serie Spark-omformare</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Mappning av konfigurationsegenskaper</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Hämta och returnera parametermappning från konfigurationsegenskaper</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

I följande tabell beskrivs klassmetoderna för en [!DNL Spark] FeaturePipelineFactory:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>Skapa och returnera en pipeline som innehåller en serie transformerare</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Mappning av konfigurationsegenskaper</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Hämta och returnera parametermappning från konfigurationsegenskaper</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

Klassen PipelineFactory kapslar metoder och definitioner för modellutbildning och poängsättning, där utbildningslogik och algoritmer definieras i form av en [!DNL Spark] pipeline.

**PySpark**

I följande tabell beskrivs klassmetoderna för en PySpark PipelineFactory:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>Skapa och returnera en Spark Pipeline som innehåller logik och algoritm för modellutbildning och poängsättning</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>Returnera en anpassad pipeline som innehåller logik och algoritm för utbildning av en modell. Den här metoden krävs inte om en Spark Pipeline används</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">dataframe</code>: Funktionsuppsättning för utbildningsmaterial</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>Poäng med hjälp av den tränade modellen och returnera resultatet</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">dataframe</code>: Indatauppsättning för poängsättning</li>
                    <li><code class=" language-undefined">model</code>: En tränad modell som används för bedömning</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Hämta och returnera parametermappning från konfigurationsegenskaper</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

I följande tabell beskrivs klassmetoderna för en [!DNL Spark] PipelineFactory:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>Skapa och returnera en pipeline som innehåller logik och algoritm för modellutbildning och poängsättning</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Hämta och returnera parametermappning från konfigurationsegenskaper</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-session</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

Klassen MLEvaluator innehåller metoder för att definiera mätvärden för utvärdering och för att fastställa data för utbildning och testning.

**PySpark**

I följande tabell beskrivs klassmetoderna för en PySpark MLEvaluator:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>Delar in datauppsättningen i underuppsättningar för utbildning och testning</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">dataframe</code>: Indatauppsättning som ska delas</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Utvärderar en utbildad modell och returnerar utvärderingsresultaten</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Självreferens</li>
                    <li><code class=" language-undefined">dataframe</code>: En DataFrame som består av utbildnings- och testdata</li>
                    <li><code class=" language-undefined">model</code>: En tränad modell</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

I följande tabell beskrivs klassmetoderna för en [!DNL Spark] MLEvaluator:

<table>
    <thead>
        <tr>
            <th>Metod och beskrivning</th>
            <th>Parametrar</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>Delar in datauppsättningen i underuppsättningar för utbildning och testning</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">data</code>: Indatauppsättning som ska delas</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrakt</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>Utvärderar en utbildad modell och returnerar utvärderingsresultaten</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationsegenskaper</li>
                    <li><code class=" language-undefined">model</code>: En tränad modell</li>
                    <li><code class=" language-undefined">data</code>: En DataFrame som består av utbildnings- och testdata</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>