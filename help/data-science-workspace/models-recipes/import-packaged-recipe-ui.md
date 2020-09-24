---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics;recipes;ui;create engine
solution: Experience Platform
title: Importera ett paketerat recept (UI)
topic: tutorial
type: Tutorial
description: I den här självstudiekursen får du information om hur du konfigurerar och importerar ett paketerat recept med hjälp av det angivna exemplet på detaljhandelsförsäljning. I slutet av den här självstudiekursen kan du skapa, utbilda och utvärdera en modell i Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 0%

---


# Importera ett paketerat recept (UI)

I den här självstudiekursen får du information om hur du konfigurerar och importerar ett paketerat recept med hjälp av det angivna exemplet på detaljhandelsförsäljning. I slutet av den här självstudiekursen är du redo att skapa, utbilda och utvärdera en modell i Adobe Experience Platform [!DNL Data Science Workspace].

## Förutsättningar

Den här självstudiekursen kräver ett paketerat recept i form av en Docker-bild-URL. Mer information finns i självstudiekursen om hur du [paketerar källfiler i en Recept](./package-source-files-recipe.md) .

## Arbetsflöde för användargränssnitt

För att importera ett paketerat recept till [!DNL Data Science Workspace] krävs särskilda receptkonfigurationer, som kompileras till en enda JSON-fil (JavaScript Object Notation). Den här kompileringen av receptkonfigurationer kallas **konfigurationsfilen**. Ett paketerat recept med en viss uppsättning konfigurationer kallas en **recept-instans**. Ett recept kan användas för att skapa många receptinstanser i [!DNL Data Science Workspace].

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
| `tenantId` | Sträng | Detta ID garanterar att de resurser du skapar namnges korrekt och finns i IMS-organisationen. [Följ stegen här](../../xdm/api/getting-started.md#know-your-tenant_id) för att hitta ditt klient-ID. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Sträng | Det indatarema som används för utbildning av en modell. Lämna detta tomt när du importerar i användargränssnittet, ersätt med utbildningsschemat-ID när du importerar med API. |
| `evaluation.labelColumn` | Sträng | Kolumnetikett för utvärderingsvisualiseringar. |
| `evaluation.metrics` | Sträng | Kommaavgränsad lista med mätvärden som ska användas för att utvärdera en modell. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Sträng | Utdatamodeller som används för att klassificera en modell. Lämna detta tomt när du importerar i användargränssnittet, ersätt med betygsschemat-ID när du importerar med API. |

I den här självstudiekursen kan du lämna standardkonfigurationsfilerna för butikssäljrecept i [!DNL Data Science Workspace] Referens på samma sätt som de är.

### Importera Docker-baserat recept - [!DNL Python] {#python}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet i [!DNL Platform] användargränssnittet. Välj sedan *Importera recept* och klicka på **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Sidan *Konfigurera* för arbetsflödet *Importera recept* visas. Ange ett namn och en beskrivning för receptet och välj sedan **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I källfilerna för [paketet till en Recept](./package-source-files-recipe.md) -självstudiekurs angavs en Docker-URL när köpreceptet för butik skapades med Python-källfiler.

När du är på *Select source* -sidan klistrar du in den Docker-URL som motsvarar det paketerade receptet som skapats med [!DNL Python] källfilerna i **[!UICONTROL Source URL]** fältet. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd **filläsaren**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Välj **[!UICONTROL Python]** i listrutan *Körtid* och **[!UICONTROL Classification]** i listrutan *Typ* . När allt är ifyllt klickar du **[!UICONTROL Next]** i det övre högra hörnet för att gå vidare till *Hantera scheman*.

>[!NOTE]
>
> *Text* har stöd **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Om modellen inte faller under någon av dessa typer väljer du **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Välj sedan in- och utdatamodeller för detaljhandel under avsnittet *Hantera scheman*, som skapades med det tillhandahållna bootstrap-skriptet i [skapa säljchemat för detaljhandeln och självstudiekursen för datauppsättningar](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicka på din innehavaridentifiering i schemavisaren under avsnittet *Funktionshantering* för att expandera indatabasschemat för butiksförsäljning. Välj in- och utdatafunktioner genom att markera den önskade funktionen och markera antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** i det högra **[!UICONTROL Field Properties]** fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som **[!UICONTROL Target Feature]** och allt annat som **[!UICONTROL Input Feature]**. Klicka **[!UICONTROL Next]** för att granska ditt nya konfigurerade recept.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Klicka **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå vidare till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nyligen skapade recept för butiksförsäljning.

### Importera Docker-baserat recept - R {#r}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet i [!DNL Platform] användargränssnittet. Välj sedan *Importera recept* och klicka på **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Sidan *Konfigurera* för arbetsflödet *Importera recept* visas. Ange ett namn och en beskrivning för receptet och välj sedan **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I källfilerna för [paketet till en Recept](./package-source-files-recipe.md) -självstudiekurs angavs en Docker-URL när köpreceptet för butik skapades med hjälp av R-källfiler.

När du är på *Select source* -sidan klistrar du in den Docker-URL som motsvarar det paketerade recept som skapats med R-källfiler i **[!UICONTROL Source URL]** fältet. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd **filläsaren**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Välj **[!UICONTROL R]** i listrutan *Körtid* och **[!UICONTROL Classification]** i listrutan *Typ* . När allt är ifyllt klickar du **[!UICONTROL Next]** i det övre högra hörnet för att gå vidare till *Hantera scheman*.

>[!NOTE]
>
> *Text* har stöd **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Om modellen inte faller under någon av dessa typer väljer du **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Välj sedan in- och utdatamodeller för detaljhandel under avsnittet *Hantera scheman*, som skapades med det tillhandahållna bootstrap-skriptet i [skapa säljchemat för detaljhandeln och självstudiekursen för datauppsättningar](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicka på din innehavaridentifiering i schemavisaren under avsnittet *Funktionshantering* för att expandera indatabasschemat för butiksförsäljning. Välj in- och utdatafunktioner genom att markera den önskade funktionen och markera antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** i det högra **[!UICONTROL Field Properties]** fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som **[!UICONTROL Target Feature]** och allt annat som **[!UICONTROL Input Feature]**. Klicka **[!UICONTROL Next]** för att granska ditt nya konfigurerade recept.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Klicka på **Slutför** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå vidare till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nyligen skapade recept för butiksförsäljning.

### Importera Docker-baserat recept - PySpark {#pyspark}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet i [!DNL Platform] användargränssnittet. Välj sedan *Importera recept* och klicka på **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Sidan *Konfigurera* för arbetsflödet *Importera recept* visas. Ange ett namn och en beskrivning för receptet och fortsätt sedan genom att välja **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I källfilerna för [paketet till en Recept](./package-source-files-recipe.md) -självstudiekurs angavs en Docker-URL när köpreceptet för butik skapades med hjälp av PySpark-källfiler.

När du är på *Select source* -sidan klistrar du in den Docker-URL som motsvarar det paketerade recept som skapats med PySpark-källfiler i **[!UICONTROL Source URL]** fältet. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd **filläsaren**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Välj **[!UICONTROL PySpark]** i *listrutan* Runtime. När PySpark-miljön har valts fylls standardartefakten automatiskt i till **[!UICONTROL Docker]**. Välj sedan **[!UICONTROL Classification]** i listrutan *Typ* . När allt är ifyllt klickar du **[!UICONTROL Next]** i det övre högra hörnet för att gå vidare till *Hantera scheman*.

>[!NOTE]
>
> *Text* har stöd **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Om modellen inte faller under någon av dessa typer väljer du **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Välj sedan in- och utdatamodeller för detaljhandel under avsnittet *Hantera scheman*, som skapades med det tillhandahållna bootstrap-skriptet i [skapa säljchemat för detaljhandeln och självstudiekursen för datauppsättningar](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicka på din innehavaridentifiering i schemavisaren under avsnittet *Funktionshantering* för att expandera indatabasschemat för butiksförsäljning. Välj in- och utdatafunktioner genom att markera den önskade funktionen och markera antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** i det högra **[!UICONTROL Field Properties]** fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som **[!UICONTROL Target Feature]** och allt annat som **[!UICONTROL Input Feature]**. Klicka **[!UICONTROL Next]** för att granska ditt nya konfigurerade recept.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Klicka **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå vidare till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nyligen skapade recept för butiksförsäljning.

### Importera Docker-baserat recept - Scala {#scala}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet i [!DNL Platform] användargränssnittet. Välj sedan *Importera recept* och klicka på **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Sidan *Konfigurera* för arbetsflödet *Importera recept* visas. Ange ett namn och en beskrivning för receptet och fortsätt sedan genom att välja **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I källfilerna för [paketet till en Recept](./package-source-files-recipe.md) -självstudiekurs angavs en Docker-URL när köpreceptet för butik skapades med hjälp av källfiler från Scala ([!DNL Spark]).

När du är på *Select source* -sidan klistrar du in den Docker-URL som motsvarar det paketerade recept som skapats med Scala-källfiler i fältet *Source URL* (Källadress). Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd **filläsaren**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Välj **[!UICONTROL Spark]** i *listrutan* Runtime. När du har valt [!DNL Spark] runtime-modulen fylls standardartefakten automatiskt i **[!UICONTROL Docker]**. Välj sedan **[!UICONTROL Regression]** i listrutan *Typ* . När allt är ifyllt klickar du **[!UICONTROL Next]** i det övre högra hörnet för att gå vidare till *Hantera scheman*.

>[!NOTE]
>
> *Text* har stöd **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Om modellen inte faller under någon av dessa typer väljer du **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Välj sedan in- och utdatamodeller för detaljhandel under avsnittet *Hantera scheman*, som skapades med det tillhandahållna bootstrap-skriptet i [skapa säljchemat för detaljhandeln och självstudiekursen för datauppsättningar](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Klicka på din innehavaridentifiering i schemavisaren under avsnittet *Funktionshantering* för att expandera indatabasschemat för butiksförsäljning. Välj in- och utdatafunktioner genom att markera den önskade funktionen och markera antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** i det högra **[!UICONTROL Field Properties]** fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som **[!UICONTROL Target Feature]** och allt annat som **[!UICONTROL Input Feature]**. Klicka **[!UICONTROL Next]** för att granska ditt nya konfigurerade recept.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Klicka **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå vidare till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nyligen skapade recept för butiksförsäljning.

## Nästa steg {#next-steps}

I den här självstudiekursen finns information om hur du konfigurerar och importerar ett recept till [!DNL Data Science Workspace]. Nu kan du skapa, utbilda och utvärdera en modell med hjälp av det nya receptet.

- [Utbildning och utvärdering av en modell i användargränssnittet](./train-evaluate-model-ui.md)
- [Utbilda och utvärdera en modell med API:t](./train-evaluate-model-api.md)