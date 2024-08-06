---
keywords: Experience Platform;utbilda och utvärdera;Data Science Workspace;populära ämnen;skapa en modell;skapa en utbildningskurs
solution: Experience Platform
title: utbilda och utvärdera en modell i användargränssnittet för datavetenskap i Workspace
type: Tutorial
description: I Adobe Experience Platform Data Science Workspace skapas en maskininlärningsmodell genom att en befintlig Recipe som är lämplig för modellens avsikt läggs till. Modellen är sedan utbildad och utvärderad för att optimera dess driftseffektivitet och effektivitet genom att finjustera de tillhörande hyperparametrarna. Recept kan återanvändas, vilket innebär att flera modeller kan skapas och skräddarsys för specifika syften med en enda Recept.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# Utbilda och utvärdera en modell i användargränssnittet för datavetenskap i Workspace

>[!NOTE]
>
>Data Science Workspace kan inte längre köpas.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

I Adobe Experience Platform Data Science Workspace skapas en maskininlärningsmodell genom att en befintlig Recipe som är lämplig för modellens avsikt läggs till. Modellen är sedan utbildad och utvärderad för att optimera dess driftseffektivitet och effektivitet genom att finjustera de tillhörande hyperparametrarna. Recept kan återanvändas, vilket innebär att flera modeller kan skapas och skräddarsys för specifika syften med en enda Recept.

Den här självstudiekursen går igenom stegen för att skapa, utbilda och utvärdera en modell.

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform] för att kunna slutföra den här självstudiekursen. Om du inte har åtkomst till en organisation i [!DNL Experience Platform], ska du tala med systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig recept. Om du inte har någon recept följer du självstudiekursen [Importera en paketerad recept i användargränssnittet](./import-packaged-recipe-ui.md) innan du fortsätter.

## Skapa en modell

I Experience Platform väljer du fliken **[!UICONTROL Models]** i den vänstra navigeringen och sedan klickar du på fliken Bläddra för att visa dina befintliga modeller. Välj **[!UICONTROL Create Model]** uppe till höger på sidan för att börja skapa en modell.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Bläddra igenom listan med befintliga recept, sök efter och välj den mottagare som ska användas för att skapa modellen och välj **[!UICONTROL Next]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Välj en lämplig indatauppsättning och välj **[!UICONTROL Next]**. Detta anger standarddatauppsättningen för inmatningsutbildning för modellen.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Ange ett namn för modellen och granska standardmodellkonfigurationerna. Standardkonfigurationer tillämpades när Recept skapades, granska och ändra konfigurationsvärdena genom att dubbelklicka på värdena.

Om du vill tillhandahålla en ny uppsättning konfigurationer väljer du **[!UICONTROL Upload New Config]** och drar en JSON-fil som innehåller modellkonfigurationer till webbläsarfönstret. Välj **[!UICONTROL Finish]** för att skapa modellen.

