---
keywords: Experience Platform;utvecklarguide;endpoint;Data Science Workspace;populära ämnen;
solution: Experience Platform
title: Sensei Machine Learning API Guide
description: I följande avsnitt finns referensinformation för olika funktioner i Sensei Machine Learning API.
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# API-guide för [!DNL Sensei Machine Learning]

I följande avsnitt finns referensinformation för olika funktioner i API:t [!DNL Sensei Machine Learning].

## Frågeparametrar för hämtning av resurser {#query}

API:t [!DNL Sensei Machine Learning] har stöd för frågeparametrar när resurser hämtas. Tillgängliga frågeparametrar och deras användning beskrivs i följande tabell:

| Frågeparameter | Beskrivning | Standardvärde |
| --------------- | ----------- | ------- |
| `start` | Anger startindex för sidnumrering. | `start=0` |
| `limit` | Anger det maximala antalet resultat som ska returneras. | `limit=25` |
| `orderby` | Anger de egenskaper som ska användas för sortering i prioritetsordning. Inkludera ett bindestreck (**-**) före ett egenskapsnamn som ska sorteras i fallande ordning, annars sorteras resultaten i stigande ordning. | `orderby=created` |
| `property` | Anger det jämförelseuttryck som ett objekt måste uppfylla för att kunna returneras. | `property=deleted==false` |

>[!NOTE]
>
>När flera frågeparametrar kombineras måste de avgränsas med et-tecken (**&amp;**).

## Python CPU- och GPU-konfigurationer {#cpu-gpu-config}

Python Engines kan välja mellan en CPU eller en GPU för sin utbildning eller poängsättning och definieras på en [MLInstance](./mlinstances.md) som en aktivitetsspecifikation (`tasks.specification`).

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
>Värdena för `cpus` och `gpus` anger inte antalet CPU:er eller GPU:er, utan antalet fysiska datorer. Dessa värden är tillåtna `"1"` och kommer i annat fall att generera ett undantag.

## Resurskonfigurationer för PySpark och Spark {#resource-config}

Spark Engines har möjlighet att modifiera beräkningsresurser för utbildning och poängsättning. Dessa resurser beskrivs i följande tabell:

| Resurs | Beskrivning | Typ |
| -------- | ----------- | ---- |
| driverMemory | Minne för drivrutin i MB | int |
| driverCores | Antal kärnor som används av drivrutinen | int |
| exutorMemory | Minne för körare i MB | int |
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
