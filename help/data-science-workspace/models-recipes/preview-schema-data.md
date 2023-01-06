---
keywords: Experience Platform;förhandsgranska schemadata;Data Science Workspace;populära ämnen
solution: Experience Platform
title: Förhandsgranska schema och datauppsättning för butiksförsäljning
type: Tutorial
description: I följande dokument visas förhandsvisningar av scheman och datauppsättningar på Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Förhandsgranska försäljningsschema och datauppsättning för återförsäljning

När Bootstrap-skriptet från [försäljningsschema och datauppsättning för butik](./create-retails-sales-dataset.md) självstudiekurs. Utdatamodeller och datauppsättningar kan visas på [!DNL Experience Platform]. Följ stegen nedan för att visa scheman och datauppsättningar:

Välj **[!UICONTROL Schemas]** -fliken som finns i den vänstra navigeringen och söker efter det inmatningsschema som har skapats av bootstrap-skriptet. Schemats namn motsvarar det som definierades i `config.yaml` från föregående steg. Visa schemainformationen och dess komposition genom att klicka på den.

![](../images/models-recipes/access-data/schema.PNG)

Välj **[!UICONTROL Datasets]** -fliken som finns i den vänstra navigeringen och öppnar den indatauppsättning som skapades genom att välja namnet på datauppsättningen. Namnet på datauppsättningen motsvarar det som definierades i `config.yaml` från föregående steg.

![](../images/models-recipes/access-data/dataset.PNG)

Välj **[!UICONTROL Preview Dataset]** längst upp till höger för att förhandsgranska en delmängd av datauppsättningen.

![](../images/models-recipes/access-data/preview.PNG)

## Nästa steg

Du har nu importerat exempeldata för butiksförsäljning till [!DNL Experience Platform] med det medföljande bootstrap-skriptet.

Så här fortsätter du att arbeta med inkapslade data:
- [Analysera dina data med Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Använd Jupyter-anteckningsböcker i [!DNL Data Science Workspace] för att få tillgång till, utforska, visualisera och förstå era data.
- [Paketera källfiler i en mottagare](./package-source-files-recipe.md)
   - Följ den här självstudiekursen för att lära dig hur du kan använda din egen modell i [!DNL Data Science Workspace] genom att paketera källfiler i en importerbar Recipe-fil.
