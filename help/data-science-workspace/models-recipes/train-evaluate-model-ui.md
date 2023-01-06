---
keywords: Experience Platform;utbilda och utvärdera;Data Science Workspace;populära ämnen;skapa en modell;skapa en utbildningskurs
solution: Experience Platform
title: Utbildning och utvärdering av en modell i användargränssnittet för datavetenskap
type: Tutorial
description: I Adobe Experience Platform Data Science Workspace skapas en maskininlärningsmodell genom att en befintlig Recipe som är lämplig för modellens avsikt läggs till. Modellen är sedan utbildad och utvärderad för att optimera dess driftseffektivitet och effektivitet genom att finjustera de tillhörande hyperparametrarna. Recept kan återanvändas, vilket innebär att flera modeller kan skapas och skräddarsys för specifika syften med en enda Recept.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 1%

---

# Utbilda och utvärdera en modell i användargränssnittet för datavetenskap

I Adobe Experience Platform Data Science Workspace skapas en maskininlärningsmodell genom att en befintlig Recipe som är lämplig för modellens avsikt läggs till. Modellen är sedan utbildad och utvärderad för att optimera dess driftseffektivitet och effektivitet genom att finjustera de tillhörande hyperparametrarna. Recept kan återanvändas, vilket innebär att flera modeller kan skapas och skräddarsys för specifika syften med en enda Recept.

Den här självstudiekursen går igenom stegen för att skapa, utbilda och utvärdera en modell.

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform]. Om du inte har tillgång till en IMS-organisation i [!DNL Experience Platform]bör du kontakta systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig recept. Om du inte har någon recept följer du [Importera en paketerad mottagare i användargränssnittet](./import-packaged-recipe-ui.md) självstudiekurs innan du fortsätter.

## Skapa en modell

I Experience Platform väljer du **[!UICONTROL Models]** i den vänstra navigeringsrutan och välj sedan fliken Bläddra för att visa dina befintliga modeller. Välj **[!UICONTROL Create Model]** i det övre högra hörnet på sidan för att påbörja en modellskapandeprocess.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Bläddra igenom listan med befintliga mottagare, sök efter och välj den mottagare som ska användas för att skapa modellen och välj **[!UICONTROL Next]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Välj en lämplig indatauppsättning och välj **[!UICONTROL Next]**. Detta anger standarddatauppsättningen för inmatningsutbildning för modellen.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Ange ett namn för modellen och granska standardmodellkonfigurationerna. Standardkonfigurationer tillämpades när Recept skapades, granska och ändra konfigurationsvärdena genom att dubbelklicka på värdena.

Välj **[!UICONTROL Upload New Config]** och dra en JSON-fil som innehåller modellkonfigurationer till webbläsarfönstret. Välj **[!UICONTROL Finish]** för att skapa modellen.

