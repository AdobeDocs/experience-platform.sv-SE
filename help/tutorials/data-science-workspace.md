---
keywords: Experience Platform;hem;populära ämnen;dsw;DSW
solution: Experience Platform
title: Självstudiekurser för datavetenskap
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---


# Självstudiekurser om [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. [!DNL Data Science Workspace] är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med ert innehåll och era dataresurser över alla Adobe-lösningar. Datavetare på alla kunskapsnivåer har sofistikerade, lättanvända verktyg som stöder snabb utveckling, utbildning och anpassning av maskininlärningsrecepten - alla fördelarna med AI-tekniken, utan komplexiteten.

Börja med att läsa översikten [Datavetenskapens arbetsyta](../data-science-workspace/home.md) om du vill veta mer.

## [!DNL Sensei Machine Learning] API

Med API:t [!DNL Sensei Machine Learning] kan datavetare ordna och hantera maskininlärningstjänster, från algoritmintroduktion till experimenterande och till driftsättning.

**Följande API-utvecklarhandböcker är tillgängliga:**
- [Motorer](../data-science-workspace/api/engines.md)  - Lär dig hur du hittar i  [!DNL Docker] registret, skapar en motor, skapar en rörlig motor för funktioner, hämtar information för en motor, uppdaterar en motor och tar bort en motor.
- [MLInstances (recept)](../data-science-workspace/api/mlinstances.md)  - Lär dig hur du skapar en MLInstance, hämtar information för en MLInstance, uppdaterar en MLInstance och tar bort en MLInstance.
- [Experimentera](../data-science-workspace/api/experiments.md)  - Lär dig hur du skapar en expert, hämtar en Experiment eller Experiment kör information, uppdaterar en Experiment och tar bort en Experiment.
- [Modeller](../data-science-workspace/api/models.md)  - Lär dig hur du registrerar din egen modell, hämtar information för en modell, uppdaterar en modell, tar bort en modell, skapar en ny omkodning för en modell och hämtar information om en omkodad modell.
- [MLServices](../data-science-workspace/api/mlservices.md)  - Lär dig hur du skapar en MLService, hämtar information för en MLService, uppdaterar en MLService och tar bort en MLService.
- [Insikter](../data-science-workspace/api/insights.md)  - Lär dig hur du hämtar information för en Insight, lägger till en ny Model Insight och hämtar en lista med standardvärden för algoritmer.

Om du vill veta mer och få de värden som krävs för att utföra CRUD-åtgärder med API:t Sensei Machine Learning går du till [guiden ](../data-science-workspace/api/getting-started.md) Komma igång.

## Använda [!DNL JupyterLab] bärbara datorer

[!DNL JupyterLab] är ett webbaserat användargränssnitt för  [!DNL Project Jupyter] och är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö för datavetare som kan arbeta med [!DNL Jupyter Notebooks], kod och data. Det här dokumentet innehåller en översikt över [!DNL JupyterLab] och dess funktioner samt instruktioner om hur du utför vanliga åtgärder.

**Den här guiden hjälper dig att:**
- Få åtkomst till och förstå [!DNL JupyterLab]-gränssnittet.
- Förstå kodceller och tillgängliga kärnor i [!DNL JupyterLab].
- Förstå GPU- och minnesserverkonfigurationen i [!DNL Python]/R.

Mer information finns i [användarhandboken för JupyterLab](../data-science-workspace/jupyterlab/overview.md).

## Dataåtkomst i JupyterLab-anteckningsböcker

JupyterLab i Data Science Workspace har för närvarande stöd för anteckningsböcker för [!DNL Python], R, PySpark och Scala. Varje kärna som stöds har inbyggda funktioner som gör att du kan läsa plattformsdata från en datamängd i en anteckningsbok. Stöd för sidnumrering av data är dock begränsat till bärbara [!DNL Python]- och R-datorer. Den här guiden fokuserar på hur du använder JupyterLab-anteckningsböcker för att få tillgång till dina data.

**Den här guiden hjälper dig att:**
- Läs, skriv och fråga plattformsdata med hjälp av de bärbara datorerna Python, R, PySpark och Scala.
- Förstå läsbegränsningarna för alla typer av bärbara datorer.

Mer information finns i [Utvecklarhandboken för JupyterLab-dataåtkomst för bärbara datorer](../data-science-workspace/jupyterlab/access-notebook-data.md)

## Paketera källfiler för redigering av [!DNL Docker]-recept

Med en [!DNL Docker]-bild kan du paketera ett program med alla delar den behöver. Detta inkluderar bibliotek och andra beroenden i ett och samma paket. Den skapade [!DNL Docker]-bilden överförs till [!DNL Azure Container Registry] med de autentiseringsuppgifter som du får när du skapar recept.

**Den här självstudiekursen hjälper dig att:**
- Ladda ned nödvändiga förutsättningar för att skapa recept.
- Förstå [!DNL Docker]-baserad modellutveckling.
- Skapa en [!DNL Docker]-bild för [!DNL Python], R, PySpark eller Scala ([!DNL Spark]).
- Hämta en URL för källfilen [!DNL Docker].

