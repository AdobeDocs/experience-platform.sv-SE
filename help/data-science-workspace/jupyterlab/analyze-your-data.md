---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;analyze data notebooks
solution: Experience Platform
title: Analysera dina data med bärbara datorer
topic: Tutorial
description: I den här självstudiekursen fokuseras på hur du använder Jupyter-anteckningsböcker som är byggda i Data Science Workspace för att få tillgång till, utforska och visualisera dina data.
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# Analysera dina data med bärbara datorer

I den här självstudiekursen fokuseras på hur du använder Jupyter-anteckningsböcker som är byggda i Data Science Workspace för att få tillgång till, utforska och visualisera dina data. I slutet av den här självstudiekursen bör du känna till några av de funktioner Jupyter-anteckningsböcker erbjuder för att bättre förstå dina data.

Följande koncept har introducerats:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) är nästa generations webbaserade gränssnitt för Project Jupyter och är nära integrerat i [!DNL Adobe Experience Platform].
- **Grupper:** Datauppsättningar består av grupper. En batch är en uppsättning data som samlats in under en tidsperiod och som bearbetas tillsammans som en enda enhet. Nya grupper skapas när data läggs till i en datauppsättning.
- **SDK för dataåtkomst (borttagen):** SDK för dataåtkomst är nu föråldrat. Använd [[!DNL Platform SDK]](../authoring/platform-sdk.md) -guiden.

## Utforska anteckningsböcker i Data Science Workspace

I det här avsnittet utforskas data som tidigare har importerats till försäljningsschemat.

Med Data Science Workspace kan man skapa [!DNL Jupyter Notebooks] på den [!DNL JupyterLab] plattform där man kan skapa och redigera maskininlärningsarbetsflöden. [!DNL JupyterLab] är ett verktyg för samarbete mellan server och klient som gör att användare kan redigera anteckningsboksdokument via en webbläsare. De här anteckningsböckerna kan innehålla både körbar kod och RTF-element. För våra syften kommer vi att använda Markdown för analysbeskrivning och körbar [!DNL Python] kod för att utföra datautforskande och -analys.

### Välj arbetsyta

När vi startar [!DNL JupyterLab]visas ett webbaserat gränssnitt för Jupyter-anteckningsböcker. Beroende på vilken typ av anteckningsbok vi väljer startas en motsvarande kärna.

