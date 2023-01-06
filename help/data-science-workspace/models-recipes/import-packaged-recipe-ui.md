---
keywords: Experience Platform;importera paketerat recept;Data Science Workspace;populära topics;recipes;ui;create engine
solution: Experience Platform
title: Importera en paketerad mottagare i gränssnittet för datavetenskapen
type: Tutorial
description: I den här självstudiekursen får du information om hur du konfigurerar och importerar ett paketerat recept med hjälp av det angivna exemplet på detaljhandelsförsäljning. I slutet av den här självstudiekursen kan du skapa, utbilda och utvärdera en modell i Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 0%

---

# Importera ett paketerat recept i användargränssnittet för datavetenskapen

I den här självstudiekursen får du information om hur du konfigurerar och importerar ett paketerat recept med hjälp av det angivna exemplet på detaljhandelsförsäljning. I slutet av den här självstudiekursen är du redo att skapa, utbilda och utvärdera en modell i Adobe Experience Platform [!DNL Data Science Workspace].

## Förutsättningar

Den här självstudiekursen kräver ett paketerat recept i form av en Docker-bild-URL. Se självstudiekursen om hur du [Paketera källfiler i en mottagare](./package-source-files-recipe.md) för mer information.

## Arbetsflöde för användargränssnitt

Importera ett paketerat recept till [!DNL Data Science Workspace] kräver specifika receptkonfigurationer, som kompileras till en enda JSON-fil (JavaScript Object Notation). Den här kompileringen av receptkonfigurationer kallas konfigurationsfilen. Ett paketerat recept med en viss uppsättning konfigurationer kallas en recept-instans. Ett recept kan användas för att skapa många receptinstanser i [!DNL Data Science Workspace].

