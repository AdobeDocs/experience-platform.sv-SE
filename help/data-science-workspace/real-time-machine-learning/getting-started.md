---
keywords: Experience Platform;utvecklarguide;Data Science Workspace;populära topics;Real time Machine Learning;
solution: Experience Platform
title: Komma igång med maskininlärning i realtid
topic-legacy: Getting started
description: I följande dokument beskrivs de steg som krävs för att skapa en Machine Learning-modell i realtid i Adobe Experience Platform.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Komma igång med maskininlärning i realtid (Alpha)

>[!IMPORTANT]
>
>Maskininlärning i realtid är inte tillgängligt för alla användare ännu. Den här funktionen är alfabet och testas fortfarande. Dokumentet kan komma att ändras.

För att kunna använda maskininlärning i realtid måste du ha tillgång till en organisation som etablerats med Adobe Experience Platform och [!DNL Data Science Workspace]. Dessutom måste ni ha en komplett datauppsättning för användning i utbildning och poängsättning.

Handböckerna för maskininlärning i realtid kräver en fungerande förståelse för Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), datavetenskap och maskininlärning.

**Nyckeltermer:**

- **DSL:** Domänspecifikt språk.
- **Edge:** Datorinlärningstjänsten i realtid kan köras på Edge-kluster som ligger närmare dina aktiveringar och program.
- **Hubb:** Den aktuella alfavärdet kör tjänsten Machine Learning i realtid på Adobe Experience Platform Hub medan Experience Edge Network är under utveckling.
- **Nod:** En nod är den grundläggande enhet som diagrammen är uppbyggda i. Varje nod utför en viss uppgift och kan kopplas ihop med hjälp av länkar för att skapa ett diagram som representerar en XML-pipeline. Uppgiften som utförs av en nod representerar en åtgärd för indata, till exempel en omvandling av data eller schema, eller en maskininlärningskonsekvens. Noden matar ut det omformade eller härledda värdet till nästa nod(er).

## Datauppsättningar i Adobe Experience Platform

Om du vill börja använda maskininlärning i realtid måste du ha tillgång till en datauppsättning. Du kan använda en extern datauppsättning och överföra den till din [!DNL JupyterLab]-miljö eller skapa en ny datauppsättning inom Platform om du inte redan har gjort det.

>[!NOTE]
>
>Om du redan har en datauppsättning som du vill använda kan du hoppa till [Nästa steg](#next-steps).

### Använd en extern datamängd

Om du vill veta mer om hur du använder en extern datauppsättning, till exempel att överföra data till din [!DNL JupyterLab]-miljö, kan du gå till självstudiekursen om hur du analyserar data med anteckningsböcker](../jupyterlab/analyze-your-data.md#external-data).[

### Skapa en ny datauppsättning

Om du vill skapa en ny datauppsättning för användning i maskininlärning i realtid behöver du ett dataschema för din datauppsättning. Därefter måste du importera data med det schema du skapade. Använd följande självstudier för att skapa och fylla i en datauppsättning för [!DNL Platform]:

- [Skapa och fylla i en datauppsättning i API:t](../../catalog/datasets/create.md)
- [Skapa och fylla i en datauppsättning i användargränssnittet](../../ingestion/tutorials/ingest-batch-data.md)

## Nästa steg {#next-steps}

När du har förberett dina data för maskininlärning i realtid börjar du med att följa användarhandboken [Maskinininlärning i realtid](./rtml-authoring-notebook.md) för att lära dig hur du skapar och överför en ONNX-modell till maskininlärningsmodellagringsplatsen i realtid.
