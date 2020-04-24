---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: Skapa en rörledning för funktioner
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Skapa en rörledning för funktioner

Med Adobe Experience Platform kan ni skapa och skapa anpassade funktionspipeliner för att utföra funktionsteknologi i stor skala via Sensei Machine Learning Framework Runtime (nedan kallad Runtime).

I det här dokumentet beskrivs de olika klasserna som finns i en funktionspipeline och här finns en stegvis självstudiekurs för att skapa en anpassad [funktionspipeline med hjälp av SDK](./sdk.md) för modellredigering i PySpark och Spark.

## Funktionsförloppsklasser

I följande tabell beskrivs de huvudsakliga Abstract-klasser som du måste utöka för att kunna skapa en funktionspipeline:

| Abstrakt klass | Beskrivning |
| -------------- | ----------- |
| DataLoader | En DataLoader-klass tillhandahåller implementering för hämtning av indata. |
| DatasetTransformer | En DataSetTransformer-klass tillhandahåller implementeringar för att omvandla indatamängden. Du kan välja att inte tillhandahålla en DatasetTransformer-klass och i stället implementera den funktionstekniska logiken i klassen FeaturePipelineFactory. |
| FeaturePipelineFactory | Klassen FeaturePipelineFactory bygger en Spark Pipeline som består av en serie Spark-omformare som utför funktionskonstruktion. Du kan välja att inte tillhandahålla en FeaturePipelineFactory-klass och i stället implementera den funktionstekniska logiken i klassen DatasetTransformer. |
| DataSaver | En DataSaver-klass innehåller logiken för lagring av en funktionsdatauppsättning. |

När ett funktionsförloppsjobb initieras kör körningsmiljön först DataLoader för att läsa in indata som en DataFrame och ändrar sedan DataFrame genom att köra antingen DatasetTransformer, FeaturePipelineFactory eller båda. Slutligen lagras den resulterande funktionsdatauppsättningen via DataSaver.

I följande flödesschema visas körningsordningen:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementera dina rörliga funktionsklasser {#implement-your-feature-pipeline-classes}

I följande avsnitt finns detaljerad information och exempel om hur du implementerar de klasser som krävs för en funktionspipeline.

### Definiera variabler i JSON-konfigurationsfilen {#define-variables-in-the-configuration-json-file}

JSON-konfigurationsfilen består av nyckelvärdepar och är avsedd för att du ska kunna ange variabler som ska definieras senare under körning. Dessa nyckelvärdepar kan definiera egenskaper som plats för indatauppsättning, ID för utdatauppsättning, klientorganisations-ID, kolumnrubriker osv.

I följande exempel visas nyckelvärdepar som finns i en konfigurationsfil. Expandera exemplet för att se detaljer:


**JSON-konfigurationsexempel**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```



Du kan komma åt konfigurations-JSON via alla klassmetoder som definierar `configProperties` som en parameter. Exempel:

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### Förbered indata med DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader ansvarar för hämtning och filtrering av indata. Din implementering av DataLoader måste utöka den abstrakta klassen `DataLoader` och åsidosätta den abstrakta metoden `load`.

I följande exempel hämtas en plattformsdatauppsättning med ID och returneras som en DataFrame, där datauppsättnings-ID (`datasetId`) är en definierad egenskap i konfigurationsfilen. Expandera varje exempel för att se detaljer:


**PySpark-exempel**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

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
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Spark-exempel**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
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



### Transformera en datauppsättning med DataSetTransformer {#transform-a-dataset-with-datasettransformer}

En DataSetTransformer tillhandahåller logiken för att omforma en DataFrame-indata och returnerar en ny härledd DataFrame. Den här klassen kan implementeras för att arbeta i samarbete med en FeaturePipelineFactory, fungera som den enda funktionstekniska komponenten, eller så kan du välja att inte implementera den här klassen.

I följande exempel utökas klassen DatasetTransformer. Expandera varje exempel för att se detaljer:


**PySpark-exempel**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Spark-exempel**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### Ingenjörsdatafunktioner med FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Med en FeaturePipelineFactory kan du implementera din funktionstekniska logik genom att definiera och sammanfoga en serie Spark-omvandlare via en Spark Pipeline. Den här klassen kan implementeras för att antingen fungera tillsammans med en DatasetTransformer, fungera som den enda funktionstekniska komponenten eller så kan du välja att inte implementera den här klassen.

I följande exempel utökas klassen FeaturePipelieFactory och en serie Spark-omformare implementeras som flera steg i en Spark Pipeline. Expandera varje exempel för att se detaljer:


**PySpark-exempel**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Spark-exempel**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### Lagra dina funktionsdata med DataSaver {#store-your-feature-dataset-with-datasaver}

DataSaver ansvarar för att lagra de resulterande funktionsdatauppsättningarna på en lagringsplats. Din implementering av DataSaver måste utöka den abstrakta klassen `DataSaver` och åsidosätta den abstrakta metoden `save`.

Följande exempel utökar klassen DataSaver som lagrar data till en plattformsdatauppsättning per ID, där dataset-ID (`featureDatasetId`) och klient-ID (`tenantId`) definieras i konfigurationsfilen. Expandera varje exempel för att se detaljer:


**PySpark-exempel**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
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

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark-exempel**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
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

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### Ange dina implementerade klassnamn i programfilen {#specify-your-implemented-class-names-in-the-application-file}

Nu när du har definierat och implementerat klasserna för rörledning för funktioner måste du ange namnen på klasserna i programfilen.

I följande exempel anges implementerade klassnamn. Expandera exemplet för att se detaljer:


**PySpark-exempel**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Spark-exempel**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## Bygg den binära artefakten {#build-the-binary-artifact}

Nu när du har implementerat dina rörliga funktionsklasser kan du skapa och kompilera den till en binär artefakt som sedan kan användas för att skapa en rörlig funktion via API-anrop.

**PySpark**

Om du vill skapa en PySpark-funktionspipeline kör du Python-skriptet som finns i rotkatalogen i Model Authoring SDK. `setup.py`

>[!NOTE] För att bygga en PySpark-funktionspipeline måste du ha Python 3 installerat på datorn.

```shell
python3 setup.py bdist_egg
```

Funktionspipelinen kommer att generera en `.egg` artefakt i `/dist` katalogen. Artefakten används för att skapa en funktionspipeline.

**Spark**

Kör följande konsolkommando i rotkatalogen för Model Authoring SDK när du vill skapa en Spark-funktionspipeline:

>[!NOTE] Om du vill skapa en Spark Feature Pipeline måste du ha Scala och sbt installerat på datorn.

```shell
mvn clean install
```

Funktionspipelinen kommer att generera en `.jar` artefakt i `/dist` katalogen. Artefakten används för att skapa en funktionspipeline.

## Skapa en rörlig motor med funktioner med API:t {#create-a-feature-pipeline-engine-using-the-api}

Nu när du har skapat din funktionspipeline och byggt den binära artefakten kan du [skapa en rörlig funktionsmotor med hjälp av API:t](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts)för Sensei Machine Learning. En rörledningsmotor för funktioner kommer att förse dig med ett motor-ID som en del av svarstexten. Spara värdet innan du fortsätter med nästa steg.

## Nästa steg {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

Genom att läsa det här dokumentet har du skapat en funktionspipeline med SDK för modellredigering, byggt en binär artefakt och använt artefakten för att skapa en rörlig funktionsmotor via ett API-anrop. Nu kan du [skapa en rörmodell](../api/mlinstances.md#create-an-mlinstance) för funktioner med den nya motorn och börja omforma datauppsättningar och extrahera datafunktioner i stor skala.