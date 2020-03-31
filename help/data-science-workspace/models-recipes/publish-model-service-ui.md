---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publicera en modell som en tjänst (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: af491361c5c3518e9bcc0af41a5aa79022229a2d

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

## Publicera en modell

1. I Adobe Experience Platform klickar du på länken **Modeller** i den vänstra navigeringskolumnen för att visa alla befintliga modeller. Sök efter och klicka på namnet på modellen som ska publiceras som en tjänst.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
1. Klicka på **Publicera** uppe till höger på sidan Modellöversikt för att starta en process för att skapa en tjänst.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
1. Ange önskat namn för tjänsten och ange eventuellt en servicebeskrivning. Klicka på **Nästa** när du är klar.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
1. Alla framgångsrika kurser för modellerna listas. Den nya tjänsten ärver utbildnings- och poängkonfigurationer från den valda kursen.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
1. Klicka på **Slutför** för att skapa tjänsten och dirigera om till **tjänstgalleriet** för att visa alla tillgängliga tjänster, inklusive den nya tjänsten.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Poäng med hjälp av en tjänst

1. I Adobe Experience Platform klickar du på fliken **Tjänster** i den vänstra navigeringskolumnen för att komma åt *tjänstgalleriet*. Hitta den tjänst du vill använda och klicka på **Resultat**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
1. Välj en lämplig indatauppsättning för poängkörningen och klicka sedan på **Nästa**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
1. Välj en lämplig datauppsättning för poängresultatet och klicka sedan på **Nästa**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
1. När en tjänst skapas ärver den standardpoängkonfigurationer. Du kan granska dessa konfigurationer och justera dem efter behov genom att dubbelklicka på värdena. När du är nöjd med konfigurationerna klickar du på **Slutför** för att påbörja poängkörningen.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
1. På sidan *Översikt* över tjänsten visas information om det nya bedömningsjobbet och dess förlopp. När jobbet är klart uppdateras det **senaste** poängjobbet.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Nästa steg

Genom att följa den här självstudiekursen har du publicerat en modell som en tillgänglig tjänst och gjort en bedömning av data med den nya tjänsten via *tjänstgalleriet*. Fortsätt till nästa självstudiekurs för att lära dig hur du kan [schemalägga automatiska kurser och poängsättning för en tjänst](./schedule-models-ui.md).
