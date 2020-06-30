---
keywords: Experience Platform;Tutorial;feature pipeline;Data Science Workspace;popular topics
solution: Adobe Experience Platform Data Science Workspace
title: Skapa en funktionspipeline
topic: Tutorial
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---


# Skapa en funktionspipeline

>[!IMPORTANT]
> Funktionspipeliner är för närvarande bara tillgängliga via API.

Med Adobe Experience Platform kan du skapa och skapa anpassade rörledningar för att utföra funktionstekniker i stor skala via Sensei Machine Learning Framework Runtime (nedan kallad Runtime).

I det här dokumentet beskrivs de olika klasserna som finns i en funktionspipeline och här finns en stegvis självstudiekurs för att skapa en anpassad funktionspipeline med hjälp av [Model Authoring SDK](./sdk.md) i PySpark.

Följande arbetsflöde utförs när en funktionspipeline körs:

1. Mottagaren läser in datauppsättningen till en pipeline.
2. Funktionsomformningen görs på datauppsättningen och skrivs tillbaka till Adobe Experience Platform.
3. De omformade data läses in för utbildning.
4. Funktionspipelinen definierar faserna med regressorn för övertoning som vald modell.
5. Rörledningen används för att passa utbildningsdata och den tränade modellen skapas.
6. Modellen omformas med bedömningsdatauppsättningen.
7. Intressanta kolumner i utdata markeras sedan och sparas tillbaka till [!DNL Experience Platform] de associerade data.

## Komma igång

Följande krävs för att köra ett recept i en organisation:
- En indatamängd.
- Datamängdens schema.
- Ett transformerat schema och en tom datauppsättning som baseras på det schemat.
- Ett utdataschema och en tom datauppsättning som baseras på det schemat.

Alla ovanstående datauppsättningar måste överföras till [!DNL Platform] användargränssnittet. Använd det Adobe-medföljande [bootstrap-skriptet](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap)för att konfigurera detta.

## Aktuella pipeline-klasser

I följande tabell beskrivs de huvudabstrakta klasser som du måste utöka för att kunna skapa en funktionspipeline:

| Abstrakt klass | Beskrivning |
| -------------- | ----------- |
| DataLoader | En DataLoader-klass tillhandahåller implementering för hämtning av indata. |
| DatasetTransformer | En DataSetTransformer-klass tillhandahåller implementeringar för att omvandla indatamängden. Du kan välja att inte tillhandahålla en DatasetTransformer-klass och i stället implementera den funktionstekniska logiken i klassen FeaturePipelineFactory. |
| FeaturePipelineFactory | Klassen FeaturePipelineFactory bygger en Spark Pipeline som består av en serie Spark-omformare som utför funktionskonstruktion. Du kan välja att inte tillhandahålla en FeaturePipelineFactory-klass och i stället implementera den funktionstekniska logiken i klassen DatasetTransformer. |
| DataSaver | En DataSaver-klass innehåller logiken för lagring av en funktionsdatauppsättning. |

När ett funktionsförloppsjobb initieras kör körtiden först DataLoader för att läsa in indata som en DataFrame och ändrar sedan DataFrame genom att köra antingen DatasetTransformer, FeaturePipelineFactory eller båda. Slutligen lagras den resulterande funktionsdatauppsättningen via DataSaver.

