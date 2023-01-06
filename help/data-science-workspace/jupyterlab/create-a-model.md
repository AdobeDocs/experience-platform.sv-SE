---
keywords: Experience Platform;JupyterLab;recept;anteckningsböcker;Data Science Workspace;populära topics;create recept
solution: Experience Platform
title: Skapa en modell med JupyterLab-anteckningsböcker
type: Tutorial
description: I den här självstudiekursen får du hjälp med att skapa ett recept med mallen för receptbyggaren för JupyterLab-anteckningsböcker.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2090'
ht-degree: 0%

---

# Skapa en modell med JupyterLab-anteckningsböcker

I den här självstudiekursen får du hjälp med att skapa en modell med hjälp av mallen för receptbyggaren för JupyterLab-anteckningsböcker.

## Nya koncept:

- **Recept:** Ett recept är en AdobeTerm för en modellspecifikation och är en behållare på den översta nivån som representerar maskininlärning, AI-algoritm eller en kombination av algoritmer, bearbetningslogik och konfiguration som krävs för att skapa och köra en utbildad modell.
- **Modell:** En modell är en instans av ett maskininlärningsrecept som är utbildat med historiska data och konfigurationer för att lösa ett affärsärende.
- **Utbildning:** Utbildning är processen att lära sig mönster och insikter från märkta data.
- **Poäng:** Poängberäkning är processen att generera insikter från data med hjälp av en tränad modell.

## Hämta de resurser som krävs {#assets}

Innan du fortsätter med den här självstudiekursen måste du skapa de scheman och datamängder som behövs. Gå till självstudiekursen för [skapa scheman och datauppsättningar för Luma-benägenhetsmodellen](../models-recipes/create-luma-data.md) för att hämta de nödvändiga resurserna och ställa in kraven.

## Kom igång med [!DNL JupyterLab] anteckningsmiljö

