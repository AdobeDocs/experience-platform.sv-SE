---
title: AI/ML-arbetsflöde för dataöverföring från början till slut
description: Använd molnbaserade bärbara datorer för maskininlärningsmiljö för att skapa en kursmodell och betygsmodell som förutser prenumerationskonverteringar från Adobe Experience Platform-data.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '632'
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

Det här dokumentet innehåller en serie molnbaserade anteckningsböcker för maskininlärningsmiljö som demonstrerar ett komplett arbetsflöde. Arbetsflödet använder de maskininlärningsverktyg du föredrar för att skapa anpassade datamodeller som stöder dina användningsfall för marknadsföring med Experience Platform-data.

Det här arbetsflödet kräver att [!DNL Python] anteckningsböcker används i maskininlärningsmiljöer. Instruktioner för hur du kommer igång med de här [!DNL Python] anteckningsböckerna finns i deras respektive Viktigt-filer.

Innan du fortsätter med den här guiden följer du de steg som beskrivs i översikten över [AI/ML-funktionens pipelines](./overview.md) för att aktivera användningen av exempelfilen för Python-anteckningsböcker som används i det här användningsexemplet för AI/ML-funktionen.

## Bärbara anteckningsböcker för maskininlärningsmiljö i molnet {#cmle-notebooks}

Arbetsflödet från början till slut kan delas in i tre stora faser baserat på de tjänster som används för att implementera arbetsflödet.

- Utforska och förbereda Experience Platform-data i början av Experience Platform.
- Modellutbildning och poängsättning utnyttjar verktygen i din molnbaserade ML-miljö. Vanliga alternativ för ML-plattformar är: Databricks ML, AWS Sagemaker, DataRobot och så vidare.
- Om ni lägger in resultat i Experience Platform och skapar och aktiverar ni kodbaserat målgruppsanpassning baserat på poängen är Experience Platform tjänster fortfarande till godo.

Alla dessa faser kan dock köras i en eller flera bärbara datorer från din ML-miljö utan att användaren behöver växla mellan Experience Platform och deras molnbaserade ML-verktyg.

De typiska stegen i det här kompletta flödet har delats upp i en uppsättning modulära bärbara datorer som tillsammans demonstrerar de steg som ingår i ett typiskt maskininlärningsprojekt som inbegriper Experience Platform-data. Detta gör det enklare att använda bärbara datorer som referens för att implementera specifika aktiviteter och att välja och anpassa kod från relevanta bärbara datorer för att implementera ett verkligt användningsexempel. I praktiken kan en datavetare ta fram en enda bärbar dator som implementerar hela rörledningen för sitt ML-projekt. Alternativt kan en datavetare helt enkelt anpassa exempelkoden för att fråga efter Experience Platform-data och göra den tillgänglig i sin XML-miljö innan han eller hon fortsätter att använda gränssnittsbaserade funktioner i sin ML-plattform.

De exempel på anteckningsböcker som ingår i den länkade databasen beskrivs kort nedan. Detaljerad dokumentation för varje anteckningsbok är inbäddad med koden i själva anteckningsböckerna.

<!-- Below is the meat - the how to (but without links or details) -->

### Generera syntetiska data {#generate-synthetic-data}

Den här anteckningsboken innehåller kod för generering av datauppsättningar med syntetiska profiler och Experience Events i din Experience Platform som ska användas för att illustrera CMLE-arbetsflödet.

### EDA och funktioner med Query Service {#eda-and-featurization-with-query-service}

Den här anteckningsboken innehåller exempel på experimentell analys av Experience Platform-datauppsättningar med interaktiva frågor via Experience Platform Query Service. Dessa följs av exempel på funktionsfrågor för att skapa en utbildningsdatauppsättning för exemplet på benägenhetsmodell.

### Exportera utbildningsdata {#export-training-data}

Den här anteckningsboken illustrerar export av utbildningsdata till molnlagring som kan läsas av dina ML-verktyg.

### Tåget är av en benägenhetsmodell {#train-a-propensity-model}

Den här anteckningsboken illustrerar utbildning av en benägenhetsmodell. Den förutsätter att XML-data för databaser används som din ML-miljö, men den skrivs i allmänhet (dvs. utan omfattande användning av databasspecifika funktioner/API:er) så att den kan anpassas till andra plattformar.

### Visa benägenhetsmodellen

Den här bärbara datorn visar hur man betygsätter den tränade benägenhetsmodellen för att ta fram en datauppsättning med benägenhetspoäng för varje Experience Platform-kundprofil.

### Ingest scores to AEP

Den här korta anteckningsboken illustrerar hur man hämtar data om benägenhetspoängen för att berika kundprofilerna i AEP.

### Skapa och aktivera målgrupper från kod

Den här anteckningsboken illustrerar hur användaren kan skapa målgrupper utifrån poängen och aktivera dessa målgrupper via Experience Platform-appar från sin anteckningsbokskod.
