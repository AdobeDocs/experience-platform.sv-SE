---
keywords: Experience Platform;utbilda och utvärdera;Data Science Workspace;populära ämnen;skapa en modell;skapa en utbildningskurs
solution: Experience Platform
title: Utbildning och utvärdering av en modell i användargränssnittet för datavetenskap
topic: tutorial
type: Tutorial
description: I Adobe Experience Platform Data Science Workspace skapas en maskininlärningsmodell genom att en befintlig Recipe som är lämplig för modellens avsikt läggs till. Modellen är sedan utbildad och utvärderad för att optimera dess driftseffektivitet och effektivitet genom att finjustera de tillhörande hyperparametrarna. Recept kan återanvändas, vilket innebär att flera modeller kan skapas och skräddarsys för specifika syften med en enda Recept.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 1%

---


# Utbilda och utvärdera en modell i användargränssnittet för datavetenskap

I Adobe Experience Platform Data Science Workspace skapas en maskininlärningsmodell genom att en befintlig Recipe som är lämplig för modellens avsikt läggs till. Modellen är sedan utbildad och utvärderad för att optimera dess driftseffektivitet och effektivitet genom att finjustera de tillhörande hyperparametrarna. Recept kan återanvändas, vilket innebär att flera modeller kan skapas och skräddarsys för specifika syften med en enda Recept.

Den här självstudiekursen går igenom stegen för att skapa, utbilda och utvärdera en modell.

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform] för att kunna slutföra den här självstudiekursen. Om du inte har tillgång till en IMS-organisation i [!DNL Experience Platform], ska du tala med systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig recept. Om du inte har någon recept följer du [Importera en paketerad recept i självstudiekursen för användargränssnittet](./import-packaged-recipe-ui.md) innan du fortsätter.

## Skapa en modell

