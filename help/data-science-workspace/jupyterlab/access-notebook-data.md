---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;%dataset;interactive mode;batch mode;Spark sdk;python sdk;access data;notebook data access
solution: Experience Platform
title: Dataåtkomst i Jupyterlabbes anteckningsböcker
topic: Developer Guide
description: Den här guiden fokuserar på hur du använder Jupyter-anteckningsböcker som är byggda i Data Science Workspace för att få tillgång till dina data.
translation-type: tm+mt
source-git-commit: 645a0f595d268fb08ebfa5652f77a4b1628afcd3
workflow-type: tm+mt
source-wordcount: '3008'
ht-degree: 9%

---


# Dataåtkomst i [!DNL Jupyterlab] bärbara datorer

Varje kärna som stöds har inbyggda funktioner som gör att du kan läsa plattformsdata från en datamängd i en anteckningsbok. JupyterLab i Adobe Experience Platform Data Science Workspace stöder för närvarande bärbara datorer för [!DNL Python], R, PySpark och Scala. Stöd för sidnumrering av data är dock begränsat till bärbara datorer [!DNL Python] och R-datorer. Den här guiden fokuserar på hur du använder JupyterLab-anteckningsböcker för att få tillgång till dina data.

## Komma igång

Innan du läser den här guiden bör du läsa [[!DNL JupyterLab] användarhandboken](./overview.md) för att få en introduktion på hög nivå [!DNL JupyterLab] och dess roll i Data Science Workspace.

## Datagränser för bärbara datorer {#notebook-data-limits}