>[!NOTE]
>
>Konfigurationer är unika och specifika för den avsedda mottagaren, vilket innebär att konfigurationer för butiksförsäljningsreceptet inte fungerar för produktmottagaren för Recommendations. Se [referens](#reference) för en lista över butiksförsäljningsmottagarkonfigurationer.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Skapa en utbildningskörning

I Experience Platform väljer du **[!UICONTROL Models]** i den vänstra navigeringsrutan och välj sedan fliken Bläddra för att visa dina befintliga modeller. Sök efter och välj den hyperlänk som är kopplad till namnet på den modell som du vill utbilda.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alla befintliga kurser med deras aktuella utbildningsstatus listas. För modeller som skapats med [!DNL Data Science Workspace] -användargränssnittet genereras och körs en utbildningskörning automatiskt med standardkonfigurationer och datauppsättningen för inmatningsutbildning.

Skapa en ny kurs genom att välja **[!UICONTROL Train]** nära överst till höger på sidan Modellöversikt.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Välj indatauppsättning för utbildning för kursen och välj sedan **[!UICONTROL Next]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Standardkonfigurationer som tillhandahålls när modellen skapas visas, ändra och ändra dem därefter genom att dubbelklicka på värdena. Välj **[!UICONTROL Finish]** för att skapa och genomföra kursen.

>[!NOTE]
>
>Konfigurationer är unika och specifika för den avsedda mottagaren, vilket innebär att konfigurationer för butiksförsäljningsreceptet inte fungerar för produktmottagaren för Recommendations. Se [referens](#reference) för en lista över butiksförsäljningsmottagarkonfigurationer.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Utvärdera modellen

I Experience Platform väljer du **[!UICONTROL Models]** i den vänstra navigeringsrutan och välj sedan fliken Bläddra för att visa dina befintliga modeller. Sök efter och markera hyperlänken som är kopplad till namnet på den modell som du vill utvärdera.

![välj modell](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alla befintliga kurser med deras aktuella utbildningsstatus listas. Med flera färdiga kurser kan man jämföra utvärderingsvärden för olika utbildningar i modellutvärderingsschemat. Välj ett utvärderingsmått i listrutan ovanför diagrammet.

MAPE-mätvärdet (Meean Absolute Percent Error) anger noggrannheten som en procentandel av felet. Detta används för att identifiera de mest högpresterande experterna. Ju lägre värde, desto bättre.

![översikt över utbildningar](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

Precisionsmåttet beskriver procentandelen relevanta instanser jämfört med totalvärdet *hämtad* Instanser. Precision kan ses som sannolikheten att ett slumpmässigt valt resultat blir korrekt.

![köra flera körningar](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Om du väljer en specifik utbildningskörning visas information om den som körs genom att utvärderingssidan öppnas. Detta kan göras även innan körningen har slutförts. På utvärderingssidan kan du se andra utvärderingsmått, konfigurationsparametrar och visualiseringar som är specifika för kursen.

![förhandsgranskningsloggar](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Du kan även hämta aktivitetsloggar för att se information om körningen. Loggar är särskilt användbara för misslyckade körningar för att se vad som gick fel.

![aktivitetsloggar](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Hyperparametrar kan inte tränas och en modell måste optimeras genom att olika kombinationer av hyperparametrar testas. Upprepa denna modellutbildning och utvärderingsprocess tills du har nått en optimerad modell.

## Nästa steg

Den här självstudiekursen gick igenom hur du skapar, utbildar och utvärderar en modell i [!DNL Data Science Workspace]. När ni har kommit fram till en optimerad modell kan ni använda den tränade modellen för att generera insikter genom att följa följande [Posta en modell i användargränssnittet](./score-model-ui.md) självstudiekurs.

## Referens  {#reference}

### Detaljhandelsförsäljningens mottagarkonfigurationer

Hyperparametrar bestämmer modellens utbildningsbeteende, och om du ändrar hyperparametrar påverkas modellens precision och precision:

| Hyperparameter | Beskrivning | Rekommenderat intervall |
| --- | --- | --- |
| learning_rate | Inlärningsgraden minskar bidraget från varje träd med learning_rate. Det finns en kompromiss mellan learning_rate och n_estimators. | 0.1 |
| n_estimators | Antalet förstärkningssteg som ska utföras. Ökning av övertoningar är relativt robust för överpassning, så ett stort tal ger vanligtvis bättre prestanda. | 100 |
| max_depth | Maximalt djup för de enskilda regressionsberäknarna. Det maximala djupet begränsar antalet noder i trädet. Finjustera den här parametern för bästa prestanda. det bästa värdet beror på interaktionen mellan indatavariablerna. | 3 |

Ytterligare parametrar bestämmer modellens tekniska egenskaper:

| Parameternyckel | Typ | Beskrivning |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Sträng | Lista med kommaavgränsade inmatningsschemaattribut. |
| `ACP_DSW_TARGET_FEATURES` | Sträng | Lista med kommaseparerade utdataschemaattribut. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolean | Avgör om in- och utdatafunktionerna kan ändras |
| `tenantId` | Sträng | Detta ID garanterar att de resurser du skapar namnges korrekt och finns i IMS-organisationen. [Följ stegen här](../../xdm/api/getting-started.md#know-your-tenant_id) för att hitta ditt klientorganisations-ID. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Sträng | Det indatarema som används för utbildning av en modell. |
| `evaluation.labelColumn` | Sträng | Kolumnetikett för utvärderingsvisualiseringar. |
| `evaluation.metrics` | Sträng | Kommaavgränsad lista med mätvärden som ska användas för att utvärdera en modell. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Sträng | Utdatamodeller som används för att klassificera en modell. |