>[!NOTE]
>
>Konfigurationer är unika och specifika för den avsedda mottagaren, vilket innebär att konfigurationer för butiksförsäljningsreceptet inte fungerar för produktmottagaren för Recommendations. I avsnittet [reference](#reference) finns en lista över konfigurationer för Retail Sales Recipe.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Skapa en utbildningskörning

I Experience Platform väljer du fliken **[!UICONTROL Models]** i den vänstra navigeringen och sedan klickar du på fliken Bläddra för att visa dina befintliga modeller. Sök efter och välj den hyperlänk som är kopplad till namnet på den modell som du vill utbilda.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alla befintliga kurser med deras aktuella utbildningsstatus listas. För modeller som skapats med användargränssnittet [!DNL Data Science Workspace] genereras och körs en utbildningskörning automatiskt med standardkonfigurationer och datauppsättningen för inmatningsutbildning.

Skapa en ny utbildningskörning genom att välja **[!UICONTROL Train]** uppe till höger på sidan Modellöversikt.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Välj indatauppsättning för utbildning för utbildningskörningen och välj sedan **[!UICONTROL Next]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Standardkonfigurationer som tillhandahålls när modellen skapas visas, ändra och ändra dem därefter genom att dubbelklicka på värdena. Välj **[!UICONTROL Finish]** om du vill skapa och köra utbildningskörningen.

>[!NOTE]
>
>Konfigurationer är unika och specifika för den avsedda mottagaren, vilket innebär att konfigurationer för butiksförsäljningsreceptet inte fungerar för produktmottagaren för Recommendations. I avsnittet [reference](#reference) finns en lista över konfigurationer för Retail Sales Recipe.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Utvärdera modellen

I Experience Platform väljer du fliken **[!UICONTROL Models]** i den vänstra navigeringspanelen och sedan bläddringsfliken för att visa de modeller du redan har. Leta reda på och välj hyperlänken som är kopplad till namnet på modellen som du vill utvärdera.

![välj modell](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Alla befintliga utbildningar med aktuell utbildningsstatus listas. Med flera genomförda utbildningar kan utvärderingsmätningarna jämföras över olika utbildningar i modellutvärderingstabellen. Välj ett utvärderingsmått i listrutan ovanför diagrammet.

MAPE-mätvärdet (Meean Absolute Percent Error) anger noggrannheten som en procentandel av felet. Detta används för att identifiera det experiment som har högst prestanda. Ju lägre mape, desto bättre.

![Översikt över utbildningskörningar](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

Precisionsmåttet beskriver procentandelen relevanta instanser jämfört med det totala antalet *hämtade* instanser. Precisionen kan ses som sannolikheten att ett slumpmässigt valt utfall är korrekt.

![köra flera körningar](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Om du väljer en specifik utbildningskörning visas information om den som körs genom att du öppnar utvärderingssidan. Detta kan göras även innan körningen har slutförts. På utvärderingssidan kan du se andra utvärderingsmått, konfigurationsparametrar och visualiseringar som är specifika för kursen.

![förhandsgranskningsloggar](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Du kan även hämta aktivitetsloggar för att se information om körningen. Loggar är särskilt användbara för misslyckade körningar för att se vad som gick fel.

![aktivitetsloggar](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Hyperparametrar kan inte tränas och en modell måste optimeras genom att testa olika kombinationer av hyperparametrar. Upprepa denna modellutbildning och utvärderingsprocess tills du har kommit fram till en optimerad modell.

## Nästa steg

I den här självstudiekursen fick du vägledning genom att skapa, träna och utvärdera en modell i [!DNL Data Science Workspace]. När du har kommit fram till en optimerad modell kan du använda den utbildade modellen för att generera insikter genom att följa självstudiekursen [poängsätta en modell i användargränssnittet](./score-model-ui.md).

## Referens {#reference}

### Detaljhandelsförsäljningens mottagarkonfigurationer

Hyperparametrar bestämmer modellens utbildningsbeteende, och om du ändrar Hyperparametrar kommer det att påverka modellens noggrannhet och precision:

| Hyperparameter | Beskrivning | Rekommenderat intervall |
| --- | --- | --- |
| learning_rate | Inlärningsgraden minskar bidraget från varje träd med learning_rate. Det finns en kompromiss mellan learning_rate och n_estimators. | 0,1 |
| n_estimators | Antalet förstärkningssteg som ska utföras. Ökning av övertoningar är relativt robust för överpassning, så ett stort tal ger vanligtvis bättre prestanda. | 100 |
| max_depth | Maximalt djup för de enskilda regressionsberäknarna. Det maximala djupet begränsar antalet noder i trädet. Finjustera den här parametern för bästa prestanda. Det bästa värdet beror på interaktionen mellan indatavariablerna. | 3 |

Ytterligare parametrar bestämmer modellens tekniska egenskaper:

| Parameternyckel | Typ | Beskrivning |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Sträng | Lista med kommaavgränsade inmatningsschemaattribut. |
| `ACP_DSW_TARGET_FEATURES` | Sträng | Lista med kommaseparerade utdataschemaattribut. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolean | Avgör om in- och utdatafunktionerna kan ändras |
| `tenantId` | Sträng | Detta ID garanterar att de resurser du skapar namnges korrekt och finns i din organisation. [Följ stegen här](../../xdm/api/getting-started.md#know-your-tenant_id) för att hitta ditt klient-ID. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Sträng | Det indatarema som används för utbildning av en modell. |
| `evaluation.labelColumn` | Sträng | Kolumnetikett för utvärderingsvisualiseringar. |
| `evaluation.metrics` | Sträng | Kommaavgränsad lista med mätvärden som ska användas för att utvärdera en modell. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Sträng | Utdatamodeller som används för att klassificera en modell. |