>[!IMPORTANT]
>
>För PySpark- och Scala-anteckningsböcker om du får ett fel med anledningen&quot;RPC-fjärrklienten har kopplats från&quot;. Detta innebär vanligtvis att minnet håller på att ta slut för drivrutinen eller en exekvering. Försök med att växla till [gruppläge](#mode) för att lösa problemet.

Följande information definierar den maximala mängden data som kan läsas, vilken typ av data som användes och den beräknade tidsramen som läser data.

För [!DNL Python] och R användes en bärbar datorserver som konfigurerats med 40 GB RAM för prestandatesterna. För PySpark och Scala användes ett databricks-kluster som konfigurerats med 64 GB RAM, 8 kärnor, 2 DBU med högst 4 arbetare för de riktmärken som beskrivs nedan.

De ExperienceEvent-schemadata som användes varierade i storlek från ett tusen (1 K) rader på upp till en miljard (1B) rader. Observera att för PySpark och [!DNL Spark] mätvärden användes ett datumintervall på 10 dagar för XDM-data.

Ad hoc-schemadata bearbetades i förväg med [!DNL Query Service] Create Table as Select (CTAS). Dessa data varierade också i storlek från ett tusen (1K) rader, upp till en miljard (1B) rader.

### Använd batchläge jämfört med interaktivt läge {#mode}

När du läser datauppsättningar med bärbara datorer från PySpark och Scala kan du välja att använda interaktivt läge eller gruppläge för att läsa datauppsättningen. Interaktiv används för snabba resultat, medan batchläge används för stora datauppsättningar.

- För bärbara datorer från PySpark och Scala bör batchläge användas när 5 miljoner rader med data eller mer läses. Mer information om effektiviteten i de olika lägena finns i tabellerna [PySpark](#pyspark-data-limits) och [Scala](#scala-data-limits) datagränser nedan.

### [!DNL Python] begränsningar för bärbara datordata

**XDM ExperienceEvent-schema:** Du bör kunna läsa högst 2 miljoner rader (~6,1 GB data på disk) med XDM-data på mindre än 22 minuter. Om du lägger till ytterligare rader kan det leda till fel.

| Antal rader | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Storlek på disk (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (i sekunder) | 20.3 | 86.8 | 63 | 659 | 1315 |

**ad hoc-schema:** Du bör kunna läsa upp maximalt 5 miljoner rader (~5,6 GB data på disk) med data som inte är XDM (ad hoc) på mindre än 14 minuter. Om du lägger till ytterligare rader kan det leda till fel.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Diskstorlek (i MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (i sekunder) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### Datagränser för bärbara datorer

**XDM ExperienceEvent-schema:** Du bör kunna läsa upp maximalt 1 miljon rader XDM-data (3 GB data på disk) på mindre än 13 minuter.

| Antal rader | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Storlek på disk (MB) | 18.73 | 187.5 | 308 | 3000 |
| R Kernel (i sekunder) | 14.03 | 69.6 | 86.8 | 775 |

**ad hoc-schema:** Du bör kunna läsa upp maximalt 3 miljoner rader ad hoc-data (293 MB data på disk) på ca 10 minuter.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Diskstorlek (i MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK (i sek) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### Datagränsgränser för PySpark ([!DNL Python] kernel): {#pyspark-data-limits}

**XDM ExperienceEvent-schema:** I interaktivt läge bör du kunna läsa upp maximalt 5 miljoner rader (~13,42 GB data på disk) med XDM-data på ca 20 minuter. Interaktivt läge stöder endast upp till 5 miljoner rader. Om du vill läsa större datauppsättningar rekommenderar vi att du växlar till gruppläge. I gruppläge bör du kunna läsa upp maximalt 500 miljoner rader (~1,31 TB data på disk) med XDM-data på ca 14 timmar.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Storlek på disk | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK (interaktivt läge) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (gruppläge) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**ad hoc-schema:** I interaktivt läge bör du kunna läsa upp maximalt 5 miljoner rader (~5,36 GB data på disk) med data som inte är XDM på mindre än 3 minuter. I gruppläge bör du kunna läsa upp maximalt 1 miljard rader (~1,05 TB data på disk) med data som inte är XDM på ca 18 minuter.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Storlek på disk | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Interaktivt SDK-läge (i sekunder) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| SDK-batchläge (i sekunder) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] Datagränser för bärbara datorer (Scala kernel): {#scala-data-limits}

**XDM ExperienceEvent-schema:** I interaktivt läge bör du kunna läsa upp maximalt 5 miljoner rader (~13,42 GB data på disk) med XDM-data på ca 18 minuter. Interaktivt läge stöder endast upp till 5 miljoner rader. Om du vill läsa större datauppsättningar rekommenderar vi att du växlar till gruppläge. I gruppläge bör du kunna läsa upp maximalt 500 miljoner rader (~1,31 TB data på disk) med XDM-data på ca 14 timmar.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Storlek på disk | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| Interaktivt SDK-läge (i sekunder) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK-batchläge (i sekunder) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**ad hoc-schema:** I interaktivt läge bör du kunna läsa upp maximalt 5 miljoner rader (~5,36 GB data på disk) med data som inte är XDM på mindre än 3 minuter. I gruppläge bör du kunna läsa upp maximalt 1 miljard rader (~1,05 TB data på disk) med data som inte är XDM på ca 16 minuter.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Storlek på disk | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Interaktivt SDK-läge (i sekunder) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | - | - | - | - | - |
| SDK-batchläge (i sekunder) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

## Python bärbara datorer {#python-notebook}

[!DNL Python] Med bärbara datorer kan du numrera data när du använder datauppsättningar. Exempelkod för att läsa data med och utan sidnumrering visas nedan. Mer information om de tillgängliga startböckerna för Python finns i [[!DNL JupyterLab] startavsnittet](./overview.md#launcher) i användarhandboken för JupyterLab.

Python-dokumentationen nedan beskriver följande koncept:

- [Läsa från en datauppsättning](#python-read-dataset)
- [Skriv till en datauppsättning](#write-python)
- [Frågedata](#query-data-python)
- [Filtrera ExperienceEvent-data](#python-filter)

### Läs från en datauppsättning i Python {#python-read-dataset}

**Utan sidnumrering:**

Om du kör följande kod läses hela datauppsättningen. Om körningen lyckas sparas data som en Pandas-dataram som refereras av variabeln `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Med sidnumrering:**

Om du kör följande kod läses data från den angivna datauppsättningen. Sidnumrering uppnås genom att data begränsas och förskjuts genom funktionerna `limit()` respektive `offset()` . Begränsande data avser det maximala antalet datapunkter som ska läsas, medan förskjutning avser antalet datapunkter som ska hoppas över före läsning av data. Om läsåtgärden körs utan fel sparas data som en Pandas-dataram som variabeln refererar till `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Skriv till en datauppsättning i Python {#write-python}

Om du vill skriva till en datauppsättning i JupyterLab-anteckningsboken väljer du ikonfliken Data (markerad nedan) i den vänstra navigeringen i JupyterLab. The **[!UICONTROL Datasets]** and **[!UICONTROL Schemas]** directories appear. Markera **[!UICONTROL Datasets]** och högerklicka och välj sedan det **[!UICONTROL Write Data in Notebook]** alternativ på den nedrullningsbara menyn som finns i den datauppsättning som du vill använda. En körbar kodpost visas längst ned i anteckningsboken.

![](../images/jupyterlab/data-access/write-dataset.png)

- Använd **[!UICONTROL Write Data in Notebook]** för att generera en skrivcell med den valda datauppsättningen.
- Använd **[!UICONTROL Explore Data in Notebook]** för att generera en läscell med den valda datauppsättningen.
- Använd **[!UICONTROL Query Data in Notebook]** för att generera en grundläggande frågecell med den valda datauppsättningen.

Du kan också kopiera och klistra in följande kodcell. Ersätt både `{DATASET_ID}` och `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Fråga data med [!DNL Query Service] hjälp av [!DNL Python] {#query-data-python}

[!DNL JupyterLab] på [!DNL Platform] kan du använda SQL i en [!DNL Python] anteckningsbok för att komma åt data via [Adobe Experience Platform Query Service](https://www.adobe.com/go/query-service-home-en). Att komma åt data via [!DNL Query Service] kan vara användbart för att hantera stora datauppsättningar på grund av dess överlägsna körtider. Observera att sökning efter data med [!DNL Query Service] har en tidsgräns på tio minuter.

Innan du använder [!DNL Query Service] i [!DNL JupyterLab]måste du ha en fungerande förståelse för [[!DNL Query Service] SQL-syntaxen](https://www.adobe.com/go/query-service-sql-syntax-en).

Om du frågar efter data med [!DNL Query Service] måste du ange namnet på måldatauppsättningen. Du kan generera de nödvändiga kodcellerna genom att söka efter den önskade datauppsättningen med hjälp av **[!UICONTROL Data explorer]**. Högerklicka på datauppsättningslistan och klicka på **[!UICONTROL Query Data in Notebook]** för att generera två kodceller i anteckningsboken. Dessa två celler beskrivs mer ingående nedan.

![](../images/jupyterlab/data-access/python-query-dataset.png)

För att kunna använda [!DNL Query Service] i måste [!DNL JupyterLab]du först skapa en anslutning mellan din fungerande [!DNL Python] anteckningsbok och [!DNL Query Service]. Detta kan du göra genom att köra den första genererade cellen.

```python
qs_connect()
```

I den andra genererade cellen måste den första raden definieras före SQL-frågan. Som standard definierar den genererade cellen en valfri variabel (`df0`) som sparar frågeresultatet som en Pandas-dataram. <br>Argumentet `-c QS_CONNECTION` är obligatoriskt och anger att kernel ska köra SQL-frågan mot [!DNL Query Service]. En lista med ytterligare argument finns i [bilagan](#optional-sql-flags-for-query-service) .

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python-variabler kan refereras direkt i en SQL-fråga med hjälp av strängformaterad syntax och genom att variabler omsluts med klammerparenteser (`{}`), vilket visas i följande exempel:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrera [!DNL ExperienceEvent] data {#python-filter}

För att få åtkomst till och filtrera en [!DNL ExperienceEvent] datauppsättning i en [!DNL Python] anteckningsbok måste du ange ID:t för datauppsättningen (`{DATASET_ID}`) tillsammans med filterreglerna som definierar ett specifikt tidsintervall med logiska operatorer. När ett tidsintervall definieras, ignoreras alla angivna sidnumreringar och hela datauppsättningen beaktas.

En lista med filtreringsoperatorer beskrivs nedan:

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`: Logiskt AND-operator
- `Or()`: Logiskt OR-operator

Följande cell filtrerar en datauppsättning [!DNL ExperienceEvent] till data som finns exklusivt mellan 1 januari 2019 och 31 december 2019.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R bärbara datorer {#r-notebooks}

Med R-anteckningsböcker kan du numrera data när du använder datauppsättningar. Exempelkod för att läsa data med och utan sidnumrering visas nedan. Mer information om vilka bärbara datorer som är tillgängliga finns i avsnittet [[!DNL JupyterLab] Launcher](./overview.md#launcher) i användarhandboken för JupyterLab.

I R-dokumentationen nedan beskrivs följande begrepp:

- [Läsa från en datauppsättning](#r-read-dataset)
- [Skriv till en datauppsättning](#write-r)
- [Filtrera ExperienceEvent-data](#r-filter)

### Läs från en datauppsättning i R {#r-read-dataset}

**Utan sidnumrering:**

Om du kör följande kod läses hela datauppsättningen. Om körningen lyckas sparas data som en Pandas-dataram som refereras av variabeln `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**Med sidnumrering:**

Om du kör följande kod läses data från den angivna datauppsättningen. Sidnumrering uppnås genom att data begränsas och förskjuts genom funktionerna `limit()` respektive `offset()` . Begränsande data avser det maximala antalet datapunkter som ska läsas, medan förskjutning avser antalet datapunkter som ska hoppas över före läsning av data. Om läsåtgärden körs utan fel sparas data som en Pandas-dataram som variabeln refererar till `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### Skriv till en datauppsättning i R {#write-r}

Om du vill skriva till en datauppsättning i JupyterLab-anteckningsboken väljer du ikonfliken Data (markerad nedan) i den vänstra navigeringen i JupyterLab. The **[!UICONTROL Datasets]** and **[!UICONTROL Schemas]** directories appear. Markera **[!UICONTROL Datasets]** och högerklicka och välj sedan det **[!UICONTROL Write Data in Notebook]** alternativ på den nedrullningsbara menyn som finns i den datauppsättning som du vill använda. En körbar kodpost visas längst ned i anteckningsboken.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Använd **[!UICONTROL Write Data in Notebook]** för att generera en skrivcell med den valda datauppsättningen.
- Använd **[!UICONTROL Explore Data in Notebook]** för att generera en läscell med den valda datauppsättningen.

Du kan också kopiera och klistra in följande kodcell:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtrera [!DNL ExperienceEvent] data {#r-filter}

För att få åtkomst till och filtrera en datauppsättning i en R-anteckningsbok måste du ange ID:t för datauppsättningen ( [!DNL ExperienceEvent]`{DATASET_ID}`) tillsammans med filterreglerna som definierar ett specifikt tidsintervall med logiska operatorer. När ett tidsintervall definieras, ignoreras alla angivna sidnumreringar och hela datauppsättningen beaktas.

En lista med filtreringsoperatorer beskrivs nedan:

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`: Logiskt AND-operator
- `Or()`: Logiskt OR-operator

Följande cell filtrerar en datauppsättning [!DNL ExperienceEvent] till data som finns exklusivt mellan 1 januari 2019 och 31 december 2019.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## PySpark 3 bärbara datorer {#pyspark-notebook}

I PySpark-dokumentationen nedan beskrivs följande begrepp:

- [Initiera sparkSession](#spark-initialize)
- [Läsa och skriva data](#magic)
- [Skapa en lokal dataram](#pyspark-create-dataframe)
- [Filtrera ExperienceEvent-data](#pyspark-filter-experienceevent)

### Initierar sparkSession {#spark-initialize}

Alla [!DNL Spark] 2.4 anteckningsböcker kräver att du initierar sessionen med följande standardkod.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Använda %dataset för att läsa och skriva med en PySpark 3-anteckningsbok {#magic}

I och med introduktionen av [!DNL Spark] 2.4 medföljer `%dataset` anpassad magi för användning i bärbara datorer med PySpark 3 ([!DNL Spark] 2.4). Mer information om de magiska kommandon som finns i IPython-kärnan finns i [dokumentationen](https://ipython.readthedocs.io/en/stable/interactive/magics.html)för IPython-magin.


**Användning**

```scala
%dataset {action} --datasetId {id} --dataFrame {df}`
```

**Beskrivning**

Ett anpassat [!DNL Data Science Workspace] magiskt kommando för att läsa eller skriva en datauppsättning från en [!DNL PySpark] bärbar dator ([!DNL Python] 3 kernel).

| Namn | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| `{action}` | Den typ av åtgärd som ska utföras på datauppsättningen. Två åtgärder är tillgängliga,&quot;read&quot; eller&quot;write&quot;. | Ja |
| `--datasetId {id}` | Används för att ange ID för datauppsättningen som ska läsas eller skrivas. | Ja |
| `--dataFrame {df}` | Pandornas dataram. <ul><li> När åtgärden är &quot;read&quot; är {df} variabeln där resultaten av datauppläsningsåtgärden är tillgängliga. </li><li> När åtgärden är&quot;write&quot;, skrivs den här dataramen {df} till datauppsättningen. </li></ul> | Ja |
| `--mode` | En extra parameter som ändrar hur data läses. Tillåtna parametrar är&quot;batch&quot; och&quot;interactive&quot;. Som standard är läget inställt på &quot;interaktiv&quot;. Vi rekommenderar att du använder gruppläge när du läser stora mängder data. | Nej |

>[!TIP]
>
>Granska PySpark-tabellerna i avsnittet [Datagränser](#notebook-data-limits) för bärbara datorer för att avgöra om `mode` ska anges till `interactive` eller `batch`.

**Exempel**

- **Läs exempel**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **Exempel** på skrivning: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

Du kan generera exemplen ovan automatiskt i JupyterLab-köp med följande metod:

Välj fliken Data icon (markerad nedan) i den vänstra navigeringen i JupyterLab. The **[!UICONTROL Datasets]** and **[!UICONTROL Schemas]** directories appear. Markera **[!UICONTROL Datasets]** och högerklicka och välj sedan det **[!UICONTROL Write Data in Notebook]** alternativ på den nedrullningsbara menyn som finns i den datauppsättning som du vill använda. En körbar kodpost visas längst ned i anteckningsboken.

- Används **[!UICONTROL Explore Data in Notebook]** för att generera en läscell.
- Används **[!UICONTROL Write Data in Notebook]** för att generera en skrivcell.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Skapa en lokal dataram {#pyspark-create-dataframe}

Om du vill skapa en lokal dataram med PySpark 3 använder du SQL-frågor. Exempel:

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>Du kan också ange ett valfritt dirigeringsexempel, t.ex. ett booleskt värde med Ersättning, ett dubbelt bråk eller ett långt startvärde.

### Filtrera [!DNL ExperienceEvent] data {#pyspark-filter-experienceevent}

För att få åtkomst till och filtrera en datauppsättning i en PySpark-anteckningsbok måste du ange datamängdens identitet ( [!DNL ExperienceEvent]`{DATASET_ID}`), organisationens IMS-identitet och filterreglerna som definierar ett visst tidsintervall. Ett filtertidsintervall definieras med funktionen `spark.sql()`där funktionsparametern är en SQL-frågesträng.

Följande celler filtrerar en datauppsättning [!DNL ExperienceEvent] till data som finns exklusivt mellan 1 januari 2019 och 31 december 2019.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Skala bärbara datorer {#scala-notebook}

Dokumentationen nedan innehåller exempel på följande koncept:

- [Initiera sparkSession](#scala-initialize)
- [Läs en datauppsättning](#read-scala-dataset)
- [Skriv till en datauppsättning](#scala-write-dataset)
- [Skapa en lokal dataram](#scala-create-dataframe)
- [Filtrera ExperienceEvent-data](#scala-experienceevent)

### Initierar SparkSession {#scala-initialize}

Alla Scala-anteckningsböcker kräver att du initierar sessionen med följande standardkod:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Läs en datauppsättning {#read-scala-dataset}

I Scala kan du importera `clientContext` för att hämta och returnera plattformsvärden, vilket eliminerar behovet av att definiera variabler som `var userToken`. I exemplet Scala nedan `clientContext` används för att hämta och returnera alla värden som behövs för att läsa en datauppsättning.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Element | Beskrivning |
| ------- | ----------- |
| df1 | En variabel som representerar den Pandas-dataram som används för att läsa och skriva data. |
| user-token | Din användartoken som hämtas automatiskt med `clientContext.getUserToken()`. |
| service-token | Din tjänsttoken som hämtas automatiskt med `clientContext.getServiceToken()`. |
| ims-org | Ditt IMS-organisations-ID som hämtas automatiskt med `clientContext.getOrgId()`. |
| api-key | Din API-nyckel som hämtas automatiskt med `clientContext.getApiKey()`. |

>[!TIP]
>
>Granska Scala-tabellerna i avsnittet [Datagränser](#notebook-data-limits) för bärbara datorer för att avgöra om `mode` ska anges till `interactive` eller `batch`.

Du kan generera exemplet ovan automatiskt i JupyterLab genom att använda följande metod:

Välj fliken Data icon (markerad nedan) i den vänstra navigeringen i JupyterLab. The **[!UICONTROL Datasets]** and **[!UICONTROL Schemas]** directories appear. Markera **[!UICONTROL Datasets]** och högerklicka och välj sedan det **[!UICONTROL Explore Data in Notebook]** alternativ på den nedrullningsbara menyn som finns i den datauppsättning som du vill använda. En körbar kodpost visas längst ned i anteckningsboken.
Och
- Används **[!UICONTROL Explore Data in Notebook]** för att generera en läscell.
- Används **[!UICONTROL Write Data in Notebook]** för att generera en skrivcell.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Skriv till en datauppsättning {#scala-write-dataset}

I Scala kan du importera `clientContext` för att hämta och returnera plattformsvärden, vilket eliminerar behovet av att definiera variabler som `var userToken`. I exemplet Scala nedan `clientContext` används för att definiera och returnera alla värden som behövs för att skriva till en datauppsättning.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element | description |
| ------- | ----------- |
| df1 | En variabel som representerar den Pandas-dataram som används för att läsa och skriva data. |
| user-token | Din användartoken som hämtas automatiskt med `clientContext.getUserToken()`. |
| service-token | Din tjänsttoken som hämtas automatiskt med `clientContext.getServiceToken()`. |
| ims-org | Ditt IMS-organisations-ID som hämtas automatiskt med `clientContext.getOrgId()`. |
| api-key | Din API-nyckel som hämtas automatiskt med `clientContext.getApiKey()`. |

>[!TIP]
>
>Granska Scala-tabellerna i avsnittet [Datagränser](#notebook-data-limits) för bärbara datorer för att avgöra om `mode` ska anges till `interactive` eller `batch`.

### skapa en lokal dataram {#scala-create-dataframe}

SQL-frågor krävs för att skapa en lokal dataram med Scala. Exempel:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtrera [!DNL ExperienceEvent] data {#scala-experienceevent}

För att få åtkomst till och filtrera en datauppsättning i en Scala-anteckningsbok måste du ange datamängdens identitet ( [!DNL ExperienceEvent]`{DATASET_ID}`), organisationens IMS-identitet och filterreglerna som definierar ett visst tidsintervall. Ett filtertidsintervall definieras med funktionen `spark.sql()`där funktionsparametern är en SQL-frågesträng.

Följande celler filtrerar en datauppsättning [!DNL ExperienceEvent] till data som finns exklusivt mellan 1 januari 2019 och 31 december 2019.

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## Nästa steg

Det här dokumentet innehåller allmänna riktlinjer för åtkomst av datauppsättningar med JupyterLab-anteckningsböcker. Mer information om hur du frågar efter datauppsättningar finns i [Query Service i dokumentationen för JupyterLab-anteckningsböcker](./query-service.md) . Mer information om hur du utforskar och visualiserar datauppsättningar finns i dokumentet om hur du [analyserar data med bärbara datorer](./analyze-your-data.md).

## Valfria SQL-flaggor för [!DNL Query Service] {#optional-sql-flags-for-query-service}

Den här tabellen visar de valfria SQL-flaggor som kan användas för [!DNL Query Service].

| **Flagga** | **Beskrivning** |
| --- | --- |
| `-h`, `--help` | Visa hjälpmeddelandet och avsluta. |
| `-n`, `--notify` | Växla alternativ för att meddela frågeresultat. |
| `-a`, `--async` | Om du använder den här flaggan körs frågan asynkront och kerneln kan frigöras medan frågan körs. Var försiktig när du tilldelar frågeresultat till variabler eftersom de kan vara odefinierade om frågan inte är fullständig. |
| `-d`, `--display` | Om du använder den här flaggan kan du inte visa resultat. |

