---
keywords: Experience Platform;förhandsgranska schemadata;Data Science Workspace;populära ämnen
solution: Experience Platform
title: Förhandsgranska schema och datauppsättning för butiksförsäljning
topic: tutorial
type: Tutorial
description: I följande dokument visas förhandsvisningar av scheman och datauppsättningar på Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Förhandsgranska försäljningsschema och datauppsättning för återförsäljning

När bootstrap-skriptet från [Skapa försäljningsschema och datauppsättning](./create-retails-sales-dataset.md)-självstudiekursen har slutförts. Utdatamodeller och datauppsättningar kan visas på [!DNL Experience Platform]. Följ stegen nedan för att visa scheman och datauppsättningar:

1. Klicka på länken **[!UICONTROL Schemas]** som finns i den vänstra navigeringskolumnen och sök efter det inmatningsschema som har skapats av bootstrap-skriptet. Schemats namn motsvarar det som definierades i `config.yaml` från föregående steg. Visa schemainformationen och dess komposition genom att klicka på den.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Klicka på länken **[!UICONTROL Datasets]** i den vänstra navigeringskolumnen och öppna den indatauppsättning som skapades genom att klicka på namnet på listan. Namnet på datauppsättningen motsvarar det som definierades i `config.yaml` från föregående steg.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Klicka på **[!UICONTROL Preview Dataset]** längst upp till höger för att förhandsgranska en delmängd av datauppsättningen.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Nästa steg

Du har nu importerat exempeldata för butiksförsäljning till [!DNL Experience Platform] med det angivna bootstrap-skriptet.

Så här fortsätter du att arbeta med inkapslade data:
- [Analysera dina data med Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Använd Jupyter-anteckningsböcker i [!DNL Data Science Workspace] för att få tillgång till, utforska, visualisera och förstå dina data.
- [Paketera källfiler i en mottagare](./package-source-files-recipe.md)
   - Följ den här självstudiekursen för att lära dig hur du kan ta med din egen modell till [!DNL Data Science Workspace] genom att paketera källfiler i en importerbar Recipe-fil.