I följande flödesschema visas körningsordningen:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementera dina rörliga funktionsklasser {#implement-your-feature-pipeline-classes}

I följande avsnitt finns detaljerad information och exempel om hur du implementerar de klasser som krävs för en funktionspipeline.

### Definiera variabler i JSON-konfigurationsfilen {#define-variables-in-the-configuration-json-file}

JSON-konfigurationsfilen består av nyckelvärdepar och är avsedd för att du ska kunna ange variabler som ska definieras senare under körning. Dessa nyckelvärdepar kan definiera egenskaper som plats för indatauppsättning, ID för utdatauppsättning, klientorganisations-ID, kolumnrubriker osv.

I följande exempel visas nyckelvärdepar i en konfigurationsfil:

**JSON-konfigurationsexempel**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
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

Du kan komma åt konfigurations-JSON via alla klassmetoder som definierar `config_properties` som en parameter. Exempel:

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Se filen [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) från Data Science Workspace för ett mer ingående konfigurationsexempel.

### Förbered indata med DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader ansvarar för hämtning och filtrering av indata. Din implementering av DataLoader måste utöka den abstrakta klassen `DataLoader` och åsidosätta den abstrakta metoden `load`.

I följande exempel hämtas en datauppsättning med ett ID och returneras som en DataFrame, där datauppsättnings-ID ( [!DNL Platform]`dataset_id`) är en definierad egenskap i konfigurationsfilen.

**PySpark-exempel**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

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

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### Transformera en datauppsättning med DataSetTransformer {#transform-a-dataset-with-datasettransformer}

En DataSetTransformer tillhandahåller logiken för att omforma en DataFrame-indata och returnerar en ny härledd DataFrame. Den här klassen kan implementeras för att arbeta i samarbete med en FeaturePipelineFactory, fungera som den enda funktionstekniska komponenten, eller så kan du välja att inte implementera den här klassen.

I följande exempel utökas klassen DatasetTransformer:


**PySpark-exempel**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### Ingenjörsdatafunktioner med FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Med en FeaturePipelineFactory kan du implementera din funktionstekniska logik genom att definiera och sammanfoga en serie Spark-omvandlare via en Spark Pipeline. Den här klassen kan implementeras för att antingen fungera tillsammans med en DatasetTransformer, fungera som den enda funktionstekniska komponenten eller så kan du välja att inte implementera den här klassen.

I följande exempel utökas klassen FeaturePipelineFactory:

**PySpark-exempel**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### Lagra dina funktionsdata med DataSaver {#store-your-feature-dataset-with-datasaver}

DataSaver ansvarar för att lagra de resulterande funktionsdatauppsättningarna på en lagringsplats. Din implementering av DataSaver måste utöka den abstrakta klassen `DataSaver` och åsidosätta den abstrakta metoden `save`.

I följande exempel utökas klassen DataSaver som lagrar data till en datauppsättning per ID, där dataset-ID ( [!DNL Platform] ) och tenant-ID (`featureDatasetId``tenantId`) definieras i konfigurationen.

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


### Ange dina implementerade klassnamn i programfilen {#specify-your-implemented-class-names-in-the-application-file}

Nu när du har definierat och implementerat dina funktionspipeline-klasser måste du ange namnen på klasserna i programmets YAML-fil.

I följande exempel anges implementerade klassnamn:

**PySpark-exempel**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## Skapa en rörlig motor för funktioner med API {#create-feature-pipeline-engine-api}

Nu när du har skapat din funktionspipeline måste du skapa en Docker-bild för att kunna anropa funktionens pipeline-slutpunkter i [!DNL Sensei Machine Learning] API. Du behöver en Docker-bild-URL för att kunna anropa funktionens pipeline-slutpunkter.

>[!TIP]
>Om du inte har någon Docker-URL kan du gå till [Paketkällfilerna i en recept](../models-recipes/package-source-files-recipe.md) -självstudiekurs för att stegvis gå igenom hur du skapar en Docker-värd-URL.

Du kan också använda följande Postman-samling för att underlätta arbetet med API:t för funktionspipeline:

https://www.getpostman.com/collections/c5fc0d1d5805a5ddd41a

### Skapa en rörlig motor för funktioner {#create-engine-api}

När du har din Docker-bildplats kan du [skapa en rörlig funktionsmotor](../api/engines.md#feature-pipeline-docker) med hjälp av [!DNL Sensei Machine Learning] API:t genom att utföra en POST till `/engines`. En rörledningsmotor för funktioner har skapat en unik identifierare (`id`) för motorn. Spara värdet innan du fortsätter.

### Skapa en MLInstance {#create-mlinstance}

Med hjälp av den nya instansen `engineID`måste du [skapa en MLIstance](../api/mlinstances.md#create-an-mlinstance) genom att göra en POST-begäran till `/mlInstance` slutpunkten. Ett godkänt svar returnerar en nyttolast som innehåller information om den nyligen skapade MLInstance-instansen, inklusive dess unika identifierare (`id`) som används i nästa API-anrop.

### Skapa en expert {#create-experiment}

Sedan måste du [skapa en expert](../api/experiments.md#create-an-experiment). Om du vill skapa en expert måste du ha en unik identifierare (`id`) för din MLIstance och göra en POST-begäran till `/experiment` slutpunkten. Ett lyckat svar returnerar en nyttolast som innehåller information om den nyligen skapade experten, inklusive dess unika identifierare (`id`) som används i nästa API-anrop.

### Ange pipeline-uppgiften för funktionen för experimentell körning {#specify-feature-pipeline-task}

När du har skapat en Experiment måste du ändra Experimentens läge till `featurePipeline`. Om du vill ändra läget gör du en extra POST [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) till med `EXPERIMENT_ID` och i brödtexten som du skickar `{ "mode":"featurePipeline"}` för att ange en testkörning av funktionsflödet.

När du är klar skickar du en GET-begäran om `/experiments/{EXPERIMENT_ID}` att [hämta experimentstatusen](../api/experiments.md#retrieve-specific) och väntar på att Experimentstatusen ska uppdateras.

### Ange utbildningsuppgift för körning av experiment {#training}

Därefter måste du [specificera uppgiften](../api/experiments.md#experiment-training-scoring)för utbildningskörningen. Gör en POST till `experiments/{EXPERIMENT_ID}/runs` och ange i brödtexten läget till `train` och skicka en array med uppgifter som innehåller dina utbildningsparametrar. Ett godkänt svar returnerar en nyttolast som innehåller information om den begärda experten.

När du är klar skickar du en GET-begäran om `/experiments/{EXPERIMENT_ID}` att [hämta experimentstatusen](../api/experiments.md#retrieve-specific) och väntar på att Experimentstatusen ska uppdateras.

### Ange poänguppgiften för testkörningen {#scoring}

>[!NOTE]
> För att slutföra det här steget måste du ha minst en lyckad utbildning kopplad till din Experiment.

Efter en lyckad utbildning måste du [ange poängkörningsuppgift](../api/experiments.md#experiment-training-scoring). Gör en POST till `experiments/{EXPERIMENT_ID}/runs` och i brödtexten ställ in attributet `mode` till &quot;score&quot;. Detta startar din resultatutvärderingsexpertsession.

När du är klar skickar du en GET-begäran om `/experiments/{EXPERIMENT_ID}` att [hämta experimentstatusen](../api/experiments.md#retrieve-specific) och väntar på att Experimentstatusen ska uppdateras.

När poängsättningen är klar bör ditt tillvägagångssätt fungera.

## Nästa steg {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

Genom att läsa det här dokumentet har du skapat en funktionspipeline med hjälp av Model Authoring SDK, skapat en Docker-bild och använt Docker-bildens URL för att skapa en funktionspipeline med hjälp av [!DNL Sensei Machine Learning] API. Nu kan du fortsätta att omforma datauppsättningar och extrahera datafunktioner i stor skala med [!DNL Sensei Machine Learning API](../api/getting-started.md).