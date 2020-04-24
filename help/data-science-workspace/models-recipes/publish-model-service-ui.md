---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publicera en modell som en tjänst (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Publicera en modell som en tjänst (UI)

Med Adobe Experience Platform Data Science Workspace kan ni publicera er utbildade och utvärderade modell som en tjänst, vilket gör att användare i IMS-organisationen kan få sina data poäng utan att behöva skapa egna modeller.

I den här självstudiekursen går du igenom stegen för att publicera en modell som en tjänst och poängsätter data med en tjänst via *tjänstgalleriet*. Den delas in i följande huvudavsnitt:

- [Publicera en modell](#publish-a-model)
- [Poäng med hjälp av en tjänst](#access-a-service)

## Komma igång

För att kunna slutföra den här självstudiekursen måste du ha tillgång till Experience Platform. Om du inte har tillgång till en IMS-organisation i Experience Platform, ska du tala med systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig modell med en lyckad utbildning. Om du inte har någon publicerbar modell följer du [tåget och utvärderar en modell i självstudiekursen för användargränssnitt](./train-evaluate-model-ui.md) innan du fortsätter.

Om du föredrar att publicera en modell med hjälp av API:er för Sensei Machine Learning finns mer information i [API-självstudiekursen](./publish-model-service-api.md).

## Publicera en modell {#publish-a-model}

1. Klicka på länken i den vänstra navigeringskolumnen i Adobe Experience Platform för att visa en lista över alla befintliga modeller. **[!UICONTROL Models]** Sök efter och klicka på namnet på modellen som ska publiceras som en tjänst.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Klicka **[!UICONTROL Publish]** uppe till höger på sidan Modellöversikt för att starta en process för att skapa en tjänst.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Ange ett önskat namn för tjänsten och ange eventuellt en servicebeskrivning. Klicka **[!UICONTROL Next]** när du är klar.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Alla framgångsrika kurser för modellerna listas. Den nya tjänsten ärver utbildnings- och poängkonfigurationer från den valda kursen.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Klicka **[!UICONTROL Finish]** för att skapa tjänsten och omdirigera till **[!UICONTROL Service Gallery]** för att visa alla tillgängliga tjänster, inklusive den nya tjänsten.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Poäng med hjälp av en tjänst {#access-a-service}

1. I Adobe Experience Platform klickar du på fliken **[!UICONTROL Services]** i den vänstra navigeringskolumnen för att komma åt *tjänstgalleriet*. Hitta den tjänst du vill använda och klicka på **[!UICONTROL Score]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Välj en lämplig indatauppsättning för poängkörningen och klicka sedan på **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Välj en lämplig datauppsättning för poängresultatet och klicka sedan på **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. När en tjänst skapas ärver den standardpoängkonfigurationer. Du kan granska dessa konfigurationer och justera dem efter behov genom att dubbelklicka på värdena. När du är nöjd med konfigurationerna klickar du på **[!UICONTROL Finish]** för att påbörja poängkörningen.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. På sidan *Översikt* över tjänsten visas information om det nya bedömningsjobbet och dess förlopp. När jobbet är klart uppdateras **[!UICONTROL Most Recent]** poängjobbet.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du publicerat en modell som en tillgänglig tjänst och gjort en bedömning av data med den nya tjänsten via *tjänstgalleriet*. Fortsätt till nästa självstudiekurs för att lära dig hur du kan [schemalägga automatiska kurser och poängsättning för en tjänst](./schedule-models-ui.md).
