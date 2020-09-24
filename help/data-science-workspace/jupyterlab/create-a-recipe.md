---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics;create recipe
solution: Experience Platform
title: Skapa ett recept med Jupyter-anteckningsböcker
topic: tutorial
type: Tutorial
description: Den här självstudiekursen går igenom två huvudavsnitt. Först skapar du en maskininlärningsmodell med hjälp av en mall i JupyterLab Notebook. Därefter ska du använda anteckningsboken för att hämta arbetsflöden i JupyterLab för att skapa ett recept i arbetsytan Data Science.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '2316'
ht-degree: 0%

---


# Skapa ett recept med Jupyter-anteckningsböcker

Den här självstudiekursen går igenom två huvudavsnitt. Först skapar du en maskininlärningsmodell med hjälp av en mall i [!DNL JupyterLab Notebook]. Därefter ska du använda anteckningsboken för att hämta arbetsflödet i [!DNL JupyterLab] för att skapa ett recept i [!DNL Data Science Workspace].

## Nya koncept:

- **Recept:** Ett recept är en AdobeTerm för en modellspecifikation och är en toppnivåbehållare som representerar en specifik maskininlärning, AI-algoritm eller en kombination av algoritmer, bearbetningslogik och konfiguration som krävs för att skapa och köra en tränad modell och därmed bidra till att lösa specifika affärsproblem.
- **Modell:** En modell är en instans av ett maskininlärningsrecept som är utbildat med historiska data och konfigurationer för att lösa ett affärsärende.
- **Utbildning:** Utbildning är processen att lära sig mönster och insikter från märkta data.
- **Poäng:** Poängberäkning är processen att generera insikter från data med hjälp av en tränad modell.

## Kom igång med [!DNL JupyterLab] anteckningsboksmiljön

