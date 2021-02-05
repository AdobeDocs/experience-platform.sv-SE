---
keywords: Experience Platform;hem;populära ämnen;dataåtkomst;python sdk;dataåtkomst api;read python;write python
solution: Experience Platform
title: Åtkomst till data med Python i datavetenskapen
topic: tutorial
type: Tutorial
description: Följande dokument innehåller exempel på hur du får åtkomst till data i Python för användning i Data Science Workspace.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---


# Åtkomst till data med Python i Data Science Workspace

Följande dokument innehåller exempel på hur du får åtkomst till data med Python för användning i Data Science Workspace. Information om hur du får åtkomst till data med JupyterLab-anteckningsböcker finns i [dokumentationen för JupyterLab-anteckningsböcker för dataåtkomst](../jupyterlab/access-notebook-data.md).

## Läsa en datauppsättning

När du har angett miljövariablerna och slutfört installationen kan din datauppsättning nu läsas i pandabilden.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### SELECT-kolumner från datauppsättningen

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Hämta partitionsinformation:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT-sats

Med DISTINCT-satsen kan du hämta alla distinkta värden på rad-/kolumnnivå och ta bort alla dubblettvärden från svaret.

Ett exempel på hur du använder funktionen `distinct()` visas nedan:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE-sats

Du kan använda vissa operatorer i Python för att filtrera datauppsättningen.

>[!NOTE]
>
>De funktioner som används för filtrering är skiftlägeskänsliga.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Ett exempel på hur du använder dessa filtreringsfunktioner finns nedan:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY-instruktion

ORDER BY-satsen tillåter att mottagna resultat sorteras efter en angiven kolumn i en viss ordning (stigande eller fallande). Detta görs med funktionen `sort()`.

Ett exempel på hur du använder funktionen `sort()` visas nedan:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT-klausul

Med LIMIT-satsen kan du begränsa antalet poster som tas emot från datauppsättningen.

Ett exempel på hur du använder funktionen `limit()` visas nedan:

```python
df = dataset_reader.limit(100).read()
```

### OFFSET-sats

Med satsen OFFSET kan du hoppa över rader från början och börja returnera rader från en senare punkt. I kombination med LIMIT kan detta användas för att iterera rader i block.

Ett exempel på hur du använder funktionen `offset()` visas nedan:

```python
df = dataset_reader.offset(100).read()
```

## Skriva en datauppsättning

Om du vill skriva till en datauppsättning måste du förse din datauppsättning med pandabilder.

### Skriva pandabilden

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Användarutrymmeskatalog (kontrollpunkt)

För längre jobb som körs kan du behöva lagra mellanliggande steg. I instanser som detta kan du läsa och skriva till ett användarområde.

>[!NOTE]
>
>Sökvägar till data är **inte** lagrade. Du måste lagra motsvarande sökväg till respektive data.

### Skriv till användarområde

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Läs från användarområde

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Nästa steg

Adobe Experience Platform Data Science Workspace innehåller ett recept som använder ovanstående kodexempel för att läsa och skriva data. Om du vill veta mer om hur du använder Python för att få tillgång till dina data kan du läsa [Data Science Workspace Python GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).