1. I Adobe Experience Platform klickar du på länken **[!UICONTROL Models]** i den vänstra navigeringskolumnen för att visa alla befintliga modeller. Klicka på **[!UICONTROL Create Model]** uppe till höger på sidan för att påbörja en modellskapandeprocess.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Bläddra igenom listan med befintliga recept, sök efter och välj den Recept som ska användas för att skapa modellen och klicka på **[!UICONTROL Next]**.
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. Välj en lämplig indatauppsättning och klicka på **[!UICONTROL Next]**. Detta anger standarddatauppsättningen för inmatningsutbildning för modellen.
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. Ange ett namn för modellen och granska standardmodellkonfigurationerna. Standardkonfigurationer tillämpades när Recept skapades, granska och ändra konfigurationsvärdena genom att dubbelklicka på värdena. Om du vill skapa en ny uppsättning konfigurationer klickar du på **[!UICONTROL Upload New Config]** och drar en JSON-fil som innehåller modellkonfigurationer till webbläsarfönstret. Klicka på **[!UICONTROL Finish]** för att skapa modellen.

   >[!NOTE]
   >
   >Konfigurationer är unika och specifika för den avsedda mottagaren, vilket innebär att konfigurationer för butiksförsäljningsreceptet inte fungerar för produktmottagaren för Recommendations. I [referensavsnittet](#reference) finns en lista över konfigurationer för Retail Sales Recipe.

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Skapa en utbildningskörning

1. I Adobe Experience Platform klickar du på länken **[!UICONTROL Models]** i den vänstra navigeringskolumnen för att visa alla befintliga modeller. Sök och klicka på namnet på den modell som ska tränas.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Alla befintliga kurser med deras aktuella utbildningsstatus listas. För modeller som skapats med användargränssnittet [!DNL Data Science Workspace] skapas och körs en utbildningskörning automatiskt med standardkonfigurationer och datauppsättningen för inmatningsutbildning.
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. Skapa en ny kurs genom att klicka på **[!UICONTROL Train]** uppe till höger på sidan Modellöversikt.
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. Välj indatauppsättning för utbildning för kursen och klicka på **[!UICONTROL Next]**.
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. Standardkonfigurationer som tillhandahålls när modellen skapas visas, ändra och ändra dem därefter genom att dubbelklicka på värdena. Klicka på **[!UICONTROL Finish]** för att skapa och köra kursen.

   >[!NOTE]
   >
   >Konfigurationer är unika och specifika för den avsedda mottagaren, vilket innebär att konfigurationer för butiksförsäljningsreceptet inte fungerar för produktmottagaren för Recommendations. I [referensavsnittet](#reference) finns en lista över konfigurationer för Retail Sales Recipe.

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## Utvärdera modellen

1. I Adobe Experience Platform klickar du på länken **[!UICONTROL Models]** i den vänstra navigeringskolumnen för att visa alla befintliga modeller. Sök och klicka på namnet på den modell som ska utvärderas.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Alla befintliga kurser med deras aktuella utbildningsstatus listas. Om du har flera färdiga kurser kan du jämföra utvärderingsmätningar för olika utbildningar i modellutvärderingsdiagrammet. Välj ett utvärderingsmått i listrutan ovanför diagrammet.

   MAPE-mätvärdet (Meean Absolute Percent Error) anger noggrannheten som en procentandel av felet. Detta används för att identifiera de mest högpresterande experterna. Ju lägre värde, desto bättre.

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   Precisionsmåttet beskriver procentandelen relevanta instanser jämfört med det totala antalet *hämtade*-instanser. Precision kan ses som sannolikheten att ett slumpmässigt valt resultat blir korrekt.
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   Klicka på en särskild övning för att se mer information om den körningen. Detta kan göras även innan körningen har slutförts. På detaljsidan kan du se andra utvärderingsmått, konfigurationsparametrar och visualiseringar som är specifika för kursen. Du kan även hämta aktivitetsloggar för att se information om körningen. Loggar är särskilt användbara för misslyckade körningar för att se vad som gick fel.
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. Hyperparametrar kan inte tränas och en modell måste optimeras genom att olika kombinationer av hyperparametrar testas. Upprepa denna modellutbildning och utvärderingsprocess tills du har nått en optimerad modell.

## Nästa steg

I den här självstudiekursen steg du igenom när du skapade, utbildade och utvärderade en modell i [!DNL Data Science Workspace]. När du har nått fram till en optimerad modell kan du använda den utbildade modellen för att generera insikter genom att följa självstudiekursen [Score a Model i användargränssnittet](./score-model-ui.md).

## Referens {#reference}

### Detaljhandelsförsäljningens mottagarkonfigurationer

Hyperparametrar bestämmer modellens utbildningsbeteende, och om du ändrar hyperparametrar påverkas modellens precision och precision:

| Hyperparameter | Beskrivning | Rekommenderat intervall |
--- | --- | ---
| learning_rate | Inlärningsgraden minskar bidraget från varje träd med learning_rate. Det finns en kompromiss mellan learning_rate och n_estimators. | 0.1 | [2 - 10] / antal uppskattare |
| n_estimators | Antalet förstärkningssteg som ska utföras. Ökning av övertoningar är relativt robust för överpassning, så ett stort tal ger vanligtvis bättre prestanda. | 100 | 100 - 1000 |
| max_depth | Maximalt djup för de enskilda regressionsberäknarna. Det maximala djupet begränsar antalet noder i trädet. Finjustera den här parametern för bästa prestanda. det bästa värdet beror på interaktionen mellan indatavariablerna. | 3 | 4 - 10 |

Ytterligare parametrar bestämmer modellens tekniska egenskaper:

| Parameternyckel | Typ | Beskrivning |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Sträng | Lista med kommaavgränsade inmatningsschemaattribut. |
| `ACP_DSW_TARGET_FEATURES` | Sträng | Lista med kommaseparerade utdataschemaattribut. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolean | Avgör om in- och utdatafunktionerna kan ändras |
| `tenantId` | Sträng | Detta ID garanterar att de resurser du skapar namnges korrekt och finns i IMS-organisationen. [Följ stegen ](../../xdm/api/getting-started.md#know-your-tenant_id) här för att hitta ditt klient-ID. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Sträng | Det indatarema som används för utbildning av en modell. |
| `evaluation.labelColumn` | Sträng | Kolumnetikett för utvärderingsvisualiseringar. |
| `evaluation.metrics` | Sträng | Kommaavgränsad lista med mätvärden som ska användas för att utvärdera en modell. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Sträng | Utdatamodeller som används för att klassificera en modell. |