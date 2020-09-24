---
keywords: Experience Platform;home;popular topics;data access;python sdk;data access api
solution: Experience Platform
title: Secure Python Data Access SDK
topic: tutorial
type: Tutorial
description: Secure Python Data Access SDK är ett programutvecklingspaket som gör det möjligt att läsa och skriva datauppsättningar från Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# Säker [!DNL Python][!DNL Data Access] SDK

Secure [!DNL Python][!DNL Data Access] SDK är ett programutvecklingspaket som gör det möjligt att läsa och skriva datauppsättningar från Adobe Experience Platform.

## Komma igång

Du måste ha slutfört självstudiekursen för [autentisering](../../tutorials/authentication.md) för att kunna komma åt värdena för att kunna anropa Secure [!DNL Python][!DNL Data Access] SDK:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Om du använder [!DNL Python] SDK måste du ange namnet och ID:t för sandlådan som åtgärden ska utföras i:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

## Miljöinställningar

Som standard är tjänstslutpunkterna inställda på slutpunkter för integreringsmiljö. Till följd av detta anger du följande miljövariabler till följande värden för att peka på produktionen:

| Variabel | Slutpunkt |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

Dessutom kan dina autentiseringsuppgifter läggas till som miljövariabler.

| Variabel | Värde |
| -------- | ----- |
| `ORG_ID` | Ditt `{IMS_ORG}` ID. |
| `SERVICE_API_KEY` | Ditt `{API_KEY}` värde. |
| `USER_TOKEN` | Ditt `{ACCESS_TOKEN}` värde. |
| `SERVICE_TOKEN` | Din `{SERVICE_TOKEN}`som du kan behöva godkänna återkanalsbegäranden mellan tjänster. |
| `SANDBOX_ID` | Värdet `{SANDBOX_ID}` för sandlådan. |
| `SANDBOX_NAME` | Värdet `{SANDBOX_NAME}` för sandlådan. |

## Installation

Alla paket skickas till `./dist` efter att de har skapats.

### Hjul

```python
python3 setup.py bdist_wheel --universal
```

Ladda hjulet från projektkatalogen till din [!DNL Python] 3-miljö.

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### Ägg-fil

```python
python3 setup.py bdist_egg
```

## Läsa en datauppsättning

När du har angett miljövariablerna och slutfört installationen kan datauppsättningen nu läsas i pandabilden.

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### SELECT-kolumner från datauppsättningen

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Hämta partitionsinformation:

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT-sats

Med DISTINCT-satsen kan du hämta alla distinkta värden på rad-/kolumnnivå och ta bort alla dubblettvärden från svaret.

Ett exempel på hur du använder `distinct()` funktionen finns nedan:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE-sats

SDK:n har stöd för vissa operatorer för att filtrera datauppsättningen. [!DNL Python]

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

ORDER BY-satsen tillåter att mottagna resultat sorteras efter en angiven kolumn i en viss ordning (stigande eller fallande). I [!DNL Python] SDK görs detta med hjälp av `sort()` funktionen.

Ett exempel på hur du använder `sort()` funktionen finns nedan:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT-klausul

LIMIT-satsen tillåter användare att begränsa antalet poster som tas emot från datauppsättningen.

Ett exempel på hur du använder `limit()` funktionen finns nedan:

```python
df = dataset_reader.limit(100).read()
```

### OFFSET-sats

Med satsen OFFSET kan användare hoppa över rader från början och börja returnera rader från en senare punkt. I kombination med LIMIT kan detta användas för att iterera rader i block.

Ett exempel på hur du använder `offset()` funktionen finns nedan:

```python
df = dataset_reader.offset(100).read()
```

## Skriva en datauppsättning

SDK [!DNL Python] har stöd för att skriva datauppsättningar. Användarna måste ange den pandabildruta som behöver skrivas till datauppsättningen.

### Skriva pandabilden

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Användarutrymmeskatalog (kontrollpunkt)

För längre jobb som körs kan användaren behöva lagra mellanliggande steg. I instanser som detta ger [!DNL Python] SDK användaren möjlighet att läsa och skriva till ett användarområde.

>[!NOTE]
>
>Sökvägar till data lagras **inte** av SDK:n. Användarna måste lagra motsvarande sökväg till sina respektive data.

### Skriv till användarområde

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Läs från användarområde

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
