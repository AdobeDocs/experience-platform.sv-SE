---
keywords: Experience Platform;maskininlärningsmodell;Data Science Workspace;populära ämnen;skapa och publicera en modell
solution: Experience Platform
title: Skapa och Publish en Machine Learning-modell
type: Tutorial
description: I följande guide beskrivs de steg som krävs för att skapa och publicera en maskininlärningsmodell.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 0%

---


# Skapa och publicera en maskininlärningsmodell

I följande guide beskrivs de steg som krävs för att skapa och publicera en maskininlärningsmodell. Varje avsnitt innehåller en beskrivning av vad du ska göra och en länk till användargränssnittet och API-dokumentationen för att utföra det beskrivna steget.

## Komma igång

Innan du startar den här självstudiekursen måste du ha följande krav:

- Åtkomst till [!DNL Adobe Experience Platform]. Om du inte har åtkomst till en organisation i [!DNL Experience Platform], ska du tala med systemadministratören innan du fortsätter.

- Alla Workspace självstudiekurser för datavetenskap använder Lumas benägenhetsmodell. För att kunna följa med i utvecklingen måste du ha skapat [Luma-profilmodellscheman och datauppsättningar](./create-luma-data.md).

### Utforska data och förstå scheman

Logga in på [Adobe Experience Platform](https://platform.adobe.com/) och välj **[!UICONTROL Datasets]** om du vill visa alla befintliga datauppsättningar och välja den datauppsättning som du vill utforska. I det här fallet bör du välja datamängden **Luma-webbdata**.

![välj Luma-webbdatauppsättning](../images/models-recipes/model-walkthrough/luma-dataset.png)

Sidan för datauppsättningsaktivitet öppnas med information om datauppsättningen. Du kan välja **[!UICONTROL Preview Dataset]** nära det övre högra hörnet för att undersöka exempelposter. Du kan även visa schemat för den valda datauppsättningen.

![Förhandsgranska Luma-webbdata](../images/models-recipes/model-walkthrough/preview-dataset.png)

Markera schemalänken i den högra listen. En pover visas. Om du väljer länken under **[!UICONTROL schema name]** öppnas schemat på en ny flik.

![förhandsgranska luma-webbdataschemat](../images/models-recipes/model-walkthrough/preview-schema.png)

Du kan utforska data ytterligare med den tillhandahållna EDA-anteckningsboken (Exploratory Data Analysis). Den här anteckningsboken kan användas för att förstå mönster i Luma-data, kontrollera datavården och sammanfatta relevanta data för den prediktiva benägenhetsmodellen. Om du vill veta mer om Analys av experimentella data kan du gå till [EDA-dokumentationen](../jupyterlab/eda-notebook.md).

## Skapa receptet för lumabenägenhet {#author-your-model}

En huvudkomponent i livscykeln [!DNL Data Science Workspace] innefattar att skapa recept och modeller. Lumatbenägenhetsmodellen är utformad för att generera en prognos över om kunderna har en hög benägenhet att köpa en produkt från Luma.

Om du vill skapa en Luma-benägenhetsmodell används mallen recept builder. Recept är grunden för en modell eftersom de innehåller algoritmer för maskininlärning och logik som utformats för att lösa specifika problem. Viktigast av allt är att Recipes ger er möjlighet att demokratisera maskininlärningen i hela organisationen så att andra användare kan komma åt en modell för olika användningsområden utan att behöva skriva någon kod.

Följ självstudiekursen [Skapa en modell med JupyterLab Notebooks](../jupyterlab/create-a-model.md) för att skapa det Luma-receptrecept som används i efterföljande självstudiekurser.

## Importera och paketera ett recept från externa källor (*valfritt*)

Om du vill importera och paketera ett recept som ska användas i Data Science Workspace måste du paketera källfilerna i en arkivfil. Följ [paketets källfiler i en recept](./package-source-files-recipe.md)-självstudie. I den här självstudiekursen får du lära dig att paketera källfiler i ett recept, vilket är ett nödvändigt steg för att importera ett recept till Data Science Workspace. När självstudiekursen är klar får du en dockningsbild i ett Azure-behållarregister tillsammans med motsvarande bild-URL, med andra ord en arkivfil.

Den här arkivfilen kan användas för att skapa ett recept i Data Science Workspace genom att följa arbetsflödet för receptimportimport med hjälp av [gränssnittsarbetsflödet](./import-packaged-recipe-ui.md) eller [API-arbetsflödet](./import-packaged-recipe-api.md).

## Utbildning och utvärdering av modell {#train-and-evaluate-your-model}

Nu när dina data är förberedda och ett recept är klart kan du skapa, utbilda och utvärdera din maskininlärningsmodell ytterligare. När du använder Recipe Builder bör du ha utbildat dig, fått poäng och utvärderat din modell innan du paketerar den i ett recept.

Med användargränssnittet och API för datavetenskap kan du publicera ditt recept som en modell. Dessutom kan du finjustera specifika aspekter av modellen ytterligare, t.ex. lägga till, ta bort och ändra hyperparametrar.

### Skapa en modell

Om du vill veta mer om hur du skapar en modell med hjälp av användargränssnittet kan du gå till tåget och utvärdera en modell i Data Science Workspace [UI-självstudiekurs](./train-evaluate-model-ui.md) eller [API-självstudiekurs](./train-evaluate-model-api.md). I den här självstudiekursen får du ett exempel på hur du skapar, utbildar och uppdaterar hyperparametrar för att finjustera modellen.

>[!NOTE]
>
> Det går inte att lära sig hyperparametrar, och de måste därför tilldelas innan utbildning kan genomföras. Om du justerar hyperparametrar kan du få en större noggrannhet i den tränade modellen. Eftersom det är en iterativ process att optimera en modell kan det krävas flera kurser innan en tillfredsställande utvärdering kan göras.

## Posta en modell {#score-a-model}

Nästa steg på vägen mot att skapa och publicera en modell är att driftsätta modellen för att få kunskap om datarjön och kundprofil i realtid.

Med datavetenskap kan Workspace uppnå poäng genom att mata in data i en befintlig utbildad modell. Resultat av poängsättningen lagras och kan visas i en angiven utdatamängd som en ny grupp.

Om du vill veta hur du kan göra en modellpoäng kan du gå till en [gränssnittssjälvstudiekurs](./score-model-ui.md) eller [API-självstudiekurs](./score-model-api.md).

## Publish en poängsatt modell som en tjänst

Med Data Science Workspace kan du publicera din tränade modell som en tjänst. Detta gör det möjligt för användare i organisationen att få fram data utan att behöva skapa egna modeller.

Om du vill lära dig hur du publicerar en modell som en tjänst kan du gå till [självstudiekursen för användargränssnitt](./publish-model-service-ui.md) eller [API-självstudiekursen](./publish-model-service-api.md).

### Schemalägg automatiserad utbildning för en tjänst

När du har publicerat en modell som en tjänst kan du konfigurera schemalagda poängsättnings- och utbildningskörningar för maskininlärningstjänsten. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster. Gå till [schemat för en modell i självstudiekursen för datavetenskap i Workspace](./schedule-models-ui.md).

>[!NOTE]
>
> Du kan bara schemalägga en modell för automatiserad utbildning och poängsättning från användargränssnittet.

## Nästa steg {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] innehåller verktyg och resurser för att skapa, utvärdera och använda maskininlärningsmodeller för att generera dataprognoser och insikter. När maskininlärningsinsikter hämtas in till en [!DNL Profile]-aktiverad datauppsättning, hämtas samma data även som [!DNL Profile]-poster som sedan kan segmenteras med [!DNL Adobe Experience Platform Segmentation Service].

När data från profil- och tidsserier hämtas bestämmer kundprofilen i realtid automatiskt att inkludera eller exkludera data från segment genom en pågående process som kallas direktuppspelningssegmentering, innan den sammanfogas med befintliga data och unionsvyn uppdateras. Resultatet blir att ni omedelbart kan utföra beräkningar och fatta beslut för att leverera förbättrade, individanpassade upplevelser till kunderna när de interagerar med ert varumärke.

Gå till självstudiekursen för [att förbättra kundprofilen i realtid med maskininlärningsinsikter](./enrich-profile.md) om du vill veta mer om hur du kan använda maskininlärningsinsikter.
