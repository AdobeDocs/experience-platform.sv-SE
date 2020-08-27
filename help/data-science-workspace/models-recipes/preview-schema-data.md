---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: Förhandsgranska scheman och datauppsättningar
topic: Tutorial
description: I följande dokument visas förhandsvisningar av scheman och datauppsättningar på Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Förhandsgranska scheman och datauppsättningar

När bootstrap-skriptet har slutförts från självstudiekursen [Skapa försäljningsschema och datauppsättning](./create-retails-sales-dataset.md) (butik). Utdatamodeller och datauppsättningar kan visas på [!DNL Experience Platform]. Följ stegen nedan för att visa scheman och datauppsättningar:

1. Klicka på den **[!UICONTROL Schemas]** länk som finns i den vänstra navigeringskolumnen och sök efter det inmatningsschema som har skapats av bootstrap-skriptet. Schemats namn motsvarar det som definierades i `config.yaml` föregående steg. Visa schemainformationen och dess komposition genom att klicka på den.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Klicka på **[!UICONTROL Datasets]** länken i den vänstra navigeringskolumnen och öppna den indatauppsättning som skapades genom att klicka på namnet på listan. Namnet på datauppsättningen motsvarar det som definierades i `config.yaml` föregående steg.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Klicka på **[!UICONTROL Preview Dataset]** en deluppsättning av datauppsättningen längst upp till höger.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Nästa steg

Du har nu importerat exempeldata för butiksförsäljning till [!DNL Experience Platform] med det angivna bootstrap-skriptet.

Så här fortsätter du att arbeta med inkapslade data:
- [Analysera dina data med Jupyter-anteckningsböcker](../jupyterlab/analyze-your-data.md)
   - Använd Jupyter-anteckningsböcker i [!DNL Data Science Workspace] för att få tillgång till, utforska, visualisera och förstå dina data.
- [Paketera källfiler i en mottagare](./package-source-files-recipe.md)
   - Följ den här självstudiekursen för att lära dig hur du tar in en egen modell [!DNL Data Science Workspace] genom att paketera källfiler i en importerbar Recipe-fil.