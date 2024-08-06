---
keywords: Experience Platform;publicera en modell;Data Science Workspace;populära ämnen;göra en tjänst
solution: Experience Platform
title: Publish a Model as a Service in the Data Science Workspace UI
type: Tutorial
description: Adobe Experience Platform Data Science Workspace gör det möjligt att publicera din utbildade och utvärderade modell som en tjänst, så att användarna i organisationen kan få sina data att räcka utan att behöva skapa egna modeller.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# Publish är en modell som en tjänst i användargränssnittet för datavetenskapen i Workspace {#publish-a-model-as-a-service}

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="Publish a Model as a Service"
>abstract=""

Adobe Experience Platform Data Science Workspace gör det möjligt att publicera din utbildade och utvärderade modell som en tjänst, så att användarna i organisationen kan få sina data att räcka utan att behöva skapa egna modeller.

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform] för att kunna slutföra den här självstudiekursen. Om du inte har åtkomst till en organisation i [!DNL Experience Platform], ska du tala med systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig modell med en lyckad utbildning. Om du inte har någon publicerbar modell följer du [Utbildning och utvärderar en modell i användargränssnittet](./train-evaluate-model-ui.md) innan du fortsätter.

Om du föredrar att publicera en modell med Sensei Machine Learning API:er, se [API-självstudiekursen](./publish-model-service-api.md).

## Publish a Model {#publish-a-model}

I Adobe Experience Platform väljer du **[!UICONTROL Models]** i den vänstra navigeringskolumnen och sedan fliken **[!UICONTROL Browse]** för att visa alla befintliga modeller. Välj namnet på den modell som du vill publicera som en tjänst.

![](../images/models-recipes/publish-model/browse_model.png)

Välj **[!UICONTROL Publish]** uppe till höger på sidan Modellöversikt för att starta en process för att skapa en tjänst.

![](../images/models-recipes/publish-model/view_training.png)

Ange ett önskat namn för tjänsten och ange eventuellt en tjänstbeskrivning. Välj **[!UICONTROL Next]** när du är klar.

![](../images/models-recipes/publish-model/configure_training.png)

Alla framgångsrika kurser för modellerna listas. Den nya tjänsten ärver utbildnings- och poängkonfigurationer från den valda kursen.

![](../images/models-recipes/publish-model/select_training_run.png)

Välj **[!UICONTROL Finish]** om du vill skapa tjänsten och omdirigera till **[!UICONTROL Service Gallery]** om du vill visa alla tillgängliga tjänster, inklusive den nya tjänsten.

![](../images/models-recipes/publish-model/service_gallery.png)

## Poäng med en tjänst {#access-a-service}

I Adobe Experience Platform väljer du fliken **[!UICONTROL Services]** i den vänstra navigeringskolumnen för att komma åt **[!UICONTROL Service Gallery]**. Hitta den tjänst som du vill använda och välj **[!UICONTROL Open]**.

![](../images/models-recipes/publish-model/open_service.png)

Välj **[!UICONTROL Score]** på tjänstöversiktssidan.

![](../images/models-recipes/publish-model/score_service.png)

Välj en lämplig indatauppsättning för poängkörningen och välj sedan **[!UICONTROL Next]**. Du uppmanas att göra samma steg för poängdatauppsättningen. När du har valt in- och utdatauppsättningen kan du uppdatera konfigurationerna.

![](../images/models-recipes/publish-model/select_datasets.png)

När en tjänst skapas ärver den standardpoängkonfigurationer. Du kan granska dessa konfigurationer och justera dem efter behov genom att dubbelklicka på värdena. När du är nöjd med konfigurationerna väljer du **[!UICONTROL Finish]** för att påbörja poängkörningen.

![](../images/models-recipes/publish-model/scoring_configs.png)

På tjänstens **översiktssida** visas information om det nya bedömningsjobbet och dess förlopp. När jobbet har slutförts uppdateras rubriken **[!UICONTROL Most Recent]** i behållaren **[!UICONTROL Scoring]**.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du publicerat en modell som en tillgänglig tjänst och gjort en bedömning av data med den nya tjänsten via [!UICONTROL Service Gallery]. Fortsätt till nästa självstudiekurs för att lära dig hur du kan [schemalägga automatiserad utbildning och poängsättning för en tjänst](./schedule-models-ui.md).
