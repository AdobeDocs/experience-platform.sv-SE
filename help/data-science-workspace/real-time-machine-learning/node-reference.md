---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real-time Machine Learning;node reference;
solution: Experience Platform
title: Referenshandbok för Machine Learning-noder i realtid
topic: Nodes reference
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---


# Referenshandbok för Machine Learning-noder i realtid (alfa)

>[!IMPORTANT]
>
>Maskininlärning i realtid är inte tillgängligt för alla användare ännu. Den här funktionen är alfabet och testas fortfarande. Dokumentet kan komma att ändras.

En nod är den grundläggande enhet som diagrammen är uppbyggda i. Varje nod utför en viss uppgift och kan kopplas ihop med hjälp av länkar för att skapa ett diagram som representerar en XML-pipeline. Uppgiften som utförs av en nod representerar en åtgärd för indata, till exempel en omvandling av data eller schema, eller en maskininlärningskonsekvens. Noden matar ut det omformade eller härledda värdet till nästa nod(er).

Följande guide visar vilka nodbibliotek som stöds för maskininlärning i realtid.

## Identifiera noder som ska användas i din ML-pipeline

Kopiera följande kod till en anteckningsbok för att visa alla noder som är tillgängliga för användning. [!DNL Python]

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Exempel på svar**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## Standardnoder

Standardnoder bygger på bibliotek för datavetenskap med öppen källkod som Pandor och ScikitLearn.

### ModelUpload

ModelUpload-noden är en intern Adobe-nod som tar en model_path och överför modellen från den lokala modellsökvägen till Machine Learning-blobbutiken i realtid.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode är en intern Adobe-nod som tar ett modell-ID för att hämta den förtränade ONNX-modellen och använda den för att göra poäng på inkommande data.

>[!TIP]
>
>Ange kolumnerna i samma ordning som du vill att data ska skickas till ONNX-modellen.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandor {#pandas}

Med följande Pandarod kan du importera alla `pd.DataFrame` metoder och alla allmänna pandarfunktioner på den översta nivån. Mer information om Pandas metoder finns i dokumentationen [om](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)Pandos-metoder. Mer information om funktioner på den översta nivån finns i [Pandas API-referenshandbok för allmänna funktioner](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

Noden nedan använder `"import": "map"` för att importera metodnamnet som en sträng i parametrarna, följt av att parametrarna anges som en mappningsfunktion. Exemplet nedan gör detta med `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. När kartan är på plats kan du ange `inplace` som `True` eller `False`. Ange `inplace` som `True` eller `False` baserat på om du vill använda omformningen eller inte. Som standard `"inplace": False` skapas en ny kolumn. Stöd för att ange ett nytt kolumnnamn ställs in för att läggas till i en senare version. Den sista raden `cols` kan vara ett kolumnnamn eller en lista med kolumner. Ange kolumnerna som du vill använda omformningen på. I det här exemplet `device` anges.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

Med noden ScikitLearn kan du importera alla ScikitLearn ML-modeller eller -skalförändrare. Använd tabellen nedan om du vill ha mer information om något av värdena som används i exemplet:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Värde | Beskrivning |
| --- | --- |
| funktioner | Indatafunktioner för modellen (lista med strängar). <br> Till exempel: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Målkolumnnamn (sträng). |
| läge | Tåg/test (sträng). |
| model_path | Sökväg till modellen Spara lokalt i ett format som inte är större än ett. |
| params.model | Absolut importsökväg till modellen (sträng), t.ex.: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Modellhyperparametrar finns i dokumentationen för [sklearn API (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) . |
| node_instance.process(data_message_from_previous_node) | Metoden `process()` tar DataMsg från föregående nod och tillämpar omformning. Detta beror på vilken nod som används. |

### Dela

Använd följande nod för att dela upp din databildruta i tåg och testa genom att passera `train_size` eller `test_size`. Detta returnerar en databildruta med ett multiindex. Du kan komma åt tågs- och testdataramar med följande exempel `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Nästa steg

Nästa steg är att skapa noder som kan användas för att betygsätta en Machine Learning-modell i realtid. Mer information finns i användarhandboken för [maskininlärning i realtid](./rtml-authoring-notebook.md).