Du kan skapa ett helt nytt recept i [!DNL Data Science Workspace]. Navigera till [Adobe Experience Platform](https://platform.adobe.com) och väljer **[!UICONTROL Notebooks]** till vänster. Om du vill skapa en ny anteckningsbok väljer du mallen för Recipe Builder i dialogrutan [!DNL JupyterLab Launcher].

The [!UICONTROL Recipe Builder] bärbara datorer gör att du kan köra utbildning och poängsättning inuti den bärbara datorn. Detta ger dig flexibilitet att göra ändringar i deras `train()` och `score()` metoder mellan att köra experiment på utbildnings- och poängsättningsdata. När du är nöjd med resultatet av kursen och poängsättningen kan du skapa ett recept och dessutom publicera det som en modell med recept för att modellera funktionaliteten.

>[!NOTE]
>
>The [!UICONTROL Recipe Builder] anteckningsboken stöder arbete med alla filformat, men för närvarande har funktionen för att skapa recept endast stöd för [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

När du väljer [!UICONTROL Recipe Builder] anteckningsboken från startprogrammet öppnas den på en ny flik.

På den nya fliken för anteckningsboken överst laddas ett verktygsfält med ytterligare tre åtgärder - **[!UICONTROL Train]**, **[!UICONTROL Score]** och **[!UICONTROL Create Recipe]**. De här ikonerna visas bara i [!UICONTROL Recipe Builder] anteckningsbok. Mer information om dessa åtgärder finns [i avsnittet om utbildning och poängsättning](#training-and-scoring) när du har skapat en recept i anteckningsboken.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Kom igång med [!UICONTROL Recipe Builder] anteckningsbok

I den angivna resursmappen finns en Luma-benägenhetsmodell `propensity_model.ipynb`. Använd alternativet för överföring av anteckningsbok i JupyterLab för att överföra den angivna modellen och öppna anteckningsboken.

![ladda upp anteckningsbok](../images/jupyterlab/create-recipe/upload_notebook.png)

Den återstående delen av den här självstudiekursen omfattar följande filer som är fördefinierade i bärbara datorer med benägenhetsmodellen:

- [Kravfil](#requirements-file)
- [Konfigurationsfiler](#configuration-files)
- [Utbilda datainläsare](#training-data-loader)
- [Inläsare av poängdata](#scoring-data-loader)
- [Pipeline-fil](#pipeline-file)
- [Utvärderarfil](#evaluator-file)
- [Data Saver-fil](#data-saver-file)

I följande videofilm förklaras den bärbara datorn med Luma-benägenhetsmodellen:

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### Kravfil {#requirements-file}

Kravfilen används för att deklarera ytterligare bibliotek som du vill använda i modellen. Du kan ange versionsnumret om det finns ett beroende. Om du vill söka efter fler bibliotek går du till [anaconda.org](https://anaconda.org). Mer information om hur du formaterar kravfilen finns på [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). Listan med de huvudbibliotek som redan används är:

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Bibliotek eller specifika versioner som du lägger till kan vara inkompatibla med ovanstående bibliotek. Om du väljer att skapa en miljöfil manuellt kan du dessutom `name` får inte åsidosättas.

För bärbara Luma-benägenhetsmodeller behöver kraven inte uppdateras.

### Konfigurationsfiler {#configuration-files}

Konfigurationsfilerna, `training.conf` och `scoring.conf`, används för att ange de datauppsättningar som du vill använda för utbildning och poängsättning samt för att lägga till hyperparametrar. Det finns olika konfigurationer för utbildning och poängsättning.

För att en modell ska kunna genomföra en utbildning måste du ange `trainingDataSetId`, `ACP_DSW_TRAINING_XDM_SCHEMA`och `tenantId`. Om du vill göra en bedömning måste du ange `scoringDataSetId`, `tenantId`och `scoringResultsDataSetId `.

Gå till fliken Data för att hitta data- och schema-ID:n ![Fliken Data](../images/jupyterlab/create-recipe/dataset-tab.png) i anteckningsböcker i det vänstra navigeringsfältet (under mappikonen). Tre olika datauppsättnings-ID måste anges. The `scoringResultsDataSetId` används för att lagra modellbedömningsresultaten och ska vara en tom datamängd. Dessa datauppsättningar gjordes tidigare i [Obligatoriska resurser](#assets) steg.

![](../images/jupyterlab/create-recipe/dataset_tab.png)

Samma information finns på [Adobe Experience Platform](https://platform.adobe.com/) under **[Schema](https://platform.adobe.com/schema)** och **[Datauppsättningar](https://platform.adobe.com/dataset/overview)** -tabbar.

När du är klar bör kursen och poängkonfigurationen se ut ungefär som på följande skärmbild:

![konfiguration](../images/jupyterlab/create-recipe/config.png)

Som standard ställs följande konfigurationsparametrar in åt dig när du utbildar och poängsätter data:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Förstå inläsaren av utbildningsdata {#training-data-loader}

Syftet med inläsaren av utbildningsdata är att instansiera data som används för att skapa maskininlärningsmodellen. Vanligtvis finns det två åtgärder som inläsaren av utbildningsdata utför:

- Läser in data från [!DNL Platform]
- Datagenerering och -teknik

I följande två avsnitt går det längre att läsa in data och förbereda data.

### Läser in data {#loading-data}

Det här steget använder [pandatabilder](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Data kan läsas in från filer i [!DNL Adobe Experience Platform] med antingen [!DNL Platform] SDK (`platform_sdk`) eller från externa källor med pandor `read_csv()` eller `read_json()` funktioner.

- [[!DNL Platform SDK]](#platform-sdk)
- [Externa källor](#external-sources)

>[!NOTE]
>
>I Recipe Builder-anteckningsboken läses data in via `platform_sdk` datainläsare.

### [!DNL Platform] SDK {#platform-sdk}

En djupgående självstudiekurs om hur du använder `platform_sdk` datainläsare, besök [Plattforms-SDK - guide](../authoring/platform-sdk.md). Den här självstudiekursen innehåller information om autentisering av bygge, grundläggande läsning av data och grundläggande skrivande av data.

### Externa källor {#external-sources}

I det här avsnittet visas hur du importerar en JSON- eller CSV-fil till ett pandaobjekt. Officiell dokumentation från pandabiblioteket finns här:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Här följer ett exempel på hur du importerar en CSV-fil. The `data` -argument är sökvägen till CSV-filen. Variabeln importerades från `configProperties` i [föregående avsnitt](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

Du kan även importera från en JSON-fil. The `data` -argument är sökvägen till CSV-filen. Variabeln importerades från `configProperties` i [föregående avsnitt](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Nu finns dina data i dataframe-objektet och kan analyseras och ändras i [nästa avsnitt](#data-preparation-and-feature-engineering).

## Inläsningsfil för utbildningsdata

I det här exemplet läses data in med Platform SDK. Biblioteket kan importeras högst upp på sidan genom att inkludera raden:

`from platform_sdk.dataset_reader import DatasetReader`

Du kan sedan använda `load()` metod för att hämta utbildningsdata från `trainingDataSetId` enligt konfigurationen (`recipe.conf`).

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>Som anges i [Avsnittet Konfigurationsfil](#configuration-files)ställs följande konfigurationsparametrar in åt dig när du får åtkomst till data från Experience Platform med `client_context = get_client_context(config_properties)`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Nu när du har tillgång till dina data kan du börja med dataförberedelser och funktionskonstruktion.

### Datagenerering och -teknik {#data-preparation-and-feature-engineering}

Efter det att data har lästs in måste de rengöras och förberedas. I det här exemplet är målet med modellen att förutsäga om en kund kommer att beställa en produkt eller inte. Eftersom modellen inte tittar på specifika produkter behöver du inte `productListItems` och därför tas kolumnen bort. Därefter tas ytterligare kolumner bort som bara innehåller ett eller två värden i en enda kolumn. När du utbildar en modell är det viktigt att bara behålla användbara data som kan hjälpa dig att förutsäga ditt mål.

![exempel på dataprep](../images/jupyterlab/create-recipe/data_prep.png)

När du har släppt onödiga data kan du börja med funktionskonstruktion. De demodata som används för det här exemplet innehåller ingen sessionsinformation. Normalt vill du ha data om aktuella och tidigare sessioner för en viss kund. På grund av brist på sessionsinformation härmar det här exemplet i stället aktuella och tidigare sessioner via reseavgränsning.

![Reseavgränsning](../images/jupyterlab/create-recipe/journey_demarcation.png)

När avgränsningen är klar får data en etikett och en resa skapas.

![etikettera data](../images/jupyterlab/create-recipe/label_data.png)

Sedan skapas funktionerna och delas upp i tidigare och nuvarande. Eventuella kolumner som inte behövs tas bort, så att du får tillgång till både tidigare och nuvarande resor för Luma-kunder. Dessa resor innehåller information om t.ex. om en kund har köpt en artikel och den resa som de tog fram till köpet.

![aktuell utbildning](../images/jupyterlab/create-recipe/final_journey.png)

## Inläsare av poängdata {#scoring-data-loader}

Förfarandet för att läsa in data för bedömning liknar inläsning av utbildningsdata. Om du tittar närmare på koden ser du att allt är detsamma förutom för `scoringDataSetId` i `dataset_reader`. Detta beror på att samma Luma-datakälla används för både utbildning och poängsättning.

Om du vill använda olika datafiler för utbildning och poängsättning är inläsaren för utbildning och poängsättning separat. Detta gör att du kan utföra ytterligare förbehandling, t.ex. mappa utbildningsdata till dina poängdata om det behövs.

## Pipeline-fil {#pipeline-file}

The `pipeline.py` filen innehåller logik för utbildning och poängsättning.

Syftet med kursen är att skapa en modell med hjälp av funktioner och etiketter i utbildningsdatauppsättningen. När du har valt en utbildningsmodell måste du anpassa dina x- och y-utbildningsdata till modellen så att funktionen returnerar den tränade modellen.

>[!NOTE]
> 
>Funktionerna avser den indatavariabel som används av maskininlärningsmodellen för att förutsäga etiketterna.

![def-tåg](../images/jupyterlab/create-recipe/def_train.png)

The `score()` -funktionen ska innehålla resultatalgoritmen och returnera ett mått som anger hur framgångsrik modellen är. The `score()` funktionen använder resultatdatauppsättningsrubrikerna och den tränade modellen för att generera en uppsättning förutsedda funktioner. Dessa förväntade värden jämförs sedan med de faktiska funktionerna i poängdatauppsättningen. I det här exemplet `score()` funktionen använder den tränade modellen för att förutsäga funktioner med hjälp av etiketterna från poängdatamängden. De förväntade funktionerna returneras.

![def score](../images/jupyterlab/create-recipe/def_score.png)

## Utvärderarfil {#evaluator-file}

The `evaluator.py` filen innehåller logik för hur du vill utvärdera ditt utbildade recept och hur dina utbildningsdata ska delas upp.

### Dela datauppsättningen {#split-the-dataset}

Dataledningsfasen för utbildning kräver att datauppsättningen delas för utbildning och testning. Detta `val` data används implicit för att utvärdera modellen efter att den har tränats. Den här processen är skild från poängsättningen.

I det här avsnittet visas `split()` som läser in data i anteckningsboken och sedan rensar bort orelaterade kolumner i datauppsättningen. Därifrån kan du utföra funktionsteknologi, d.v.s. skapa ytterligare relevanta funktioner från befintliga råa funktioner i data.

![Delningsfunktion](../images/jupyterlab/create-recipe/split.png)

### Utvärdera den utbildade modellen {#evaluate-the-trained-model}

The `evaluate()` funktionen utförs efter att modellen har tränats och returnerar ett mått som anger hur framgångsrik modellen är. The `evaluate()` funktionen använder testdatauppsättningsrubrikerna och den tränade modellen för att förutsäga en uppsättning funktioner. Dessa förväntade värden jämförs sedan med de faktiska funktionerna i testdatauppsättningen. I det här exemplet är de mått som används `precision`, `recall`, `f1`och `accuracy`. Observera att funktionen returnerar en `metric` -objekt som innehåller en array med utvärderingsvärden. Dessa mått används för att utvärdera hur väl den tränade modellen fungerar.

![utvärdera](../images/jupyterlab/create-recipe/evaluate.png)

Lägger till `print(metric)` gör att du kan visa mätresultaten.

![mätresultat](../images/jupyterlab/create-recipe/evaluate_metric.png)

## Data Saver-fil {#data-saver-file}

The `datasaver.py` filen innehåller `save()` och används för att spara din förutsägelse när du testar poängsättningen. The `save()` funktionen tar hänsyn till dina förutsägelser och använder [!DNL Experience Platform Catalog] API:er, skriver data till `scoringResultsDataSetId` du angett i `scoring.conf` -fil. Du kan

![Datasparare](../images/jupyterlab/create-recipe/data_saver.png)

## Utbildning och poängsättning {#training-and-scoring}

När du har gjort ändringar i din bärbara dator och vill utbilda ditt recept kan du välja de tillhörande knapparna högst upp i fältet för att skapa en träningskörning i cellen. När du väljer knappen visas en logg med kommandon och utdata från utbildningsskriptet i anteckningsboken (under `evaluator.py` cell). Conda installerar först alla beroenden, sedan initieras kursen.

Observera att du måste genomföra en utbildning minst en gång innan du kan göra en poängsättning. Markera **[!UICONTROL Run Scoring]** kommer att poängsätta den tränade modell som genererades under kursen. Bedömningsskriptet visas under `datasaver.py`.

Om du vill se dolda utdata lägger du till `debug` till slutet av utdatacellen och kör den igen.

![Utbildning och poäng](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Skapa ett recept {#create-recipe}

När du är klar med redigeringen av recept och nöjd med utbildnings-/poängsättningsresultatet kan du skapa ett recept från anteckningsboken genom att välja **[!UICONTROL Create Recipe]** i det övre högra hörnet.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Efter markering **[!UICONTROL Create Recipe]** uppmanas du att ange ett receptnamn. Det här namnet representerar det faktiska receptet som skapades på [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

När du har valt **[!UICONTROL Ok]**, börjar processen att skapa recept. Detta kan ta en stund och en förloppsindikator visas i stället för knappen Skapa recept. När du är klar kan du välja **[!UICONTROL View Recipes]** för att ta dig till **[!UICONTROL Recipes]** flik under **[!UICONTROL ML Models]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - Ta inte bort någon av filcellerna
> - Redigera inte `%%writefile` rad överst i filcellerna
> - Skapa inte recept i olika anteckningsböcker samtidigt


## Nästa steg {#next-steps}

Genom att slutföra den här självstudiekursen har du lärt dig att skapa en maskininlärningsmodell i [!UICONTROL Recipe Builder] anteckningsbok. Du har också lärt dig hur du använder anteckningsboken för att hämta arbetsflöden.

Att fortsätta lära sig att arbeta med resurser i [!DNL Data Science Workspace], besök [!DNL Data Science Workspace] recept och modeller.