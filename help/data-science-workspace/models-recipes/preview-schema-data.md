---
keywords: Experience Platform;förhandsgranska schemadata;Data Science Workspace;populära ämnen
solution: Experience Platform
title: Förhandsgranska schema och datauppsättning för butiksförsäljning
type: Tutorial
description: I följande dokument visas förhandsvisningar av scheman och datauppsättningar på Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Förhandsgranska försäljningsschema och datauppsättning för återförsäljning

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

När bootstrap-skriptet från självstudiekursen [Retail Sales schema and dataset](./create-retails-sales-dataset.md) har slutförts. Utdatamodeller och datauppsättningar kan visas på [!DNL Experience Platform]. Följ stegen nedan för att visa scheman och datauppsättningar:

Välj fliken **[!UICONTROL Schemas]** som finns i den vänstra navigeringen och sök efter det indatabema som har skapats av bootstrap-skriptet. Schemats namn motsvarar det som definierades i `config.yaml` från föregående steg. Visa schemainformationen och dess komposition genom att klicka på den.

![](../images/models-recipes/access-data/schema.PNG)

Välj fliken **[!UICONTROL Datasets]** som finns i den vänstra navigeringen och öppna den indatauppsättning som skapades genom att välja namnet på datauppsättningen. Namnet på datauppsättningen motsvarar det som definierades i `config.yaml` från föregående steg.

![](../images/models-recipes/access-data/dataset.PNG)

Välj **[!UICONTROL Preview Dataset]** längst upp till höger om du vill förhandsgranska en delmängd av datauppsättningen.

![](../images/models-recipes/access-data/preview.PNG)

## Nästa steg

Du har nu importerat exempeldata för butiksförsäljning till [!DNL Experience Platform] med det angivna bootstrap-skriptet.

Så här fortsätter du att arbeta med inkapslade data:
- [Analysera dina data med Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Använd Jupyter-anteckningsböcker i [!DNL Data Science Workspace] för att få tillgång till, utforska, visualisera och förstå dina data.
- [Paketera källfiler i en mottagare](./package-source-files-recipe.md)
   - Följ den här självstudiekursen för att lära dig hur du kan ta med din egen modell till [!DNL Data Science Workspace] genom att paketera källfiler i en importerbar Recipe-fil.
