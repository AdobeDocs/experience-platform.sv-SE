---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Komma igång med maskininlärning i realtid
topic: Getting started
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Komma igång med maskininlärning i realtid (Alpha)

>[!IMPORTANT]
>
>Maskininlärning i realtid är inte tillgängligt för alla användare ännu. Den här funktionen är alfabet och testas fortfarande. Dokumentet kan komma att ändras.

För att kunna använda maskininlärning i realtid måste du ha tillgång till en organisation som har etablerats hos Adobe Experience Platform och [!DNL Data Science Workspace]. Dessutom måste ni ha en komplett datauppsättning för användning i utbildning och poängsättning.

Handböckerna för maskininlärning i realtid kräver en fungerande förståelse för Python 3, [Jupyters bärbara](../jupyterlab/overview.md)datorer, datavetenskap och maskininlärning.

**Nyckeltermer:**

- **DSL:** Domänspecifikt språk.
- **Kant:** Machine Learning-betygstjänsten i realtid kan köras på Edge-kluster som ligger närmare dina aktiveringar och program.
- **Hubb:** Den nuvarande alfavärdet kör tjänsten Machine Learning i realtid på Adobe Experience Platform Hub medan Experience Edge Network är under utveckling.
- **Nod:** En nod är den grundläggande enhet som diagrammen är uppbyggda i. Varje nod utför en viss uppgift och kan kopplas ihop med hjälp av länkar för att skapa ett diagram som representerar en XML-pipeline. Uppgiften som utförs av en nod representerar en åtgärd för indata, till exempel en omvandling av data eller schema, eller en maskininlärningskonsekvens. Noden matar ut det omformade eller härledda värdet till nästa nod(er).

## Datauppsättningar i Adobe Experience Platform

Om du vill börja använda maskininlärning i realtid måste du ha tillgång till en datauppsättning. Du kan välja att använda en extern datauppsättning och överföra den till din [!DNL JupyterLab] miljö eller skapa en ny datauppsättning inom plattformen om du inte redan har gjort det.

>[!NOTE]
>
>Om du redan har en datauppsättning som du vill använda kan du hoppa till [nästa steg](#next-steps).

### Använd en extern datamängd

Om du vill veta mer om hur du använder en extern datauppsättning, som att överföra data till din [!DNL JupyterLab] miljö, kan du gå till självstudiekursen om hur du [analyserar data med bärbara datorer](../jupyterlab/analyze-your-data.md#external-data).

### Skapa en ny datauppsättning

Om du vill skapa en ny datauppsättning för användning i maskininlärning i realtid behöver du ett dataschema för din datauppsättning. Därefter måste du importera data med det schema du skapade. Använd följande självstudiekurser för att skapa och fylla i en datauppsättning för [!DNL Platform]:

- [Skapa och fylla i en datauppsättning i API:t](../../catalog/datasets/create.md)
- [Skapa och fylla i en datauppsättning i användargränssnittet](../../ingestion/tutorials/ingest-batch-data.md)

## Nästa steg {#next-steps}

När du har förberett dina data för maskininlärning i realtid börjar du med att följa användarhandboken [för maskininlärning i](./rtml-authoring-notebook.md) realtid för att lära dig hur du skapar och överför en ONNX-modell till maskininlärningsmodellagringsplatsen i realtid.

