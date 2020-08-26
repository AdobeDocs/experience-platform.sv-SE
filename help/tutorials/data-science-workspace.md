---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Självstudiekurser för datavetenskap
topic: tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 0%

---


# Självstudiekurser om [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Integrerat i Adobe Experience Platform och [!DNL Data Science Workspace] gör det enklare att förutse hur ni använder ert innehåll och era datatillgångar i olika Adobe-lösningar. Datavetare på alla kunskapsnivåer har sofistikerade, lättanvända verktyg som stöder snabb utveckling, utbildning och anpassning av maskininlärningsrecepten - alla fördelarna med AI-tekniken, utan komplexiteten.

Börja med att läsa översikten över arbetsytan för [datavetenskap](../data-science-workspace/home.md)om du vill veta mer.

## [!DNL Sensei Machine Learning] API

API:t [!DNL Sensei Machine Learning] tillhandahåller en mekanism för datavetare som organiserar och hanterar maskininlärningstjänster, från algoritmintroduktion till experimenterande och driftsättning.

**Följande API-utvecklarhandböcker är tillgängliga:**
- [Motorer](../data-science-workspace/api/engines.md) - Lär dig hur du hittar i ditt [!DNL Docker] register, skapar en motor, skapar en rörlig motor för funktioner, hämtar information för en motor, uppdaterar en motor och tar bort en motor.
- [MLInstances (recept)](../data-science-workspace/api/mlinstances.md) - Lär dig hur du skapar en MLInstance, hämtar information för en MLInstance, uppdaterar en MLInstance och tar bort en MLInstance.
- [Experimentera](../data-science-workspace/api/experiments.md) - Lär dig hur du skapar en expert, hämtar information från en expert eller en expert, uppdaterar en expert och tar bort en expert.
- [Modeller](../data-science-workspace/api/models.md) - Lär dig hur du registrerar din egen modell, hämtar information för en modell, uppdaterar en modell, tar bort en modell, skapar en ny omkodning för en modell och hämtar information om en omkodad modell.
- [MLServices](../data-science-workspace/api/mlservices.md) - Lär dig hur du skapar en MLService, hämtar information för en MLService, uppdaterar en MLService och tar bort en MLService.
- [Insikter](../data-science-workspace/api/insights.md) - Lär dig hur du hämtar information för en Insight, lägger till en ny Model Insight och hämtar en lista med standardvärden för algoritmer.

Om du vill veta mer och få de värden som krävs för att utföra CRUD-åtgärder med API:t Sensei Machine Learning går du till [Komma igång-guiden](../data-science-workspace/api/getting-started.md).

## How to use [!DNL JupyterLab] Notebooks

[!DNL JupyterLab] är ett webbaserat användargränssnitt för [!DNL Project Jupyter] och är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med [!DNL Jupyter notebooks], kod och data. Det här dokumentet innehåller en översikt över [!DNL JupyterLab] och dess funktioner samt instruktioner om hur du utför vanliga åtgärder.

**Den här guiden hjälper dig att:**
- Få åtkomst till och förstå [!DNL JupyterLab] gränssnittet.
- Förstå kodceller och tillgängliga kärnor i [!DNL JupyterLab].
- Förstå GPU- och minnesserverkonfiguration i [!DNL Python]/R.
- Läs och fråga efter [!DNL Platform] data med hjälp av anteckningsböcker.
- Förstå datagränserna för bärbara datorer.

Mer information finns i användarhandboken för [JupyterLab](../data-science-workspace/jupyterlab/overview.md).

## Paketera källfiler för [!DNL Docker] receptframtagning

Med en [!DNL Docker] bild kan du paketera ett program med alla delar som behövs. Detta inkluderar bibliotek och andra beroenden i ett och samma paket. Den inbyggda [!DNL Docker] bilden överförs till [!DNL Azure Container Registry] med hjälp av de inloggningsuppgifter som du får när du skapar recept.

**Den här självstudiekursen hjälper dig att:**
- Ladda ned nödvändiga förutsättningar för att skapa recept.
- Förstå [!DNL Docker] baserad modellutveckling.
- Skapa en [!DNL Docker] bild för [!DNL Python], R, PySpark eller Scala ([!DNL Spark]).
- Hämta en URL för [!DNL Docker] källfilen.

