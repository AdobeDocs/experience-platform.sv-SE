---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: Utvecklarhandbok för SDK
topic: Overview
translation-type: tm+mt
source-git-commit: 897e897c80421c8eddd779222ddfa20298e72298

---


# Utvecklarhandbok för SDK

Med SDK för modellredigering kan du utveckla anpassade maskininlärningsrecept och funktionspipeliner som kan användas i Adobe Experience Platform Data Science Workspace och tillhandahålla implementerbara mallar i PySpark och Spark.

Det här dokumentet innehåller information om de olika klasserna i SDK för modellredigering:

- [DataLoader](#dataloader)
   - [Läsa in data från en plattformsdatauppsättning](#load-data-from-a-platform-dataset)
- [DataSaver](#datasaver)
   - [Spara data i en plattformsdatauppsättning](#save-data-to-a-platform-dataset)
- [DatasetTransformer](#datasettransformer)
- [FeaturePipelineFactory](#featurepipelinefactory)
- [PipelineFactory](#pipelinefactory)
- [MLEvaluator](#mlevaluator)

## DataLoader

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

I följande tabell beskrivs de abstrakta metoderna för en Spark Data Loader-klass:

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

### Läsa in data från en plattformsdatauppsättning

Följande exempel hämtar plattformsdata efter ID och returnerar en DataFrame, där datauppsättnings-ID (`datasetId`) är en definierad egenskap i konfigurationsfilen.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```

## DataSaver

Klassen DataSaver kapslar in allt som rör lagring av utdata, inklusive data från poängsättning eller funktionsteknik. Datasparare utökar den abstrakta klassen `DataSaver` och måste åsidosätta den abstrakta metoden `save`.

**PySpark**

I följande tabell beskrivs de abstrakta metoderna för en PySpark-klass:

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

**Spark**

I följande tabell beskrivs de abstrakta metoderna för en Spark Data Saver-klass:

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

### Spara data i en plattformsdatauppsättning

För att kunna lagra data på en plattformsdatauppsättning måste egenskaperna antingen anges eller definieras i konfigurationsfilen:

- Ett giltigt ID för plattformsdatauppsättning som data ska lagras på
- Klient-ID som tillhör din organisation

I följande exempel lagras data (`prediction`) i en plattformsdatauppsättning, där datauppsättnings-ID (`datasetId`) och klient-ID (`tenantId`) definieras i konfigurationsfilen.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## DatasetTransformer

Klassen DatasetTransformer ändrar och omformar strukturen i en datauppsättning. Sensei Machine Learning Runtime kräver inte att den här komponenten definieras och implementeras utifrån dina krav.

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

**Spark**

I följande tabell beskrivs de abstrakta metoderna för en transformerarklass för Spark-datamängd:

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

## FeaturePipelineFactory

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

**Spark**

I följande tabell beskrivs klassmetoderna för en Spark FeaturePipelineFactory:

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

## PipelineFactory

Klassen PipelineFactory kapslar metoder och definitioner för modellutbildning och poängsättning, där utbildningslogik och algoritmer definieras i form av en Spark Pipeline.

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

**Spark**

I följande tabell beskrivs klassmetoderna för en Spark PipelineFactory:

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

## MLEvaluator

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

**Spark**

I följande tabell beskrivs klassmetoderna för en Spark MLEvaluator:

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