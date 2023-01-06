---
keywords: Experience Platform;utvecklarguide;SDK;Data Access SDK;Data Science Workspace;populära topics
solution: Experience Platform
title: Modellredigering med Adobe Experience Platform Platform SDK
description: I den här självstudien får du information om hur du konverterar data_access_sdk_python till den nya Python-plattformen_sdk i både Python och R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Skapa modeller med Adobe Experience Platform [!DNL Platform] SDK

Den här självstudiekursen innehåller information om konvertering `data_access_sdk_python` till nya Python `platform_sdk` i både Python och R. I den här självstudiekursen finns information om följande åtgärder:

- [Bygg autentisering](#build-authentication)
- [Grundläggande läsning av data](#basic-reading-of-data)
- [Grundläggande skrivande av data](#basic-writing-of-data)

## Bygg autentisering {#build-authentication}

Autentisering krävs för att anropa [!DNL Adobe Experience Platform]och består av API-nyckel, IMS Org ID, en användartoken och en tjänsttoken.

### Python

Om du använder Jupyter Notebook, ska du använda koden nedan för att skapa `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Om du inte använder Jupyter Notebook eller behöver ändra IMS-organisationen använder du följande kodexempel:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Om du använder Jupyter Notebook, ska du använda koden nedan för att skapa `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Om du inte använder Jupyter Notebook eller behöver ändra IMS-organisationen använder du följande kodexempel:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Grundläggande läsning av data {#basic-reading-of-data}

Med nya [!DNL Platform] SDK, den maximala lässtorleken är 32 GB med en maximal lästid på 10 minuter.

Om lästiden är för lång kan du försöka med att använda något av följande filtreringsalternativ:

- [Filtrera data efter förskjutning och begränsning](#filter-by-offset-and-limit)
- [Filtrera data efter datum](#filter-by-date)
- [Filtrera data efter kolumn](#filter-by-selected-columns)
- [Få sorterade resultat](#get-sorted-results)

>[!NOTE]
>
>IMS-organisationen anges i `client_context`.

### Python

Läs data i Python genom att använda kodexemplet nedan:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Använd kodexemplet nedan för att läsa data i R:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtrera efter förskjutning och begränsning {#filter-by-offset-and-limit}

Eftersom det inte längre finns stöd för att filtrera efter batch-ID måste du använda `offset` och `limit`.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## Filtrera efter datum {#filter-by-date}

Datumfiltreringens detaljrikedom definieras nu av tidsstämpeln i stället för att anges av dagen.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

Den nya [!DNL Platform] SDK har stöd för följande åtgärder:

| Åtgärd |  -funktion |
| --------- | -------- |
| Är lika med (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Greater than or equal to (`>=`) | `ge()` |
| Less than (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| And (`&`) | `And()` |
| Eller (`|`) | `Or()` |

## Filtrera efter markerade kolumner {#filter-by-selected-columns}

Om du vill förfina läsningen av data ytterligare kan du även filtrera efter kolumnnamn.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Få sorterade resultat {#get-sorted-results}

Mottagna resultat kan sorteras efter angivna kolumner i måldatauppsättningen och i deras ordning (asc/desc).

I följande exempel sorteras dataramen med &quot;column-a&quot; först i stigande ordning. Rader som har samma värden för &quot;column-a&quot; sorteras sedan med &quot;column-b&quot; i fallande ordning.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Grundläggande skrivande av data {#basic-writing-of-data}

>[!NOTE]
>
>IMS-organisationen anges i `client_context`.

Om du vill skriva data i Python och R använder du ett av följande exempel:

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## Nästa steg

När du har konfigurerat `platform_sdk` datainläsaren, bearbetas och delas sedan upp i `train` och `val` datauppsättningar. Läs mer om dataförberedelse och funktionskonstruktion i avsnittet om [dataförberedelse och funktionsteknik](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) i självstudiekursen för att skapa ett recept med [!DNL JupyterLab] bärbara datorer.