Om du vill veta mer kan du följa [paketets källfiler i en recept-självstudiekurs](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Importera ett recept

>[!NOTE]
>
>Den här självstudiekursen kräver att du har en URL för [!DNL Docker] källfilen. Besök [paketets källfiler i en recept-självstudiekurs](../data-science-workspace/models-recipes/package-source-files-recipe.md) om du inte har någon URL för [!DNL Docker] källfilen.

Självstudiekurserna för importrecept ger insikter om hur du konfigurerar och importerar ett paketerat recept. I slutet av den här självstudiekursen kan du skapa, utbilda och utvärdera en modell i Adobe Experience Platform [!DNL Data Science Workspace].

**Den här självstudiekursen hjälper dig att:**
- Skapa en uppsättning konfigurationer för ett recept.
- Importera ett [!DNL Docker] baserat recept för [!DNL Python], R, PySpark eller Scala ([!DNL Spark]).

Om du vill ha mer information kan du följa självstudiekursen för att importera ett paketerat [recept](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) eller [API-självstudiekursen](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Utbildning och utvärdering av modell

I Adobe Experience Platform [!DNL Data Science Workspace]skapas en maskininlärningsmodell genom att en befintlig Recipe som är lämplig för modellens avsikt läggs till. Modellen är sedan utbildad och utvärderad för att optimera dess driftseffektivitet och effektivitet genom att finjustera de tillhörande hyperparametrarna. Recept kan återanvändas, vilket innebär att flera modeller kan skapas och skräddarsys för specifika syften med en enda Recept.

**Den här självstudiekursen hjälper dig att:**
- Skapa en ny modell.
- Skapa en utbildningskurs för din modell.
- Utvärdera din modellutbildning.

Kom igång genom att följa kursen och utvärdera en [modell-API-självstudiekurs](../data-science-workspace/models-recipes/train-evaluate-model-api.md) eller [gränssnittsjälvstudiekursen](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Optimera en modell med Model Insights-ramverket

Model Insights Framework ger datavetenskaparna verktyg i Adobe Experience Platform [!DNL Data Science Workspace] för att göra snabba och välgrundade val för optimala maskininlärningsmodeller baserade på experiment. Ramverket kommer att förbättra snabbheten och effektiviteten i maskininlärningsarbetsflödet samt förbättra användarvänligheten för datavetare. Det gör du genom att ange en standardmall för varje maskininlärningsalgoritmtyp som ska vara till hjälp vid modelljustering. Slutresultatet gör att datavetare och datavetare kan fatta bättre modelloptimeringsbeslut för sina slutkunder.

**Den här självstudiekursen hjälper dig att:**
- Konfigurera receptkod.
- Definiera anpassade mätvärden.
- Använd fördefinierade mätvärden och visualiseringsdiagram.

Kom igång genom att följa självstudiekursen om hur du [optimerar en modell](../data-science-workspace/models-recipes/optimize-model.md).

## Posta en modell

Du kan göra poängsättningen i Adobe Experience Platform [!DNL Data Science Workspace] genom att mata in indata i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp.

**Den här självstudiekursen hjälper dig att:**
- Skapa en ny poängkörning.
- Visa dina poängresultat.

Kom igång genom att följa poängen i en [API-självstudiekurs](../data-science-workspace/models-recipes/score-model-api.md) eller i [användargränssnittets självstudiekurs](../data-science-workspace/models-recipes/score-model-ui.md).

## Publicera en modell som en tjänst

Med Adobe Experience Platform [!DNL Data Science Workspace] kan du publicera din modell som en tjänst, vilket gör att användare i IMS-organisationen kan få sina data poäng utan att behöva skapa egna modeller. Detta kan du göra med [!DNL Platform] användargränssnittet eller [!DNL Sensei Machine Learning] API:t.

**Den här självstudiekursen hjälper dig att:**
- Publicera en modell som en tjänst.
- Posta data med en tjänst via [!DNL Platform][!UICONTROL Service Gallery].

Kom igång genom att följa självstudiekursen [för publicering av en modell som en](../data-science-workspace/models-recipes/publish-model-service-api.md) tjänst-API eller [användargränssnittet](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Boka utbildning och poängsättning för en modell

Med Adobe Experience Platform [!DNL Data Science Workspace] kan du konfigurera schemalagda kurser i maskininlärning. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster.

**Den här självstudiekursen hjälper dig att:**
- Konfigurera schemalagd poängsättning
- Konfigurera schemalagd utbildning

Kom igång genom att följa självstudiekursen [för modellgränssnitt](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Skapa en funktionspipeline

>[!NOTE]
>
>För närvarande är funktionspipelinjer bara tillgängliga via API.

Med Adobe Experience Platform kan du skapa och skapa anpassade rörledningar för att utföra funktionstekniker i stor skala via [!DNL Sensei Machine Learning Framework Runtime].

**Den här guiden hjälper dig att:**
- Implementera rörlighetsklasser för funktioner.
- Skapa en rörlig funktionsmotor med API:t.

Mer information finns i självstudiekursen om hur du [skapar en introduktion](../data-science-workspace/authoring/feature-pipeline.md).

## Skapa ett [!DNL Real-Time Machine Learning] program (alfa)

En kombination av sömlös beräkning på både hubben och den [!DNL Edge] minskar dramatiskt den latens som traditionellt används för att skapa hyper-personaliserade upplevelser som är både relevanta och responsiva. Det innebär att [!DNL Real-time Machine Learning] ni kan dra slutsatser med otroligt låg latens för synkront beslutsfattande. Exempel är återgivning av anpassat webbsidesinnehåll, visning av ett erbjudande och rabatter som minskar bortfallet samtidigt som konverteringsgraden ökar i en webbutik.

**Den här guiden hjälper dig att:**
- Förstå [!DNL Real-time Machine Learning] arkitekturen.
- Förstå [!DNL Real-time Machine Learning] arbetsflödet.
- Förstå de aktuella funktionerna för [!DNL Real-time Machine Learning].
- Ange nästa steg för att skapa en egen [!DNL Real-time Machine Learning model].

Mer information finns i [Machine Learning-översikten](../data-science-workspace/real-time-machine-learning/home.md)i realtid.