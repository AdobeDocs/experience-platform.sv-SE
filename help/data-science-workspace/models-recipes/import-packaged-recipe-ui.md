---
keywords: Experience Platform;importera paketerat recept;Data Science Workspace;populära topics;recipes;ui;create engine
solution: Experience Platform
title: Importera en paketerad mottagare i gränssnittet för datavetenskapen
topic: tutorial
type: Tutorial
description: I den här självstudiekursen får du information om hur du konfigurerar och importerar ett paketerat recept med hjälp av det angivna exemplet på detaljhandelsförsäljning. I slutet av den här självstudiekursen kan du skapa, utbilda och utvärdera en modell i Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 0%

---


# Importera ett paketerat recept i användargränssnittet för datavetenskapen

I den här självstudiekursen får du information om hur du konfigurerar och importerar ett paketerat recept med hjälp av det angivna exemplet på detaljhandelsförsäljning. I slutet av den här självstudiekursen kan du skapa, utbilda och utvärdera en modell i Adobe Experience Platform [!DNL Data Science Workspace].

## Förutsättningar

Den här självstudiekursen kräver ett paketerat recept i form av en Docker-bild-URL. Mer information finns i självstudiekursen om hur du [paketerar källfiler i en recept](./package-source-files-recipe.md).

## Arbetsflöde för användargränssnitt

För import av ett paketerat recept till [!DNL Data Science Workspace] krävs specifika receptkonfigurationer, som kompileras till en enda JavaScript-objektnotationsfil (JSON). Den här kompileringen av receptkonfigurationer kallas konfigurationsfilen. Ett paketerat recept med en viss uppsättning konfigurationer kallas en recept-instans. Ett recept kan användas för att skapa många receptinstanser i [!DNL Data Science Workspace].

