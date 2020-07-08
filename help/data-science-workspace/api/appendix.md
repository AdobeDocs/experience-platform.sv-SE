---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Bilaga
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---


# Bilaga

I följande avsnitt finns referensinformation för olika funktioner i [!DNL Sensei Machine Learning] API:t.

## Frågeparametrar för hämtning av resurser {#query}

API:t [!DNL Sensei Machine Learning] har stöd för frågeparametrar med hämtning av resurser. Tillgängliga frågeparametrar och deras användning beskrivs i följande tabell:

| Frågeparameter | Beskrivning | Standardvärde |
| --------------- | ----------- | ------- |
| `start` | Anger startindex för sidnumrering. | `start=0` |
| `limit` | Anger det maximala antalet resultat som ska returneras. | `limit=25` |
| `orderby` | Anger de egenskaper som ska användas för sortering i prioritetsordning. Inkludera ett streck (**-**) före ett egenskapsnamn om du vill sortera i fallande ordning, annars sorteras resultaten i stigande ordning. | `orderby=created` |
| `property` | Anger det jämförelseuttryck som ett objekt måste uppfylla för att kunna returneras. | `property=deleted==false` |

>[!NOTE]
>
>När du kombinerar flera frågeparametrar måste de avgränsas med et-tecken (**&amp;**).

## Python CPU- och GPU-konfigurationer {#cpu-gpu-config}

Python Engines har möjlighet att välja mellan antingen en CPU eller en GPU för sin utbildning eller i poängsyfte, och definieras på en [MLInstance](./mlinstances.md) som en uppgiftsspecifikation (`tasks.specification`).

Följande är ett exempel på konfiguration som anger hur du använder en CPU för utbildning och en GPU för bedömning:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>Värdena för `cpus` och `gpus` anger inte antalet CPU:er eller grafikprocessorer, utan antalet fysiska datorer. Dessa värden är tillåtna `"1"` och genererar i annat fall ett undantag.

## Resurskonfigurationer för PySpark och Spark {#resource-config}

Spark Engines kan modifiera beräkningsresurser för utbildning och poängsättning. Dessa resurser beskrivs i följande tabell:

| Resurs | Beskrivning | Typ |
| -------- | ----------- | ---- |
| driverMemory | Minne för drivrutin i megabyte | int |
| driverCores | Antal kärnor som används av drivrutinen | int |
| exutorMemory | Minne för körare i megabyte | int |
| exutorCores | Antal kärnor som används av köraren | int |
| numExecutors | Antal körare | int |

Resurser kan anges på en [MLInstance](./mlinstances.md) som antingen (A) enskilda utbildnings- eller poängparametrar, eller (B) inom ett ytterligare specifikationsobjekt (`specification`). Följande resurskonfigurationer är till exempel desamma för både utbildning och poängsättning:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