Om du vill veta mer kan du följa [paketets källfiler i en recept-självstudiekurs](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Importera ett recept

>[!NOTE]
>
>I den här självstudiekursen måste du ha en [!DNL Docker]-källfils-URL. Besök [paketets källfiler i en självstudiekurs](../data-science-workspace/models-recipes/package-source-files-recipe.md) om du inte har en [!DNL Docker]-källfils-URL.

Självstudiekurserna för importrecept ger insikter om hur du konfigurerar och importerar ett paketerat recept. I slutet av den här självstudiekursen kan du skapa, utbilda och utvärdera en modell i Adobe Experience Platform [!DNL Data Science Workspace].

**Den här självstudiekursen hjälper dig att:**
- Skapa en uppsättning konfigurationer för ett recept.
- Importera ett [!DNL Docker]-baserat recept för [!DNL Python], R, PySpark eller Scala ([!DNL Spark]).

Om du vill veta mer kan du följa självstudiekursen [för import av ett paketerat recept](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) eller självstudiekursen [API](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Utbildning och utvärdering av modell

I Adobe Experience Platform [!DNL Data Science Workspace] skapas en maskininlärningsmodell genom att en befintlig Recipe som är lämplig för modellens avsikt inkluderas. Modellen är sedan utbildad och utvärderad för att optimera dess driftseffektivitet och effektivitet genom att finjustera de tillhörande hyperparametrarna. Recept kan återanvändas, vilket innebär att flera modeller kan skapas och skräddarsys för specifika syften med en enda Recept.

**Den här självstudiekursen hjälper dig att:**
- Skapa en ny modell.
- Skapa en utbildningskurs för din modell.
- Utvärdera din modellutbildning.

Kom igång genom att följa kursen och utvärdera en modell [API-självstudiekurs](../data-science-workspace/models-recipes/train-evaluate-model-api.md) eller [användargränssnittet](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Optimera en modell med Model Insights-ramverket

Model Insights Framework ger datavetenskaparen verktyg i Adobe Experience Platform [!DNL Data Science Workspace] för att göra snabba och välgrundade val för optimala maskininlärningsmodeller baserade på experiment. Ramverket kommer att förbättra snabbheten och effektiviteten i maskininlärningsarbetsflödet samt förbättra användarvänligheten för datavetare. Det gör du genom att ange en standardmall för varje maskininlärningsalgoritmtyp som ska vara till hjälp vid modelljustering. Slutresultatet gör att datavetare och datavetare kan fatta bättre modelloptimeringsbeslut för sina slutkunder.

**Den här självstudiekursen hjälper dig att:**
- Konfigurera receptkod.
- Definiera anpassade mätvärden.
- Använd fördefinierade mätvärden och visualiseringsdiagram.

Kom igång genom att följa självstudiekursen [optimera en modell](../data-science-workspace/models-recipes/optimize-model.md).

## Posta en modell

Du kan göra poängsättningen i Adobe Experience Platform [!DNL Data Science Workspace] genom att mata in indata i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp.

**Den här självstudiekursen hjälper dig att:**
- Skapa en ny poängkörning.
- Visa dina poängresultat.

Kom igång genom att följa poängen i en modell [API-självstudiekurs](../data-science-workspace/models-recipes/score-model-api.md) eller [gränssnittsjälvstudiekursen](../data-science-workspace/models-recipes/score-model-ui.md).

## Publicera en modell som en tjänst

Med Adobe Experience Platform [!DNL Data Science Workspace] kan du publicera din modell som en tjänst, så att användare i din IMS-organisation kan få sina data poäng utan att behöva skapa egna modeller. Detta kan du göra med användargränssnittet [!DNL Platform] eller API:t [!DNL Sensei Machine Learning].

**Den här självstudiekursen hjälper dig att:**
- Publicera en modell som en tjänst.
- Posta data med en tjänst via [!DNL Platform] [!UICONTROL Service Gallery].

Kom igång genom att följa självstudiekursen för att publicera en modell som en tjänst [API](../data-science-workspace/models-recipes/publish-model-service-api.md) eller [användargränssnittet](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Boka utbildning och poängsättning för en modell

Med Adobe Experience Platform [!DNL Data Science Workspace] kan du konfigurera schemalagda poängsättnings- och utbildningar för en maskininlärningstjänst. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster.

**Den här självstudiekursen hjälper dig att:**
- Konfigurera schemalagd poängsättning
- Konfigurera schemalagd utbildning

Kom igång genom att följa självstudiekursen [för att schemalägga en modell för användargränssnitt](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Skapa en funktionspipeline

>[!NOTE]
>
>För närvarande är funktionspipelinjer bara tillgängliga via API.

Med Adobe Experience Platform kan du skapa och skapa anpassade rörledningar för funktioner som kan användas i stor skala via [!DNL Sensei Machine Learning Framework Runtime].

**Den här guiden hjälper dig att:**
- Implementera rörlighetsklasser för funktioner.
- Skapa en rörlig funktionsmotor med API:t.

Mer information finns i självstudiekursen för [hur du skapar en funktionspipeline](../data-science-workspace/authoring/feature-pipeline.md).

## Skapa ett [!DNL Real-Time Machine Learning]-program (alfa)

En kombination av sömlös beräkning på både hubben och [!DNL Edge] minskar dramatiskt den latens som traditionellt används för att driva hyperpersonaliserade upplevelser som är både relevanta och responsiva. [!DNL Real-time Machine Learning] ger därför en otroligt låg fördröjning för synkront beslutsfattande. Exempel är återgivning av anpassat webbsidesinnehåll, visning av ett erbjudande och rabatter som minskar bortfallet samtidigt som konverteringsgraden ökar i en webbutik.

**Den här guiden hjälper dig att:**
- Förstå [!DNL Real-time Machine Learning]-arkitekturen.
- Förstå arbetsflödet för [!DNL Real-time Machine Learning].
- Förstå den aktuella funktionaliteten för [!DNL Real-time Machine Learning].
- Ange nästa steg för att skapa en egen [!DNL Real-time Machine Learning model].

Mer information finns i [maskininlärningsöversikt i realtid](../data-science-workspace/real-time-machine-learning/home.md).