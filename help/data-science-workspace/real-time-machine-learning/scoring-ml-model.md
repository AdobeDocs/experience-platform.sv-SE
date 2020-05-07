---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Posta en maskininlärningsmodell i realtid
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Posta en maskininlärningsmodell i realtid

>[!IMPORTANT]
>Maskininlärning i realtid är inte tillgängligt för alla användare ännu. Den här funktionen är alfabet och testas fortfarande. Dokumentet kan komma att ändras.

I den här självstudiekursen får du lära dig hur du använder Machine Learning-noder i realtid för att bearbeta inkommande data och poängsätta dem mot din ONNX-modell.

>[!IMPORTANT]
> - Funktioner som används i noder kan inte serialiseras. En lambda-funktion används till exempel i en pandod.
> - Det finns ett viloläge på 60 sekunder efter att edge-distributionen har utförts manuellt. Detta kan överföras till metoden score_edge för EdgeUtils.


>[!NOTE]
>För att kunna göra en modell för användning i maskininlärning i realtid måste du ha slutfört den tidigare självstudiekursen om att [utbilda en modell för maskininlärning i realtid](./training-ml-model.md)

## Skapa en ny anteckningsbok

I användargränssnittet för Adobe Experience Platform väljer du **[!UICONTROL Notebooks]** inom *datavetenskap*. Välj sedan **[!UICONTROL JupyterLab]** och tillåt lite tid för att läsa in miljön.

![öppna JupyterLab](../images/rtml/open-jupyterlab.png)

Börja med att välja den **tomma bärbara Python 3-datorn** inifrån JupyterLab-startprogrammet.

![blank python](../images/rtml/python-blank.png)

## Importera och identifiera noder

Börja med att importera alla nödvändiga paket för modellen. Kontrollera att alla paket som du tänker använda för nodredigering importeras.

>[!NOTE]
>Listan över importer kan variera beroende på vilken modell du har skapat.

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

Om du vill visa en lista över tillgängliga noder kopierar och klistrar du in följande exempel i anteckningsboken.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

Svaret är en lista med noder.

![lista med anteckningar](../images/rtml/node-list.png)

## Nodredigering för kantpoäng

Därefter måste du definiera och skapa en nod för kantpoängning. Ersätt `model_id` i exemplet med det modell-ID som du fick när du slutförde kursen i den [tidigare självstudiekursen](./training-ml-model.md). I det här exemplet används Pandanoden för att importera en pd.DataDrame-metod eller allmänna pandor-funktioner på den översta nivån. Kartfunktionen importeras och används för att skapa två noder. Mer information om tillgängliga noder och hur du använder dem finns i [nodreferensguiden](./node-reference.md).

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## Bygg diagram-DSL

När dina noder har skapats är nästa steg att kedja ihop noderna för att skapa ett diagram.

Börja med att lista alla noder som är en del av diagrammet.

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

Koppla sedan noderna med kanter. Varje tuppel är en kantanslutning.

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

Skapa diagrammet när noderna är anslutna.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## Publicera i kant

Nu när du har skapat ett diagram kan du distribuera diagrammet till kanten.

>[!IMPORTANT]
>Publicera inte i kanterna ofta, vilket kan överbelasta kantnoderna. Du bör inte publicera samma modell flera gånger.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## Edge Client

Efter publicering till edge utförs poängsättningen genom en POST-begäran från en klient. Vanligtvis kan detta göras från ett klientprogram som behöver ML-poäng. Du kan också göra det från Postman. Här används EdgeUtils för att demonstrera processen.

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

När poängsättningen är klar returneras edge-URL:en, nyttolasten och resultatet från kanten.

![poängsättning-slutförd](../images/rtml/scoring-complete.png)

## Ta bort en distribuerad app från edge (valfritt)

>!![CAUTION]
Den här cellen används för att ta bort ditt distribuerade edge-program. Använd inte följande cell om du inte behöver ta bort ett distribuerat edge-program.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Nästa steg

Genom att följa självstudiekursen ovan har du lyckats betygsätta och driftsätta din maskininlärningsmodell i realtid. Om du vill veta mer om de noder som är tillgängliga för modellredigering kan du gå till [nodreferensguiden](./node-reference.md).



