---
keywords: Experience Platform;hem;populära ämnen;dataåtkomst;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: Åtkomst till data med Spark in Data Science Workspace
type: Tutorial
description: Följande dokument innehåller exempel på hur du får åtkomst till data med Spark för användning i Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Åtkomst till data med Spark in Data Science Workspace

Följande dokument innehåller exempel på hur du får åtkomst till data med Spark för användning i Data Science Workspace. Information om hur du får åtkomst till data med JupyterLab-anteckningsböcker finns på [Dataåtkomst för JupyterLab-anteckningsböcker](../jupyterlab/access-notebook-data.md) dokumentation.

## Komma igång

Använda [!DNL Spark] kräver prestandaoptimeringar som behöver läggas till i `SparkSession`. Dessutom kan du konfigurera `configProperties` för att senare läsa och skriva till datauppsättningar.

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Läsa en datauppsättning

När du använder Spark har du tillgång till två läslägen: interaktivt och gruppvis.

I det interaktiva läget skapas en Java Database Connectivity-anslutning (JDBC) till [!DNL Query Service] och får resultat via en vanlig JDBC `ResultSet` som automatiskt översätts till `DataFrame`. Det här läget fungerar ungefär som det inbyggda [!DNL Spark] method `spark.read.jdbc()`. Det här läget är endast avsett för små datauppsättningar. Om datauppsättningen överstiger 5 miljoner rader föreslår vi att du byter till gruppläge.

Batchläget använder [!DNL Query Service]&#39;s COPY command to generate Parquet result sets in a shared location. Dessa Parquet-filer kan sedan bearbetas ytterligare.

Ett exempel på hur du läser en datauppsättning i interaktivt läge visas nedan:

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

Ett exempel på hur du läser en datauppsättning i batchläge visas nedan:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### SELECT-kolumner från datauppsättningen

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT-sats

Med DISTINCT-satsen kan du hämta alla distinkta värden på rad-/kolumnnivå och ta bort alla dubblettvärden från svaret.

Ett exempel på hur du använder `distinct()` finns nedan:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE-sats

The [!DNL Spark] SDK tillåter två filtreringsmetoder: Använda ett SQL-uttryck eller filtrera genom villkor.

Ett exempel på hur du använder dessa filtreringsfunktioner finns nedan:

#### SQL-uttryck

```scala
df.where("age > 15")
```

#### Filtreringsvillkor

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY-instruktion

ORDER BY-satsen tillåter att mottagna resultat sorteras efter en angiven kolumn i en viss ordning (stigande eller fallande). I [!DNL Spark] SDK, detta görs med `sort()` funktion.

Ett exempel på hur du använder `sort()` finns nedan:

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-klausul

Med LIMIT-satsen kan du begränsa antalet poster som tas emot från datauppsättningen.

Ett exempel på hur du använder `limit()` finns nedan:

```scala
df = df.limit(100)
```

## Skriva till en datauppsättning

Med `configProperties` kan du skriva till en datauppsättning i Experience Platform med `QSOption`.

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Nästa steg

Adobe Experience Platform Data Science Workspace innehåller ett Scala-recept (Spark) som använder ovanstående kodexempel för att läsa och skriva data. Om du vill veta mer om hur du använder Spark för att få tillgång till dina data kan du läsa [Data Science Workspace Scala GitHub-databas](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
