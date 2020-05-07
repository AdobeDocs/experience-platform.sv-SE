---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Komma igång med maskininlärning i realtid
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# Komma igång med maskininlärning i realtid

>[!IMPORTANT]
>Maskininlärning i realtid är inte tillgängligt för alla användare ännu. Den här funktionen är alfabet och testas fortfarande. Dokumentet kan komma att ändras.

För att kunna använda maskininlärning i realtid måste ni ha tillgång till en organisation som har etablerats med Adobe Experience Platform och Data Science Workspace. Dessutom måste du ha en datauppsättning i Platform.

Handböckerna för maskininlärning i realtid kräver en fungerande förståelse för Python 3, [Jupyters bärbara](../jupyterlab/overview.md)datorer, datavetenskap och maskininlärning.

## Datauppsättningar i Adobe Experience Platform

Om du vill börja använda maskininlärning i realtid måste du ha en ifylld datauppsättning i Experience Platform. Du kan använda en extern datauppsättning och överföra den till JupyterLab-miljön eller skapa en ny datauppsättning i Platform om du inte redan har gjort det.

>[!NOTE]
>Om du redan har en datauppsättning som du vill använda kan du hoppa över följande två steg.

### Använd en extern datamängd

Om du vill veta mer om hur du använder en extern datauppsättning, som att överföra data till JupyterLab-miljön, kan du gå till självstudiekursen om hur du [analyserar data med bärbara datorer](../jupyterlab/analyze-your-data.md#external-data).

### Skapa en ny datauppsättning

Om du vill skapa en ny datauppsättning för användning i maskininlärning i realtid behöver du ett dataschema för din datauppsättning. Därefter måste du importera data med det schema du skapade. Använd följande självstudiekurser för att skapa och fylla i en datauppsättning för Platform:

- [Skapa och fylla i en datauppsättning i API:t](../../catalog/datasets/create.md)
- [Skapa och fylla i en datauppsättning i användargränssnittet](../../ingestion/tutorials/ingest-batch-data.md)

## Git och Docker

Om du planerar att utbilda en modell med arbetsflödet Data Science Workplace krävs Git och Docker.

>[!NOTE]
>Du behöver inte ladda ned Git och Docker om du planerar att utbilda en modell med en Python-bärbar dator eller om du använder en egen ONNX-modell.

- [Installationsguide för Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Installationshandbok för Docker](https://docs.docker.com/get-docker/)

## Nästa steg

När du har förberett dina data för maskininlärning i realtid börjar du med att följa självstudiekursen om [utbildning av en modell](./training-ml-model.md) för att lära dig hur du skapar och överför en ONNX-modell till maskininlärningsmodellagringsplatsen i realtid.

