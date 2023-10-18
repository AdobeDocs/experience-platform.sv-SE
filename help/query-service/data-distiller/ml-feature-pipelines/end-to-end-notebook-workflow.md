---
title: AI/ML-arbetsflöde för dataöverföring från början till slut
description: Använd molnbaserade bärbara datorer för maskininlärningsmiljö för att skapa en kursmodell och betygsmodell som förutser prenumerationskonverteringar från Adobe Experience Platform-data.
hide: true
hidefromtoc: true
source-git-commit: 12926f36514d289449cf0d141b5828df3fac37c2
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# AI/ML-arbetsflöde för berikning av data från början till slut

Använd Data Distiller för att berika era maskininlärningslinjer med värdefulla kundupplevelsedata som samlats in och strukturerats i Adobe Experience Platform.

Det här dokumentet innehåller en serie molnbaserade anteckningsböcker för maskininlärningsmiljö som demonstrerar ett komplett arbetsflöde. Arbetsflödet använder de maskininlärningsverktyg du föredrar för att skapa anpassade datamodeller som stöder dina marknadsföringsfall med data från Experience Platform.

Det här arbetsflödet kräver att [!DNL Python] bärbara datorer i maskininlärningsmiljöer. Instruktioner för att komma igång med dessa [!DNL Python] bärbara datorer ingår i deras respektive Viktigt-filer.

Innan du fortsätter med den här guiden följer du de steg som beskrivs i [Översikt över AI/ML-funktionspipelines](./overview.md) för att göra det möjligt att använda Python-anteckningsböcker som används i det här AI/ML-användningsförloppet.

## Bärbara anteckningsböcker för maskininlärningsmiljö i molnet {#cmle-notebooks}

Arbetsflödet från början till slut kan delas in i tre stora faser baserat på de tjänster som används för att implementera arbetsflödet.

- Initial utforskning och förberedelse av plattformsdata bygger på plattformstjänster.
- Modellutbildning och poängsättning utnyttjar verktygen i din molnbaserade ML-miljö. Vanliga alternativ för ML-plattformar är: Databricks ML, AWS Sagemaker, DataRobot och så vidare.
- Om ni samlar in poäng på nytt i Platform och alla kodbaserade målgrupper som skapats och aktiverats baserat på poängen, skulle ni åter förlita er på plattformstjänster.

Alla dessa faser kan dock köras i en eller flera bärbara datorer från din ML-miljö utan att användaren behöver växla mellan olika plattformar och deras molnbaserade ML-verktyg.

De typiska stegen i det här kompletta flödet har delats upp i en uppsättning modulära bärbara datorer som tillsammans demonstrerar de steg som ingår i ett typiskt maskininlärningsprojekt som inbegriper plattformsdata. Detta gör det enklare att använda bärbara datorer som referens för att implementera specifika aktiviteter och att välja och anpassa kod från relevanta bärbara datorer för att implementera ett verkligt användningsexempel. I praktiken kan en datavetare ta fram en enda bärbar dator som implementerar hela rörledningen för sitt ML-projekt. En datavetare kan också helt enkelt anpassa exempelkoden för att fråga efter plattformsdata och göra den tillgänglig i sin XML-miljö innan projektet fortsätter att använda gränssnittsbaserade funktioner i sin ML-plattform.

De exempel på anteckningsböcker som ingår i den länkade databasen beskrivs kort nedan. Detaljerad dokumentation för varje anteckningsbok är inbäddad med koden i själva anteckningsböckerna.

<!-- Below is the meat - the how to (but without links or details) -->

### Generera syntetiska data {#generate-synthetic-data}

Den här anteckningsboken innehåller kod för att generera datauppsättningar med syntetiska profiler och Experience Events i plattformen som ska användas som exempel på CMLE-arbetsflödet.

### EDA och funktioner med Query Service {#eda-and-featurization-with-query-service}

Den här anteckningsboken innehåller exempel på experimentell analys av plattformsdatauppsättningar med hjälp av interaktiva frågor via plattformsfrågetjänsten. Dessa följs av exempel på funktionsfrågor för att skapa en utbildningsdatauppsättning för exemplet på benägenhetsmodell.

### Exportera utbildningsdata {#export-training-data}

Den här anteckningsboken illustrerar export av utbildningsdata till molnlagring som kan läsas av dina ML-verktyg.

### Tåget är av en benägenhetsmodell {#train-a-propensity-model}

Den här anteckningsboken illustrerar utbildning av en benägenhetsmodell. Den förutsätter att XML-data för databaser används som din ML-miljö, men den skrivs i allmänhet (dvs. utan omfattande användning av databasspecifika funktioner/API:er) så att den kan anpassas till andra plattformar.

### Visa benägenhetsmodellen

Den här bärbara datorn visar hur man betygsätter den tränade benägenhetsmodellen för att ta fram en datauppsättning med benägenhetspoäng för varje plattformskundprofil.

### Ingest scores to AEP

Den här korta anteckningsboken illustrerar hur man hämtar data om benägenhetspoängen för att berika kundprofilerna i AEP.

### Skapa och aktivera målgrupper från kod

Den här anteckningsboken visar hur användaren kan skapa målgrupper utifrån poängen och aktivera dessa målgrupper via plattformsappar från sin anteckningsbokskod.