Arbetsflödet för att importera ett paketrecept består av följande steg:
- [Konfigurera ett recept](#configure)
- [Importera Docker-baserat recept - Python](#python)
- [Importera Docker-baserat recept - R](#r)
- [Importera Docker-baserat recept - PySpark](#pyspark)
- [Importera Docker-baserat recept - Scala](#scala)

### Konfigurera ett recept {#configure}

Varje recept-instans i [!DNL Data Science Workspace] åtföljs av en uppsättning konfigurationer som anpassar recept-instansen så att den passar ett visst användningsfall. Konfigurationsfiler definierar standardutbildnings- och bedömningsbeteenden för en modell som skapas med den här recept-instansen.

>[!NOTE]
>
>Konfigurationsfilerna är recept- och fallspecifika.

Nedan visas ett exempel på en konfigurationsfil som visar standardutbildnings- och bedömningsbeteenden för recept för detaljhandelsförsäljning.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| Parameternyckel | Typ | Beskrivning |
| ----- | ----- | ----- |
| `learning_rate` | Siffra | Skala för övertoningsmultiplikation. |
| `n_estimators` | Siffra | Antal träd i skogen för slumpmässig skogsklassificering. |
| `max_depth` | Siffra | Maximalt djup i ett träd i slumpmässig skogsklassificering. |
| `ACP_DSW_INPUT_FEATURES` | Sträng | Lista med kommaavgränsade inmatningsschemaattribut. |
| `ACP_DSW_TARGET_FEATURES` | Sträng | Lista med kommaseparerade utdataschemaattribut. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolean | Avgör om in- och utdatafunktionerna kan ändras |
| `tenantId` | Sträng | Detta ID garanterar att de resurser du skapar namnges korrekt och finns i IMS-organisationen. [Följ stegen ](../../xdm/api/getting-started.md#know-your-tenant_id) här för att hitta ditt klient-ID. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Sträng | Det indatarema som används för utbildning av en modell. Lämna detta tomt när du importerar i användargränssnittet, ersätt med utbildningsschemat-ID när du importerar med API. |
| `evaluation.labelColumn` | Sträng | Kolumnetikett för utvärderingsvisualiseringar. |
| `evaluation.metrics` | Sträng | Kommaavgränsad lista med mätvärden som ska användas för att utvärdera en modell. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Sträng | Utdatamodeller som används för att klassificera en modell. Lämna detta tomt när du importerar i användargränssnittet, ersätt med betygsschemat-ID när du importerar med API. |

I den här självstudiekursen kan du lämna standardkonfigurationsfilerna för butikssäljrecept i [!DNL Data Science Workspace]-referensen på samma sätt som de är.

### Importera Docker-baserat recept - [!DNL Python] {#python}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet i användargränssnittet för [!DNL Platform]. Välj sedan **Importera recept** och klicka på **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Sidan **Konfigurera** för arbetsflödet **Importera recept** visas. Ange ett namn och en beskrivning för receptet och välj sedan **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I [Paketkällfilerna i en Recipe](./package-source-files-recipe.md)-självstudie angavs en Docker-URL när butikssäljreceptet skapades med Pythons källfiler.

När du är på **Välj källa**-sidan klistrar du in den Docker-URL som motsvarar det paketerade receptet som skapats med [!DNL Python] källfiler i fältet **[!UICONTROL Source URL]**. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd filsystemet **Webbläsare**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Välj **[!UICONTROL Python]** i listrutan **Runtime** och **[!UICONTROL Classification]** i listrutan **Typ**. När allt har fyllts i klickar du på **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta till **Hantera scheman**.

>[!NOTE]
>
> Typen stöder **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Välj **[!UICONTROL Custom]** om modellen inte faller under någon av dessa typer.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Välj sedan in- och utdatamodeller för butiksförsäljning under avsnittet **Hantera scheman**, som skapades med det angivna bootstrap-skriptet i [skapa försäljningsschemat för detaljhandeln och datamängden](../models-recipes/create-retails-sales-dataset.md) självstudiekursen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under **Feature Management**-avsnittet klickar du på din innehavaridentifiering i schemavisaren för att expandera indatabasschemat för butiksförsäljning. Markera in- och utdatafunktionerna genom att markera den önskade funktionen och markera antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** i det högra **[!UICONTROL Field Properties]**-fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som **[!UICONTROL Target Feature]** och allt annat som **[!UICONTROL Input Feature]**. Klicka på **[!UICONTROL Next]** om du vill granska det nya konfigurerade receptet.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Klicka på **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå vidare till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nya försäljningsreceptet.

### Importera Docker-baserat recept - R {#r}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet i användargränssnittet för [!DNL Platform]. Välj sedan **Importera recept** och klicka på **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Sidan **Konfigurera** för arbetsflödet **Importera recept** visas. Ange ett namn och en beskrivning för receptet och välj sedan **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I [Paketkällfilerna i en Recipe](./package-source-files-recipe.md)-självstudie angavs en Docker-URL när försäljningsreceptet för butik skapades med R-källfiler.

När du är på **Välj källa**-sidan klistrar du in den Docker-URL som motsvarar det paketerade recept som skapats med R-källfiler i fältet **[!UICONTROL Source URL]**. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd filsystemet **Webbläsare**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Välj **[!UICONTROL R]** i listrutan **Runtime** och **[!UICONTROL Classification]** i listrutan **Typ**. När allt har fyllts i klickar du på **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta till **Hantera scheman**.

>[!NOTE]
>
> *Typesupports* and  **[!UICONTROL Classification]**  **[!UICONTROL Regression]** and. Välj **[!UICONTROL Custom]** om modellen inte faller under någon av dessa typer.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Välj sedan in- och utdatamodeller för butiksförsäljning under avsnittet **Hantera scheman**, som skapades med det angivna bootstrap-skriptet i [skapa försäljningsschemat för detaljhandeln och datamängden](../models-recipes/create-retails-sales-dataset.md) självstudiekursen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under *Feature Management*-avsnittet klickar du på din innehavaridentifiering i schemavisaren för att expandera indatabasschemat för butiksförsäljning. Markera in- och utdatafunktionerna genom att markera den önskade funktionen och markera antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** i det högra **[!UICONTROL Field Properties]**-fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som **[!UICONTROL Target Feature]** och allt annat som **[!UICONTROL Input Feature]**. Klicka på **[!UICONTROL Next]** om du vill granska det nya konfigurerade receptet.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Klicka på **Slutför** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå vidare till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nya försäljningsreceptet.

### Importera Docker-baserat recept - PySpark {#pyspark}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet i användargränssnittet för [!DNL Platform]. Välj sedan **Importera recept** och klicka på **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Sidan **Konfigurera** för arbetsflödet **Importera recept** visas. Ange ett namn och en beskrivning för receptet och fortsätt sedan genom att välja **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I [Paketkällfilerna i en Recipe](./package-source-files-recipe.md)-självstudie angavs en Docker-URL när köpreceptet för butik skapades med hjälp av PySpark-källfiler.

När du är på **Välj källa**-sidan klistrar du in den Docker-URL som motsvarar det paketerade receptet som skapats med PySpark-källfiler i fältet **[!UICONTROL Source URL]**. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd filsystemet **Webbläsare**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Välj **[!UICONTROL PySpark]** i listrutan **Runtime**. När PySpark-miljön har valts fylls standardartefakten automatiskt i till **[!UICONTROL Docker]**. Välj sedan **[!UICONTROL Classification]** i listrutan **Typ**. När allt har fyllts i klickar du på **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta till **Hantera scheman**.

>[!NOTE]
>
> *Typesupports* and  **[!UICONTROL Classification]**  **[!UICONTROL Regression]** and. Välj **[!UICONTROL Custom]** om modellen inte faller under någon av dessa typer.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Välj sedan in- och utdatamodeller för butiksförsäljning under avsnittet **Hantera scheman**, som skapades med det angivna bootstrap-skriptet i [skapa försäljningsschemat för detaljhandeln och datamängden](../models-recipes/create-retails-sales-dataset.md) självstudiekursen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under **Feature Management**-avsnittet klickar du på din innehavaridentifiering i schemavisaren för att expandera indatabasschemat för butiksförsäljning. Markera in- och utdatafunktionerna genom att markera den önskade funktionen och markera antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** i det högra **[!UICONTROL Field Properties]**-fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som **[!UICONTROL Target Feature]** och allt annat som **[!UICONTROL Input Feature]**. Klicka på **[!UICONTROL Next]** om du vill granska det nya konfigurerade receptet.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Klicka på **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå vidare till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nya försäljningsreceptet.

### Importera Docker-baserat recept - Scala {#scala}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet i användargränssnittet för [!DNL Platform]. Välj sedan **Importera recept** och klicka på **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Sidan **Konfigurera** för arbetsflödet **Importera recept** visas. Ange ett namn och en beskrivning för receptet och fortsätt sedan genom att välja **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I [Paketkällfilerna i en Recipe](./package-source-files-recipe.md)-självstudie angavs en Docker-URL när butikssäljreceptet byggdes med källfiler för Scala ([!DNL Spark]).

När du är på **Välj källa**-sidan klistrar du in den Docker-URL som motsvarar det paketerade recept som skapats med Scala-källfiler i fältet Källadress. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd filläsaren. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Välj **[!UICONTROL Spark]** i listrutan **Runtime**. När du har valt [!DNL Spark]-miljön fylls standardartefakten automatiskt till **[!UICONTROL Docker]**. Välj sedan **[!UICONTROL Regression]** i listrutan **Typ**. När allt har fyllts i klickar du på **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta till **Hantera scheman**.

>[!NOTE]
>
> Typen stöder **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Välj **[!UICONTROL Custom]** om modellen inte faller under någon av dessa typer.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Välj sedan in- och utdatamodeller för butiksförsäljning under avsnittet **Hantera scheman**, som skapades med det angivna bootstrap-skriptet i [skapa försäljningsschemat för detaljhandeln och datamängden](../models-recipes/create-retails-sales-dataset.md) självstudiekursen.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under **Feature Management**-avsnittet klickar du på din innehavaridentifiering i schemavisaren för att expandera indatabasschemat för butiksförsäljning. Markera in- och utdatafunktionerna genom att markera den önskade funktionen och markera antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** i det högra **[!UICONTROL Field Properties]**-fönstret. I den här självstudiekursen anger du [!UICONTROL weeklySales] som **[!UICONTROL Target Feature]** och allt annat som **[!UICONTROL Input Feature]**. Klicka på **[!UICONTROL Next]** om du vill granska det nya konfigurerade receptet.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Klicka på **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå vidare till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nya försäljningsreceptet.

## Nästa steg {#next-steps}

I den här självstudiekursen finns information om hur du konfigurerar och importerar ett recept till [!DNL Data Science Workspace]. Nu kan du skapa, utbilda och utvärdera en modell med hjälp av det nya receptet.

- [Utbildning och utvärdering av en modell i användargränssnittet](./train-evaluate-model-ui.md)
- [Utbilda och utvärdera en modell med API:t](./train-evaluate-model-api.md)