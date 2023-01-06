---
keywords: Experience Platform;publicera en modell;Data Science Workspace;populära ämnen;göra en tjänst
solution: Experience Platform
title: Publicera en modell som en tjänst i gränssnittet för datavetenskapen
type: Tutorial
description: Med Adobe Experience Platform Data Science Workspace kan du publicera din utbildade och utvärderade modell som en tjänst, vilket gör att användare i IMS-organisationen kan få sina data poäng utan att behöva skapa egna modeller.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Publicera en modell som en tjänst i gränssnittet för datavetenskapen

Med Adobe Experience Platform Data Science Workspace kan du publicera din utbildade och utvärderade modell som en tjänst, vilket gör att användare i IMS-organisationen kan få sina data poäng utan att behöva skapa egna modeller.

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform]. Om du inte har tillgång till en IMS-organisation i [!DNL Experience Platform]bör du kontakta systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig modell med en lyckad utbildning. Om du inte har någon publicerbar modell följer du [Utbildning och utvärdering av en modell i användargränssnittet](./train-evaluate-model-ui.md) självstudiekurs innan du fortsätter.

Om du föredrar att publicera en modell med Sensei Machine Learning API:er finns i [API, genomgång](./publish-model-service-api.md).

## Publicera en modell {#publish-a-model}

I Adobe Experience Platform väljer du **[!UICONTROL Models]** i den vänstra navigeringskolumnen väljer du **[!UICONTROL Browse]** för att visa alla befintliga modeller. Välj namnet på den modell som du vill publicera som en tjänst.

![](../images/models-recipes/publish-model/browse_model.png)

Välj **[!UICONTROL Publish]** i det övre högra hörnet på modellöversiktssidan för att starta en process för att skapa tjänster.

![](../images/models-recipes/publish-model/view_training.png)

Ange önskat namn för tjänsten och ange en servicebeskrivning, välj **[!UICONTROL Next]** när du är klar.

![](../images/models-recipes/publish-model/configure_training.png)

Alla framgångsrika kurser för modellerna listas. Den nya tjänsten ärver utbildnings- och poängkonfigurationer från den valda kursen.

![](../images/models-recipes/publish-model/select_training_run.png)

Välj **[!UICONTROL Finish]** för att skapa tjänsten och omdirigera till **[!UICONTROL Service Gallery]** för att visa alla tillgängliga tjänster, inklusive den nya tjänsten.

![](../images/models-recipes/publish-model/service_gallery.png)

## Poäng med hjälp av en tjänst {#access-a-service}

I Adobe Experience Platform väljer du **[!UICONTROL Services]** -fliken som finns i den vänstra navigeringskolumnen för att komma åt **[!UICONTROL Service Gallery]**. Hitta den tjänst du vill använda och välj **[!UICONTROL Open]**.

![](../images/models-recipes/publish-model/open_service.png)

Välj **[!UICONTROL Score]**.

![](../images/models-recipes/publish-model/score_service.png)

Välj en lämplig indatauppsättning för poängkörningen och välj sedan **[!UICONTROL Next]**. Du uppmanas att göra samma steg för poängdatauppsättningen. När du har valt in- och utdatauppsättningen kan du uppdatera konfigurationerna.

![](../images/models-recipes/publish-model/select_datasets.png)

När en tjänst skapas ärver den standardpoängkonfigurationer. Du kan granska dessa konfigurationer och justera dem efter behov genom att dubbelklicka på värdena. När du är nöjd med konfigurationerna väljer du **[!UICONTROL Finish]** för att börja poängsättningen.

![](../images/models-recipes/publish-model/scoring_configs.png)

På tjänstens **Översikt** sida visas information om det nya poängjobbet och hur det fortskrider. När jobbet är klart **[!UICONTROL Most Recent]** sidhuvud i **[!UICONTROL Scoring]** behållaren uppdateras.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du publicerat en modell som en tillgänglig tjänst och gjort en bedömning av data med den nya tjänsten via [!UICONTROL Service Gallery]. Fortsätt till nästa självstudiekurs för att lära dig hur du kan [schemalägga automatiserad utbildning och poängsättning för en tjänst](./schedule-models-ui.md).