Arbetsflödet för att importera ett paketrecept består av följande steg:
- [Konfigurera ett recept](#configure)
- [Importera Docker-baserat recept - Python](#python)
- [Importera Docker-baserat recept - R](#r)
- [Importera Docker-baserat recept - PySpark](#pyspark)
- [Importera Docker-baserat recept - Scala](#scala)

### Konfigurera ett recept {#configure}

Alla recept-instanser i [!DNL Data Science Workspace] åtföljs av en uppsättning konfigurationer som skräddarsyr recept-instansen så att den passar ett visst användningsfall. Konfigurationsfiler definierar standardutbildnings- och bedömningsbeteenden för en modell som skapas med den här recept-instansen.

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
| `tenantId` | Sträng | Detta ID garanterar att de resurser du skapar namnges korrekt och finns i IMS-organisationen. [Följ stegen här](../../xdm/api/getting-started.md#know-your-tenant_id) för att hitta ditt klientorganisations-ID. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Sträng | Det indatarema som används för utbildning av en modell. Lämna detta tomt när du importerar i användargränssnittet, ersätt med utbildningsschemat-ID när du importerar med API. |
| `evaluation.labelColumn` | Sträng | Kolumnetikett för utvärderingsvisualiseringar. |
| `evaluation.metrics` | Sträng | Kommaavgränsad lista med mätvärden som ska användas för att utvärdera en modell. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Sträng | Utdatamodeller som används för att klassificera en modell. Lämna detta tomt när du importerar i användargränssnittet, ersätt med betygsschemat-ID när du importerar med API. |

I den här självstudiekursen kan du lämna standardkonfigurationsfilerna för butikssäljare i [!DNL Data Science Workspace] Se hur de är.

### Importera Docker-baserat recept - [!DNL Python] {#python}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet av [!DNL Platform] Gränssnitt. Nästa, välj **Importera recept** och markera **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

The **Konfigurera** sidan för **Importera recept** arbetsflödet visas. Ange ett namn och en beskrivning för receptet och välj sedan **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I [Paketera källfiler i en mottagare](./package-source-files-recipe.md) Självstudiekursen innehöll en Docker URL när köpreceptet för butik byggdes med Pythons källfiler.

När du är på **Välj källa** sida, klistra in den Docker-URL som motsvarar det paketerade receptet som skapats med [!DNL Python] källfiler i **[!UICONTROL Source URL]** fält. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd filsystemet **Webbläsare**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Välj **[!UICONTROL Python]** i **Körning** nedrullningsbar och **[!UICONTROL Classification]** i **Typ** nedrullningsbar meny. När allt är ifyllt väljer du **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta till **Hantera scheman**.

>[!NOTE]
>
> Typstöd **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Om modellen inte faller under någon av dessa typer väljer du **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Välj sedan in- och utdatamodeller (butik) under avsnittet **Hantera scheman** skapades de med det angivna bootstrap-skriptet i [skapa försäljningsschema och datauppsättning för återförsäljning](../models-recipes/create-retails-sales-dataset.md) självstudiekurs.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under **Funktionshantering** väljer du i din klientidentitet i schemavisaren för att expandera indatabasschemat för butiksförsäljning. Välj in- och utdatafunktioner genom att markera den önskade funktionen och välja antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** till höger **[!UICONTROL Field Properties]** -fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som  **[!UICONTROL Target Feature]** och allt annat **[!UICONTROL Input Feature]**. Välj **[!UICONTROL Next]** för att granska ditt nya konfigurerade recept.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Välj **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nyligen skapade recept för butiksförsäljning.

### Importera Docker-baserat recept - R {#r}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet av [!DNL Platform] Gränssnitt. Nästa, välj **Importera recept** och markera **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

The **Konfigurera** sidan för **Importera recept** arbetsflödet visas. Ange ett namn och en beskrivning för receptet och välj sedan **[!UICONTROL Next]** i det övre högra hörnet.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I [Paketera källfiler i en mottagare](./package-source-files-recipe.md) självstudiekursen tillhandahölls en Docker URL när köpreceptet för butik byggdes med R-källfiler.

När du är på **Välj källa** klistra in den Docker-URL som motsvarar det paketerade receptet som skapats med R-källfiler i **[!UICONTROL Source URL]** fält. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd filsystemet **Webbläsare**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Välj **[!UICONTROL R]** i **Körning** nedrullningsbar och **[!UICONTROL Classification]** i **Typ** nedrullningsbar meny. När allt är ifyllt väljer du **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta till **Hantera scheman**.

>[!NOTE]
>
> *Typ* supports **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Om modellen inte faller under någon av dessa typer väljer du **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Välj sedan in- och utdatamodeller (butik) under avsnittet **Hantera scheman** skapades de med det angivna bootstrap-skriptet i [skapa försäljningsschema och datauppsättning för återförsäljning](../models-recipes/create-retails-sales-dataset.md) självstudiekurs.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Under *Funktionshantering* väljer du i din klientidentitet i schemavisaren för att expandera indatabasschemat för butiksförsäljning. Välj in- och utdatafunktioner genom att markera den önskade funktionen och välja antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** till höger **[!UICONTROL Field Properties]** -fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som  **[!UICONTROL Target Feature]** och allt annat **[!UICONTROL Input Feature]**. Välj **[!UICONTROL Next]** för att granska ditt nya konfigurerade recept.

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Välj **Slutför** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nyligen skapade recept för butiksförsäljning.

### Importera Docker-baserat recept - PySpark {#pyspark}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet av [!DNL Platform] Gränssnitt. Nästa, välj **Importera recept** och markera **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

The **Konfigurera** sidan för **Importera recept** arbetsflödet visas. Ange ett namn och en beskrivning för receptet och välj sedan **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I [Paketera källfiler i en mottagare](./package-source-files-recipe.md) självstudiekursen innehöll en Docker URL när köpreceptet för butik byggdes med hjälp av PySpark-källfiler.

När du är på **Välj källa** klistra in den Docker-URL som motsvarar det paketerade receptet som skapats med PySpark-källfiler i **[!UICONTROL Source URL]** fält. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd filsystemet **Webbläsare**. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Välj **[!UICONTROL PySpark]** i **Körning** nedrullningsbar meny. När PySpark-miljön har valts fylls standardartefakten automatiskt i till **[!UICONTROL Docker]**. Nästa, välj **[!UICONTROL Classification]** i **Typ** nedrullningsbar meny. När allt är ifyllt väljer du **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta till **Hantera scheman**.

>[!NOTE]
>
> *Typ* supports **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Om modellen inte faller under någon av dessa typer väljer du **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Välj sedan in- och utdatamodeller (butik) med hjälp av **Hantera scheman** väljaren, skapades scheman med hjälp av det angivna bootstrap-skriptet i [skapa försäljningsschema och datauppsättning för återförsäljning](../models-recipes/create-retails-sales-dataset.md) självstudiekurs.

![hantera scheman](../images/models-recipes/import-package-ui/manage-schemas.png)

Under **Funktionshantering** väljer du i din klientidentitet i schemavisaren för att expandera indatabasschemat för butiksförsäljning. Välj in- och utdatafunktioner genom att markera den önskade funktionen och välja antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** till höger **[!UICONTROL Field Properties]** -fönstret. I den här självstudiekursen anger du **[!UICONTROL weeklySales]** som  **[!UICONTROL Target Feature]** och allt annat **[!UICONTROL Input Feature]**. Välj **[!UICONTROL Next]** för att granska ditt nya konfigurerade recept.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Välj **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nyligen skapade recept för butiksförsäljning.

### Importera Docker-baserat recept - Scala {#scala}

Börja med att navigera och välja **[!UICONTROL Workflows]** i det övre vänstra hörnet av [!DNL Platform] Gränssnitt. Nästa, välj **Importera recept** och markera **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

The **Konfigurera** sidan för **Importera recept** arbetsflödet visas. Ange ett namn och en beskrivning för receptet och välj sedan **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![konfigurera arbetsflöde](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> I [Paketera källfiler i en mottagare](./package-source-files-recipe.md) självstudiekursen tillhandahölls en Docker URL när butikssäljreceptet byggdes med Scala ([!DNL Spark]) källfiler.

När du är på **Välj källa** klistrar du in den Docker-URL som motsvarar det paketerade receptet som skapats med källfiler från Scala i fältet Källadress. Importera sedan den angivna konfigurationsfilen genom att dra och släppa eller använd filläsaren. Den angivna konfigurationsfilen finns på `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Välj **[!UICONTROL Spark]** i **Körning** nedrullningsbar meny. När [!DNL Spark] runtime är vald som standardartefakt fylls automatiskt i till **[!UICONTROL Docker]**. Nästa, välj **[!UICONTROL Regression]** från **Typ** nedrullningsbar meny. När allt är ifyllt väljer du **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta till **Hantera scheman**.

>[!NOTE]
>
> Typstöd **[!UICONTROL Classification]** och **[!UICONTROL Regression]**. Om modellen inte faller under någon av dessa typer väljer du **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Välj sedan in- och utdatamodeller (butik) med hjälp av **Hantera scheman** väljaren, skapades scheman med hjälp av det angivna bootstrap-skriptet i [skapa försäljningsschema och datauppsättning för återförsäljning](../models-recipes/create-retails-sales-dataset.md) självstudiekurs.

![hantera scheman](../images/models-recipes/import-package-ui/manage-schemas.png)

Under **Funktionshantering** väljer du i din klientidentitet i schemavisaren för att expandera indatabasschemat för butiksförsäljning. Välj in- och utdatafunktioner genom att markera den önskade funktionen och välja antingen **[!UICONTROL Input Feature]** eller **[!UICONTROL Target Feature]** till höger **[!UICONTROL Field Properties]** -fönstret. I den här självstudiekursen ställer du in &quot;[!UICONTROL weeklySales]&quot; som  **[!UICONTROL Target Feature]** och allt annat **[!UICONTROL Input Feature]**. Välj **[!UICONTROL Next]** för att granska ditt nya konfigurerade recept.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Granska recept, lägg till, ändra eller ta bort konfigurationer efter behov. Välj **[!UICONTROL Finish]** för att skapa receptet.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Gå till [nästa steg](#next-steps) för att ta reda på hur du skapar en modell i [!DNL Data Science Workspace] med hjälp av det nyligen skapade recept för butiksförsäljning.

## Nästa steg {#next-steps}

I den här självstudiekursen finns information om hur du konfigurerar och importerar ett recept till [!DNL Data Science Workspace]. Nu kan du skapa, utbilda och utvärdera en modell med hjälp av det nya receptet.

- [Utbildning och utvärdering av en modell i användargränssnittet](./train-evaluate-model-ui.md)
- [Utbilda och utvärdera en modell med API:t](./train-evaluate-model-api.md)