När vi jämför vilken miljö vi ska använda måste vi ta hänsyn till varje tjänsts begränsningar. Om vi till exempel använder [pandabiblioteket](https://pandas.pydata.org/) med [!DNL Python]som vanlig användare är RAM-gränsen 2 GB. Även som kraftfull användare är vi begränsade till 20 GB RAM. Om du hanterar större beräkningar är det bra att använda [!DNL Spark] som erbjuder 1,5 TB som delas med alla instanser av bärbara datorer.

Som standard fungerar Tensorflow-receptet i ett GPU-kluster och Python körs i ett CPU-kluster.

### Skapa en ny anteckningsbok

Klicka på fliken Datavetenskap i den övre menyn i [!DNL Adobe Experience Platform] användargränssnittet för att ta dig till arbetsytan Datavetenskap. På den här sidan klickar du på den [!DNL JupyterLab] flik som öppnar [!DNL JupyterLab] startprogrammet. Du bör se en liknande sida.

![](../images/jupyterlab/analyze-data/jupyterlab_launcher.png)

I vår självstudiekurs kommer vi att använda [!DNL Python] 3 i Jupyter Notebook för att visa hur du kommer åt och utforskar data. På startsidan finns exempelanteckningsböcker. Vi kommer att använda recept för [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

Koden för butiksförsäljning är ett fristående exempel som använder samma datauppsättning för butiksförsäljning för att visa hur data kan utforskas och visualiseras i Jupyter Notebook. Dessutom går den bärbara datorn vidare i detalj med utbildning och verifiering. Mer information om den här specifika anteckningsboken finns i den här [genomgången](../walkthrough.md).

### Åtkomstdata

>[!NOTE]
>
>Funktionen `data_access_sdk_python` är föråldrad och rekommenderas inte längre. Se självstudiekursen [Konvertera dataåtkomst till SDK till Platform SDK](../authoring/platform-sdk.md) för att konvertera koden. Samma steg nedan gäller fortfarande för den här självstudiekursen.

Vi kommer att gå igenom åtkomsten till data internt från [!DNL Adobe Experience Platform] och externt. Vi kommer att använda biblioteket för att komma åt interna data som datauppsättningar och XDM-scheman. `data_access_sdk_python` För externa data kommer vi att använda [!DNL Python] pandabiblioteket.

#### Externa data

När butiksförsäljningsjournalen är öppen hittar du rubriken&quot;Läs in data&quot;. I följande [!DNL Python] kod används pandas `DataFrame` datastruktur och funktionen [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) för att läsa CSV-filen som finns [!DNL Github] i DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

Pandornas DataFrame-datastruktur är en tvådimensionell datastruktur med etiketter. För att snabbt se dimensionerna på våra data kan vi använda `df.shape`. Detta returnerar en tuppel som representerar dimensionaliteten för DataFrame:

![](../images/jupyterlab/analyze-data/df_shape.png)

Slutligen kan vi ta en titt på hur våra data ser ut. Vi kan använda `df.head(n)` för att visa de första `n` raderna i DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] data

Nu går vi igenom åtkomsten till [!DNL Experience Platform] data.

##### Efter datauppsättnings-ID

I det här avsnittet använder vi datauppsättningen Detaljhandel, som är samma datauppsättning som används i exempelanteckningsboken för detaljhandelsförsäljning.

I Jupyter Notebook har vi åtkomst till våra data från fliken **Data** till vänster. När du klickar på fliken visas en lista med datauppsättningar.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

I katalogen Datasets kan vi nu se alla inkapslade datauppsättningar. Observera att det kan ta en minut att läsa in alla poster om din katalog är mycket ifylld med datauppsättningar.

Eftersom datauppsättningen är densamma vill vi ersätta inläsningsdata från föregående avsnitt som använder externa data. Markera kodblocket under **Läs in data** och tryck två gånger på **&#39;d&#39;** på tangentbordet. Se till att fokus ligger på blocket och inte på texten. Du kan trycka på **&#39;esc&#39;** för att undvika textfokus innan du trycker **&#39;d&#39;** två gånger.

Nu kan vi högerklicka på `Retail-Training-<your-alias>` datauppsättningen och välja alternativet Utforska data i anteckningsbok i listrutan. En körbar kodpost visas i anteckningsboken.

>[!TIP]
>
>gå till [[!DNL Platform SDK]](../authoring/platform-sdk.md) -guiden för att konvertera koden.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Om du arbetar med andra kärnor än [!DNL Python], se [den här sidan](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) för att få åtkomst till data på [!DNL Adobe Experience Platform].

Om du väljer den körbara cellen och sedan trycker på uppspelningsknappen i verktygsfältet körs den körbara koden. Utdata för `head()` blir en tabell med datamängdens nycklar som kolumner och de första n raderna i datauppsättningen. `head()` använder ett heltalsargument för att ange hur många rader som ska skrivas ut. Som standard är detta 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Om du startar om kärnan och kör alla celler igen bör du få samma utdata som tidigare.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Utforska era data

Nu när vi har tillgång till era data kan vi fokusera på själva data genom att använda statistik och visualisering. Den datauppsättning som vi använder är en detaljhandelsdatamängd som ger övrig information om 45 olika butiker en viss dag. Vissa egenskaper för en viss `date` och `store` omfattar följande:
- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### Statistisk sammanfattning

Vi kan utnyttja [!DNL Python's] pandabiblioteket för att hämta datatypen för varje attribut. Utdata från följande anrop ger oss information om antalet poster och datatypen för var och en av kolumnerna:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Den här informationen är användbar eftersom du vet vilken datatyp varje kolumn har, så att vi kan veta hur vi ska behandla data.

Låt oss titta på den statistiska sammanfattningen. Endast de numeriska datatyperna visas, så `date`, `storeType`och `isHoliday` kommer inte att skrivas ut:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Här ser vi att det finns 6 435 förekomster för varje egenskap. Dessutom ges statistiska uppgifter som medelvärde, standardavvikelse (std), min, max och interkvartilter. Detta ger oss information om avvikelsen för data. I nästa avsnitt ska vi gå igenom visualisering som fungerar tillsammans med denna information för att ge oss en god förståelse för våra data.

Om vi tittar på minimi- och maximivärdena för `store`ser vi att det finns 45 unika lagringsplatser som data representerar. Det finns också `storeTypes` som skiljer ut vad en butik är. Vi kan se distributionen av `storeTypes` genom att göra följande:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Det betyder att 22 butiker är av `storeType``A`, 17 är `storeType` `B`och 6 är `storeType` `C`.

#### Datavisualisering

Nu när vi känner till våra värden för dataramar vill vi komplettera detta med visualiseringar för att göra saker klarare och enklare att identifiera mönster. Diagram är också användbara när du vill förmedla resultat till en viss målgrupp. Vissa [!DNL Python] bibliotek som är användbara för visualisering är:
- [Matplotlib](https://matplotlib.org/)
- [pandor](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [ggplot](https://ggplot2.tidyverse.org/)

I det här avsnittet går vi snabbt igenom några fördelar med att använda varje bibliotek.

[Matplotlib](https://matplotlib.org/) är det äldsta [!DNL Python] visualiseringspaketet. Deras mål är att göra&quot;enkla saker enkla och hårda saker möjliga&quot;. Detta brukar vara sant eftersom paketet är extremt kraftfullt men också innehåller komplexitet. Det är inte alltid lätt att få en bra bild utan att behöva lägga en hel del tid och arbete på att göra det.

[Pandor](https://pandas.pydata.org/) används främst för objektet DataFrame, vilket möjliggör datahantering med integrerad indexering. Pandor har dock även en inbyggd plottningsfunktion som är baserad på matplotlib.

[seaborn](https://seaborn.pydata.org/) är ett paket som byggs ovanpå matplotlib. Det främsta målet är att göra standarddiagram mer visuellt tilltalande och att förenkla skapandet av komplicerade diagram.

[ggplot](https://ggplot2.tidyverse.org/) är ett paket som också är byggt ovanpå matplotlib. Den största skillnaden är dock att verktyget är en port för GPlot2 för R. På samma sätt som för sjömän är målet att förbättra för matplotlib. Användare som är bekanta med ggplot2 for R bör överväga det här biblioteket.


##### Univariata diagram

Univariata diagram är diagram av en enskild variabel. Ett vanligt univariat-diagram används för att visualisera dina data är lådan och morrplotten.

Med hjälp av våra butiksdata från tidigare kan vi generera låda och morrfack för var och en av de 45 butikerna och deras försäljning varje vecka. Ritytan genereras med `seaborn.boxplot` funktionen.

![](../images/jupyterlab/analyze-data/box_whisker.png)

En låda och en löpyta används för att visa datafördelningen. De yttre raderna i ritytan visar de övre och nedre kvartilarna, medan rutan sträcker sig över interkvartilsintervallet. Linjen i rutan anger medianen. Alla datapunkter som är mer än 1,5 gånger den övre eller nedre kanten markeras som en cirkel. Dessa punkter betraktas som avvikelser.

##### Multivariata diagram

Multivariata diagram används för att se interaktionen mellan variabler. Med visualiseringen kan datavetare se om det finns några samband eller mönster mellan variablerna. Ett vanligt multivariatdiagram är en korrelationsmatris. Med en korrelationsmatris kvantifieras beroenden mellan flera variabler med korrelationskoefficienten.

Med samma butiksdatauppsättning kan vi generera en korrelationsmatris.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Observera diagonalen för 1 är nedåt i mitten. Detta visar att en variabel har en fullständig positiv korrelation när den jämförs med sig själv. Stark positiv korrelation kommer att ha en storlek närmare 1 medan svaga korrelationer kommer närmare 0. Negativ korrelation visas med en negativ koefficient som visar en omvänd trend.


## Nästa steg

Den här självstudiekursen gick igenom hur du skapar en ny Jupyter-anteckningsbok i arbetsytan Data Science och hur du får tillgång till data både externt och från [!DNL Adobe Experience Platform]. Vi gick igenom följande steg:
- Skapa en ny Jupyter-anteckningsbok
- Få tillgång till datauppsättningar och scheman
- Utforska datauppsättningar

Nu kan du gå vidare till [nästa avsnitt](../models-recipes/package-source-files-recipe.md) för att paketera ett recept och importera det till Data Science Workspace.