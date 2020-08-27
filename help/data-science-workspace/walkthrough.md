---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Genomgång av datavetenskapens arbetsyta
topic: Walkthrough
description: Det här dokumentet innehåller en genomgång av Adobe Experience Platform Data Science Workspace. Det allmänna arbetsflöde som en datavetare skulle gå igenom för att lösa ett problem med maskininlärning.
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---


# [!DNL Data Science Workspace] genomgång

Det här dokumentet innehåller en genomgång för Adobe Experience Platform [!DNL Data Science Workspace]. Vi går igenom det allmänna arbetsflöde som en datavetare skulle gå igenom för att lösa ett problem med maskininlärning.

## Förutsättningar

- Ett registrerat Adobe ID-konto
   - Adobe ID-kontot måste ha lagts till i en organisation med tillgång till Adobe Experience Platform och [!DNL Data Science Workspace]

## Datavetenskaparens motivation

En återförsäljare står inför många utmaningar när det gäller att vara konkurrenskraftiga på den nuvarande marknaden. En av detaljhandlarens främsta bekymmer är att besluta om den optimala prissättningen av deras produkter och att förutse försäljningstrender. Med en korrekt prognosmodell skulle handlaren kunna hitta förhållandet mellan efterfrågan och prispolitiken och fatta optimerade prissättningsbeslut för att maximera försäljningen och intäkterna.

## Datavetenskaparens lösning

En datavetare kan utnyttja den stora mängd historiska data som en återförsäljare har tillgång till för att förutse framtida trender och optimera prissättningsbesluten. Vi kommer att använda tidigare försäljningsdata för att utbilda vår maskininlärningsmodell och använda modellen för att förutse framtida försäljningstrender. Med detta kan återförsäljaren få insikter som hjälper dem att ändra priserna.

I den här översikten ska vi gå igenom de steg som en datavetare skulle gå igenom för att ta en datauppsättning och skapa en modell för att förutse försäljningen varje vecka. Vi går igenom följande avsnitt i den exempel som finns på Adobe Experience Platform [!DNL Data Science Workspace]:

- [Inställningar](#setup)
- [Utforska data](#exploring-data)
- [Funktionskonstruktion](#feature-engineering)
- [Utbildning och verifiering](#training-and-verification)

### Anteckningsböcker i [!DNL Data Science Workspace]

För det första vill vi skapa en [!DNL JupyterLab] anteckningsbok för att öppna exempelanteckningsboken&quot;Detaljhandel&quot;. Om vi följer de steg som datavetenskaparen utför i den bärbara datorn kan vi få en förståelse för ett typiskt arbetsflöde.

I Adobe Experience Platform-gränssnittet klickar du på fliken Datavetenskap på den översta menyn för att ta dig till [!DNL Data Science Workspace]. På den här sidan klickar du på den [!DNL JupyterLab] flik som öppnar [!DNL JupyterLab] startprogrammet. Du bör se en liknande sida.

![](./images/walkthrough/jupyterlab_launcher.png)

I vår självstudiekurs kommer vi att använda [!DNL Python] 3 i [!DNL Jupyter Notebook] för att visa hur du får tillgång till och utforskar data. På startsidan finns exempelanteckningsböcker. Vi kommer att använda exemplet&quot;Detaljhandel försäljning&quot; för [!DNL Python] 3.

![](./images/walkthrough/retail_sales.png)

### Inställningar {#setup}

I och med att Butik Sales-anteckningsboken är öppen är det första vi gör att läsa in de bibliotek som krävs för vårt arbetsflöde. I följande lista ges en kort beskrivning av vad de används för:
- **numpy** - vetenskapligt datorbibliotek som ger stöd för stora flerdimensionella matriser och matriser
- **pandor** - bibliotek som innehåller datastrukturer och operationer som används för datamanipulering och -analys
- **matplotlib.pyplot** - plottningsbibliotek som ger en MATLAB-liknande upplevelse vid plottning
- **seaborn** - högnivåbibliotek för visualisering av gränssnittsdata baserat på matplotlib
- **sklearn** - maskininlärningsbibliotek med klassificering, regression, stöd för vektor- och klusteralgoritmer
- **varningar** - bibliotek som styr varningsmeddelanden

### Utforska data {#exploring-data}

#### Läs in data

När biblioteken har lästs in kan vi börja titta på data. I följande [!DNL Python] kod används pandas `DataFrame` datastruktur och funktionen [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) för att läsa CSV-filen som finns [!DNL Github] i pandornas DataFrame:

![](./images/walkthrough/read_csv.png)

Pandornas DataFrame-datastruktur är en tvådimensionell datastruktur med etiketter. För att snabbt se dimensionerna på våra data kan vi använda `df.shape`. Detta returnerar en tuppel som representerar dimensionaliteten för DataFrame:

![](./images/walkthrough/df_shape.png)

Slutligen kan vi ta en titt på hur våra data ser ut. Vi kan använda `df.head(n)` för att visa de första `n` raderna i DataFrame:

![](./images/walkthrough/df_head.png)

#### Statistisk sammanfattning

Vi kan utnyttja [!DNL Python's] pandabiblioteket för att hämta datatypen för varje attribut. Utdata från följande anrop ger oss information om antalet poster och datatypen för var och en av kolumnerna:

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Den här informationen är användbar eftersom du vet vilken datatyp varje kolumn har, så att vi kan veta hur vi ska behandla data.

Låt oss titta på den statistiska sammanfattningen. Endast de numeriska datatyperna visas så `date`, `storeType`och `isHoliday` kommer inte att skrivas ut:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Här ser vi att det finns 6 435 förekomster för varje egenskap. Dessutom ges statistiska uppgifter som medelvärde, standardavvikelse (std), min, max och interkvartilter. Detta ger oss information om avvikelsen för data. I nästa avsnitt ska vi gå igenom visualisering som fungerar tillsammans med denna information för att ge oss en fullständig förståelse för våra data.

Om vi tittar på minimi- och maximivärdena för `store`ser vi att det finns 45 unika lagringsplatser som data representerar. Det finns också `storeTypes` som skiljer ut vad en butik är. Vi kan se distributionen av `storeTypes` genom att göra följande:

![](./images/walkthrough/df_groupby.png)

Det innebär att 22 butiker är av `storeType A` , 17 är `storeType B`och 6 är `storeType C`.

#### Visualisera data

Nu när vi känner till våra värden för dataramar vill vi komplettera detta med visualiseringar för att göra saker klarare och enklare att identifiera mönster. Dessa diagram är också användbara när du vill förmedla resultat till en viss målgrupp.

#### Univariata diagram

Univariata diagram är diagram av en enskild variabel. Ett vanligt unikt diagram som används för att visualisera dina data är lådor och morrdiagram.

Med hjälp av våra butiksdata från tidigare kan vi generera låda och morrfack för var och en av de 45 butikerna och deras försäljning varje vecka. Ritytan genereras med `seaborn.boxplot` funktionen.

![](./images/walkthrough/box_whisker.png)

En låda och en löpyta används för att visa datafördelningen. De yttre raderna i ritytan visar de övre och nedre kvartilarna medan rutan sträcker sig över interkvartilsintervallet. Linjen i rutan anger medianen. Alla datapunkter som är mer än 1,5 gånger den övre eller nedre kanten markeras som en cirkel. Dessa punkter betraktas som avvikelser.

Sedan kan vi plotta veckoförsäljningen med tiden. Vi visar bara resultatet från den första butiken. Koden i den bärbara datorn genererar 6 ytor som motsvarar 6 av de 45 butikerna i vår datamängd.

![](./images/walkthrough/weekly_sales.png)

I det här diagrammet kan vi jämföra försäljningen varje vecka under en tvåårsperiod. Det är lätt att se försäljningstoppar och dalmönster över tiden.

#### Multivariata diagram

Multivariata diagram används för att se interaktionen mellan variabler. Med visualiseringen kan datavetare se om det finns några samband eller mönster mellan variablerna. Ett vanligt multivariatdiagram är en korrelationsmatris. Med en korrelationsmatris kvantifieras beroenden mellan flera variabler med korrelationskoefficienten.

Med samma butiksdatauppsättning kan vi generera en korrelationsmatris.

![](./images/walkthrough/correlation_1.png)

Observera diagonalen för de där bilderna nedåt i mitten. Detta visar att en variabel har en fullständig positiv korrelation när den jämförs med sig själv. Stark positiv korrelation kommer att ha en storlek närmare 1 medan svaga korrelationer kommer närmare 0. Negativ korrelation visas med en negativ koefficient som visar en omvänd trend.

### Funktionsteknik {#feature-engineering}

I det här avsnittet kommer vi att göra ändringar i vår detaljhandelsdatamängd. Vi kommer att utföra följande åtgärder:

- lägg till vecka- och årskolumner
- konvertera storeType till en indikatorvariabel
- konvertera isHoliday till en numerisk variabel
- predikat weekSales of next week

#### Lägg till vecka- och årskolumner

Det aktuella formatet för datum (`2010-02-05`) är svårt att skilja mellan data för varje vecka. På grund av detta kommer vi att konvertera datumet till vecka och år.

![](./images/walkthrough/date_to_week_year.png)

Vecka och datum är följande:

![](./images/walkthrough/date_week_year.png)

#### Konvertera storeType till indikatorvariabel

Sedan vill vi konvertera kolumnen storeType till kolumner som representerar varje `storeType`. Det finns tre butikstyper (`A`, `B`, `C`) som vi skapar tre nya kolumner från. Värdet som anges i var och en av dem blir ett booleskt värde där 1 anges beroende på vad som `storeType` var och `0` för de andra två kolumnerna.

![](./images/walkthrough/storeType.png)

Den aktuella `storeType` kolumnen tas bort.

#### Konvertera isHoliday till numerisk typ

Nästa ändring är att ändra det booleska värdet till en numerisk `isHoliday` representation.

![](./images/walkthrough/isHoliday.png)


#### Förutspå varje veckaFörsäljning nästa vecka

Nu vill vi lägga till föregående och kommande veckoförsäljning till var och en av våra datauppsättningar. Vi gör det här genom att offra våra `weeklySales`. Dessutom beräknar vi `weeklySales` skillnaden. Detta görs genom att subtrahera `weeklySales` med föregående veckas `weeklySales`.

![](./images/walkthrough/weekly_past_future.png)

Eftersom vi förskjuter 45 datauppsättningar framåt och 45 datauppsättningar bakåt för att skapa nya kolumner kommer de första och sista 45 datapunkterna att ha NaN-värden. `weeklySales` Vi kan ta bort de här punkterna från vår datauppsättning genom att använda `df.dropna()` funktionen som tar bort alla rader som har NaN-värden.

![](./images/walkthrough/dropna.png)

En sammanfattning av datauppsättningen efter våra ändringar visas nedan:

![](./images/walkthrough/df_info_new.png)

### Utbildning och kontroll {#training-and-verification}

Nu är det dags att skapa några modeller av data och välja vilken modell som är bäst för att förutse framtida försäljning. Vi kommer att utvärdera följande fem algoritmer:

- Linjär regression
- Beslutsträd
- Slumpmässig skog
- Övertoningsförstärkning
- K-grannar

#### Dela upp datauppsättningar till utbildnings- och testunderuppsättningar

Vi behöver ett sätt att veta hur korrekt vår modell kommer att kunna förutse värden. Utvärderingen kan göras genom att en del av datauppsättningen tilldelas som validering och resten som utbildningsdata. Eftersom `weeklySalesAhead` är de faktiska framtida värdena för `weeklySales`kan vi använda detta för att utvärdera hur exakt modellen är när värdet förutses. Delningen görs nedan:

![](./images/walkthrough/split_data.png)

Vi har nu `X_train` och `y_train` för att förbereda modellerna och `X_test` och `y_test` för utvärdering senare.

#### Kontrollalgoritmer

I det här avsnittet deklarerar vi alla algoritmer i en array med namnet `model`. Därefter itererar vi igenom den här arrayen och för varje algoritm anger vi våra utbildningsdata `model.fit()` som skapar en modell `mdl`. Genom att använda den här modellen kan vi förutse `weeklySalesAhead` med våra `X_test` data.

![](./images/walkthrough/training_scoring.png)

För poängsättningen tar vi den genomsnittliga procentuella skillnaden mellan det förväntade värdet `weeklySalesAhead` och de faktiska värdena i `y_test` data. Eftersom vi vill minimera skillnaden mellan vår prognos och den faktiska är övertoningsregressorn den bästa modellen.

#### Visualisera prognoser

Slutligen ska vi visualisera vår prognosmodell med de faktiska veckoförsäljningsvärdena. Den blå linjen representerar de faktiska siffrorna, medan den gröna representerar vår förutsägelse med hjälp av Övertoningsförstärkning. Följande kod genererar 6 plot som representerar 6 av de 45 butikerna i vår datamängd. Endast `Store 1` här:

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## Slutsats

Med den här översikten gick vi igenom arbetsflödet som en datavetare skulle gå igenom för att lösa ett försäljningsproblem inom detaljhandeln. Vi gick igenom följande steg för att nå en lösning som förutser framtida försäljning varje vecka.

- [Inställningar](#setup)
- [Utforska data](#exploring-data)
- [Funktionskonstruktion](#feature-engineering)
- [Utbildning och verifiering](#training-and-verification)