---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SDK för säker Spark-dataåtkomst
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Säker [!DNL Spark Data Access] SDK

Secure [!DNL Spark][!DNL Data Access] SDK är ett programutvecklingspaket som gör det möjligt att läsa och skriva data från Adobe Experience Platform.

## Komma igång

Du måste ha slutfört självstudiekursen för [autentisering](../../tutorials/authentication.md) för att kunna komma åt värdena för att kunna anropa Secure [!DNL Spark][!DNL Data Access] SDK:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Om du använder [!DNL Spark] SDK måste du ange namnet och ID:t för sandlådan som åtgärden ska utföras i:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

## Miljöinställningar

SDK förväntar [!DNL Spark] att du anger autentiseringsuppgifter i miljövariabler eller alternativ för datakälla.

| Variabel | Värde |
| -------- | ----- | 
| `SERVICE_TOKEN` | Din tjänstauktoriseringstoken. |
| `SERVICE_API_KEY` | Tjänstens API-nyckel. Detta är vanligtvis detsamma som ditt IMS-klient-ID. |
| `ORG_ID` | Ditt `{IMS_ORG}` ID-värde. |
| `USER_TOKEN` | Ditt `{ACCESS_TOKEN}` värde. |

Andra konfigurationsparametrar är:

| Variabel | Värde |
| -------- | ----- |
| `ENVIRONMENT_NAME` | Den miljö du försöker ansluta till. Det kan vara &quot;dev&quot;, &quot;stage&quot; eller &quot;prod&quot;. |
| `SANDBOX_NAME` | Namnet på den sandlåda som du ansluter till. |

Förutom `ENVIRONMENT_NAME`kan du även ange de ovanstående miljövariablerna i `QSOption`enligt exemplet nedan:

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## Installation

För att använda [!DNL Spark] SDK krävs prestandaoptimeringar som måste läggas till i `SparkSession`. Du kan tillämpa dem på något av följande sätt:

Använd den direkt på den aktuella SparkSession:

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

Ange följande conf före eller när SparkSession skapas:

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## Läsa en datauppsättning

SDK:n har stöd för två [!DNL Spark] läslägen: interaktivt och gruppvis.

I det interaktiva läget skapas en Java Database Connectivity-anslutning (JDBC) till [!DNL Query Service] och resultat fås genom en vanlig JDBC `ResultSet` som automatiskt översätts till en `DataFrame`. Det här läget fungerar ungefär som den inbyggda [!DNL Spark] metoden `spark.read.jdbc()`. Det här läget är endast avsett för små datauppsättningar och kräver endast en användartoken för autentisering.

I gruppläget används [!DNL Query Service]kommandot COPY för att generera resultatuppsättningar för Parquet på en delad plats. Dessa Parquet-filer kan sedan bearbetas ytterligare. Det här läget kräver både en användartoken och en tjänsttoken med `acp.foundation.catalog.credentials` omfånget.

Ett exempel på hur du läser en datauppsättning i interaktivt läge visas nedan:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

Ett exempel på hur du läser en datauppsättning i batchläge visas nedan:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

### SELECT-kolumner från datauppsättningen

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT-sats

Med DISTINCT-satsen kan du hämta alla distinkta värden på rad-/kolumnnivå och ta bort alla dubblettvärden från svaret.

Ett exempel på hur du använder `distinct()` funktionen finns nedan:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE-sats

I [!DNL Spark] SDK kan du filtrera på två sätt: Använda ett SQL-uttryck eller filtrera genom villkor.

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

ORDER BY-satsen tillåter att mottagna resultat sorteras efter en angiven kolumn i en viss ordning (stigande eller fallande). I [!DNL Spark] SDK görs detta med hjälp av `sort()` funktionen.

Ett exempel på hur du använder `sort()` funktionen finns nedan:

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-klausul

LIMIT-satsen tillåter användare att begränsa antalet poster som tas emot från datauppsättningen.

Ett exempel på hur du använder `limit()` funktionen finns nedan:

```scala
df = df.limit(100)
```

## Skriva till en datauppsättning

SDK [!DNL Spark] har stöd för att skriva datauppsättningar. Användarna måste först hämta en tidigare datauppsättning för att kunna skriva till en ny datauppsättning.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