Du kan skapa ett helt nytt recept i [!DNL Data Science Workspace]. Börja med att navigera till [Adobe Experience Platform](https://platform.adobe.com) och klicka på **[!UICONTROL Notebooks]** fliken till vänster. Skapa en ny anteckningsbok genom att välja mallen Recipe Builder i [!DNL JupyterLab Launcher].

Med den [!UICONTROL Recipe Builder] bärbara datorn kan du köra utbildning och poängsättning inuti den bärbara datorn. Detta ger er flexibilitet att ändra deras `train()` och `score()` metoder mellan att köra experiment med kurser och poängdata. När du är nöjd med resultatet av kursen och poängsättningen kan du skapa ett recept som ska användas i [!DNL Data Science Workspace] den bärbara datorn för att hämta funktionalitet som är inbyggd i den bärbara datorn i Recipe Builder.

>[!NOTE]
>
>Anteckningsboken Recipe Builder har stöd för att arbeta med alla filformat, men för närvarande har funktionen Skapa recept bara stöd [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder.png)

När du klickar på anteckningsboken i Recipe Builder från startprogrammet öppnas anteckningsboken på fliken. Mallen som används i anteckningsboken är Python Retail Sales Forecasting Recipe, som också finns i [denna offentliga databas](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

Du ser att det finns ytterligare tre åtgärder i verktygsfältet: - **[!UICONTROL Train]**, **[!UICONTROL Score]** och **[!UICONTROL Create Recipe]**. De här ikonerna visas bara i [!UICONTROL Recipe Builder] anteckningsboken. Mer information om de här åtgärderna kommer att behandlas [i avsnittet](#training-and-scoring) Utbildning och poängsättning när du har skapat din recept i anteckningsboken.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Redigera filer

Om du vill redigera receptfilerna går du till den cell i Jupyter som motsvarar filsökvägen. Om du till exempel vill göra ändringar i `evaluator.py`söker du efter `%%writefile demo-recipe/evaluator.py`.

Börja göra nödvändiga ändringar i cellen och kör cellen när du är klar. Med `%%writefile filename.py` kommandot skriver du innehållet i cellen till `filename.py`cellen. Du måste köra cellen manuellt för varje fil med ändringar.

>[!NOTE]
>
>Du bör köra cellerna manuellt när det är tillämpligt.

## Kom igång med anteckningsboken i Recipe Builder

Nu när du vet grunderna för [!DNL JupyterLab] anteckningsboksmiljön kan du börja titta på de filer som utgör ett maskininlärningsmodellrecept. De filer vi ska prata om visas här:

- [Kravfil](#requirements-file)
- [Konfigurationsfiler](#configuration-files)
- [Utbilda datainläsare](#training-data-loader)
- [Inläsare av poängdata](#scoring-data-loader)
- [Pipeline-fil](#pipeline-file)
- [Utvärderarfil](#evaluator-file)
- [Data Saver-fil](#data-saver-file)

### Kravfil {#requirements-file}

Kravfilen används för att deklarera ytterligare bibliotek som du vill använda i receptet. Du kan ange versionsnumret om det finns ett beroende. Om du vill söka efter fler bibliotek går du till https://anaconda.org. Listan med de huvudbibliotek som redan används är:

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Bibliotek eller specifika versioner som du lägger till kan vara inkompatibla med ovanstående bibliotek.

### Konfigurationsfiler {#configuration-files}

Konfigurationsfilerna, `training.conf` och `scoring.conf`, används för att ange de datauppsättningar som du vill använda för utbildning och bedömning samt för att lägga till hyperparametrar. Det finns olika konfigurationer för utbildning och poängsättning.

Användarna måste fylla i följande variabler innan de kör utbildning och poängsättning:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Om du vill hitta data- och schema-ID:n går du till fliken Data i anteckningsböcker i det vänstra navigeringsfältet (under mappikonen).

![](../images/jupyterlab/create-recipe/datasets.png)

Samma information finns på [Adobe Experience Platform](https://platform.adobe.com/) på flikarna **[Schema](https://platform.adobe.com/schema)** och **[Datauppsättningar](https://platform.adobe.com/dataset/overview)** .

Som standard ställs följande konfigurationsparametrar in åt dig när du använder data:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Utbilda datainläsare {#training-data-loader}

Syftet med inläsaren av utbildningsdata är att instansiera data som används för att skapa maskininlärningsmodellen. Vanligtvis finns det två åtgärder som inläsaren av utbildningsdata utför:
- Läs in data från [!DNL Platform]
- Datagenerering och -teknik

I följande två avsnitt går det längre att läsa in data och förbereda data.

### Läser in data {#loading-data}

I det här steget används [pandabilden](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Data kan läsas in från filer i [!DNL Adobe Experience Platform] med [!DNL Platform] SDK (`platform_sdk`) eller från externa källor med pandas `read_csv()` eller `read_json()` funktioner.

- [[!DNL Platform SDK]](#platform-sdk)
- [Externa källor](#external-sources)

>[!NOTE]
>
>I Recipe Builder-anteckningsboken läses data in via `platform_sdk` datainläsaren.

### [!DNL Platform] SDK {#platform-sdk}

En ingående självstudiekurs om hur du använder `platform_sdk` datainläsaren finns i handboken [för](../authoring/platform-sdk.md)plattforms-SDK. Den här självstudiekursen innehåller information om autentisering av bygge, grundläggande läsning av data och grundläggande skrivande av data.

### Externa källor {#external-sources}

I det här avsnittet visas hur du importerar en JSON- eller CSV-fil till ett pandaobjekt. Officiell dokumentation från pandabiblioteket finns här:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Här följer ett exempel på hur du importerar en CSV-fil. Argumentet `data` är sökvägen till CSV-filen. Variabeln importerades från `configProperties` i det [föregående avsnittet](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

Du kan även importera från en JSON-fil. Argumentet `data` är sökvägen till CSV-filen. Variabeln importerades från `configProperties` i det [föregående avsnittet](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Nu finns dina data i dataframe-objektet och kan analyseras och ändras i [nästa avsnitt](#data-preparation-and-feature-engineering).

### Från SDK för dataåtkomst (borttagen)

>[!CAUTION]
>
> `data_access_sdk_python` rekommenderas inte längre, se [Konvertera dataåtkomstkod till plattforms-SDK](../authoring/platform-sdk.md) för en guide om hur du använder `platform_sdk` datainläsaren.

Användare kan läsa in data med hjälp av SDK för dataåtkomst. Biblioteket kan importeras högst upp på sidan genom att inkludera raden:

`from data_access_sdk_python.reader import DataSetReader`

Sedan använder vi metoden för att hämta utbildningsdatauppsättningen från `load()` enligt vår konfigurationsfil ( `trainingDataSetId``recipe.conf`).

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE]
>
>Som vi nämnt i avsnittet [](#configuration-files)Konfigurationsfil ställs följande konfigurationsparametrar in åt dig när du får åtkomst till data från [!DNL Experience Platform]:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Nu när du har tillgång till dina data kan du börja med dataförberedelser och funktionskonstruktion.

### Datagenerering och -teknik {#data-preparation-and-feature-engineering}

När data har lästs in, förbereds de och delas sedan upp i `train` - och `val` datauppsättningar. Exempelkod visas nedan:

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

I det här exemplet görs fem saker med den ursprungliga datauppsättningen:
- lägga till `week` och `year` kolumner
- konvertera `storeType` till en indikatorvariabel
- konvertera `isHoliday` till en numerisk variabel
- offset `weeklySales` för att få framtida och föregående försäljningsvärde
- dela data, efter datum, till `train` och `val` datauppsättning

Först skapas `week` och `year` kolumner och den ursprungliga `date` kolumnen konverteras till [!DNL Python] datetime [](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). Vecka- och årtalsvärden extraheras från datetime-objektet.

Därefter `storeType` konverteras de till tre kolumner som representerar de tre olika butikstyperna (`A`, `B`och `C`). Var och en innehåller ett booleskt värde som `storeType` är true. Kolumnen tas bort `storeType` .

På samma sätt `weeklySales` ändras det booleska värdet `isHoliday` till en numerisk representation, en eller noll.

Dessa data delas mellan `train` och `val` datauppsättning.

Funktionen ska `load()` slutföras med `train` och `val` datauppsättningen som utdata.

### Inläsare av poängdata {#scoring-data-loader}

Förfarandet för att läsa in data för poängsättning liknar inläsningen av utbildningsdata i `split()` funktionen. Vi använder SDK:n för dataåtkomst för att läsa in data från de `scoringDataSetId` som finns i vår `recipe.conf` fil.

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

När du har läst in data färdigställs data och funktionen är klar.

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

Eftersom syftet med vår modell är att förutsäga framtida försäljning varje vecka, måste du skapa en poängsättningsdatauppsättning som används för att utvärdera hur väl modellens förutsägelse fungerar.

Den här Recipe Builder-anteckningsboken gör detta genom att kompensera för vår veckoförsäljning 7 dagar framåt. Observera att det finns mått för 45 butiker varje vecka så att du kan flytta värdena för 45 datauppsättningar framåt till en ny kolumn som kallas `weeklySales` `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

På samma sätt kan du skapa en kolumn `weeklySalesLag` som har flyttats 45 bakåt. På så sätt kan du även beräkna skillnaden i veckoförsäljning och lagra dem i kolumn `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Eftersom du förskjuter datapunkterna 45-datauppsättningar framåt och 45-datauppsättningar bakåt för att skapa nya kolumner kommer den första och sista 45 datapunkterna att ha NaN-värden. `weeklySales` Du kan ta bort de här punkterna från vår datauppsättning genom att använda `df.dropna()` funktionen som tar bort alla rader som har NaN-värden.

```PYTHON
df.dropna(0, inplace=True)
```

Funktionen i din inläsare för betygsdata ska vara fullständig med betygsdatamängden som utdata. `load()`

### Pipeline-fil {#pipeline-file}

Filen innehåller `pipeline.py` logik för utbildning och poängsättning.

### Utbildning {#training}

Syftet med kursen är att skapa en modell med hjälp av funktioner och etiketter i utbildningsdatauppsättningen.

>[!NOTE]
> 
>_Funktionerna_ avser den indatavariabel som används av maskininlärningsmodellen för att förutsäga _etiketterna_.

Funktionen ska omfatta `train()` utbildningsmodellen och returnera den utbildade modellen. Exempel på olika modeller finns i dokumentationen till användarhandboken [med](https://scikit-learn.org/stable/user_guide.html)vetenskaplig information.

När du har valt en utbildningsmodell passar du in i dina x- och y-utbildningsdata efter modellen, och funktionen returnerar den tränade modellen. Ett exempel som visar detta är:

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

Observera att beroende på vilket program du använder så har du argument i `GradientBoostingRegressor()` funktionen. `xTrainingDataset` ska innehålla de funktioner som används för utbildning och `yTrainingDataset` ska innehålla etiketter.

### Poäng {#scoring}

Funktionen ska innehålla `score()` resultatalgoritmen och returnera ett mått som anger hur framgångsrik modellen är. Funktionen använder `score()` poängsättningsdatauppsättningsrubrikerna och den tränade modellen för att generera en uppsättning förutsedda funktioner. Dessa förväntade värden jämförs sedan med de faktiska funktionerna i poängdatauppsättningen. I det här exemplet använder `score()` funktionen den tränade modellen för att förutsäga funktioner med hjälp av etiketterna från resultatdatauppsättningen. De förväntade funktionerna returneras.

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### Utvärderarfil {#evaluator-file}

Filen `evaluator.py` innehåller logik för hur du vill utvärdera ditt utbildade recept och hur dina utbildningsdata ska delas upp. I exemplet med detaljhandel inkluderas logiken för att läsa in och förbereda utbildningsdata. Vi går igenom de två avsnitten nedan.

### Dela datauppsättningen {#split-the-dataset}

Dataledningsfasen för utbildning kräver att datauppsättningen delas för utbildning och testning. Dessa `val` data används implicit för att utvärdera modellen efter att den har tränats. Den här processen är skild från poängsättningen.

I det här avsnittet visas den `split()` funktion som först läser in data i anteckningsboken och sedan rensar data genom att ta bort orelaterade kolumner i datauppsättningen. Därifrån kan du utföra funktionsteknologi, d.v.s. skapa ytterligare relevanta funktioner från befintliga råa funktioner i data. Ett exempel på den här processen visas nedan tillsammans med en förklaring.

Funktionen `split()` visas nedan. Den databildruta som anges i argumentet delas upp i `train` och de variabler `val` som ska returneras.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### Utvärdera den utbildade modellen {#evaluate-the-trained-model}

Funktionen utförs `evaluate()` efter att modellen har tränats och returnerar ett mått som anger hur framgångsrik modellen är. Funktionen använder `evaluate()` testdatauppsättningsrubrikerna och den utbildade modellen för att förutsäga en uppsättning funktioner. Dessa förväntade värden jämförs sedan med de faktiska funktionerna i testdatauppsättningen. Vanliga bedömningsalgoritmer är:
- [Genomsnittligt absolut procentfel (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Medel absolut fel (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [RMSE (Root-ean-square error)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


Funktionen `evaluate()` i exemplet med försäljning inom detaljhandeln visas nedan:

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

Observera att funktionen returnerar ett `metric` objekt som innehåller en array med utvärderingsmått. Dessa mätvärden kommer att användas för att utvärdera hur väl den utbildade modellen fungerar.

### Data Saver-fil {#data-saver-file}

Filen `datasaver.py` innehåller `save()` funktionen som sparar din förutsägelse när du testar poängsättningen. Funktionen `save()` tar din förutsägelse och använder API: [!DNL Experience Platform Catalog] er, skriver data till den `scoringResultsDataSetId` du har angett i `scoring.conf` filen.

Exemplet som används i exempelreceptet för försäljning inom detaljhandeln visas här. Observera hur biblioteket `DataSetWriter` används för att skriva data till plattformen:

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## Utbildning och poängsättning {#training-and-scoring}

När du har gjort ändringar i din bärbara dator och vill utbilda ditt recept kan du klicka på de tillhörande knapparna högst upp i fältet för att skapa en utbildning i cellen. När du klickar på knappen visas en logg med kommandon och utdata från utbildningsskriptet i anteckningsboken (under `evaluator.py` cellen). Conda installerar först alla beroenden, sedan initieras kursen.

Observera att du måste genomföra en utbildning minst en gång innan du kan göra en poängsättning. Om du klickar på **[!UICONTROL Run Scoring]** knappen får du poäng på den tränade modell som skapades under träningen. Poängskriptet visas under `datasaver.py`.

Om du vill se dolda utdata lägger du till dem i slutet `debug` av utdatacellen och kör den igen.

## Skapa recept {#create-recipe}

När du är klar med redigeringen av recept och nöjd med utbildnings-/poängsättningsresultatet kan du skapa ett recept från anteckningsboken genom att trycka **[!UICONTROL Create Recipe]** i den övre högra navigeringen.

![](../images/jupyterlab/create-recipe/create-recipe.png)

När du har tryckt på knappen uppmanas du att ange ett receptnamn. Det här namnet representerar det faktiska receptet som skapades [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

När du trycker på **[!UICONTROL Ok]** kan du navigera till det nya receptet på [Adobe Experience Platform](https://platform.adobe.com/). Du kan klicka på **[!UICONTROL View Recipes]** knappen för att gå till **[!UICONTROL Recipes]** fliken under **[!UICONTROL ML Models]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

När processen är klar ser receptet ut ungefär så här:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - Ta inte bort någon av filcellerna
> - Redigera inte raden `%%writefile` överst i filcellerna
> - Skapa inte recept i olika anteckningsböcker samtidigt


## Nästa steg {#next-steps}

Genom att slutföra den här självstudiekursen har du lärt dig att skapa en maskininlärningsmodell i anteckningsboken för Recipe Builder. Du har också lärt dig hur du använder anteckningsboken för att hämta arbetsflöden i anteckningsboken för att skapa ett recept i [!DNL Data Science Workspace].

Om du vill fortsätta lära dig hur du arbetar med resurser i [!DNL Data Science Workspace]går du till listrutan [!DNL Data Science Workspace] recept och modeller.

## Ytterligare resurser {#additional-resources}

Följande video har utformats för att ge stöd för din förståelse för att bygga och driftsätta modeller.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


