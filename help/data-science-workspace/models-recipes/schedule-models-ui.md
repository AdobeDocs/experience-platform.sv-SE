---
keywords: Experience Platform;schemalägg en modell;Datavetenskap, arbetsyta;populära ämnen;schemaläggning;schemalägga utbildning
solution: Experience Platform
title: Schemalägg en modell i gränssnittet för datavetenskapen
type: Tutorial
description: Med Adobe Experience Platform Data Science Workspace kan du skapa schemalagda kurser i maskininlärning. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Schemalägg en modell i gränssnittet för datavetenskapen

Adobe Experience Platform [!DNL Data Science Workspace] gör att du kan konfigurera schemalagda poängsättnings- och utbildningskörningar på en maskininlärningstjänst. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster.

Den här självstudiekursen går igenom stegen för att konfigurera utbildnings- och poängsättningsscheman för en befintlig tjänst via [!UICONTROL Service Gallery]. Den delas in i följande huvudavsnitt:

- [Konfigurera schemalagd poängsättning](#configure-scheduled-scoring)
- [Konfigurera schemalagd utbildning](#configure-scheduled-training)

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform]. Om du inte har tillgång till en organisation i [!DNL Experience Platform]bör du kontakta systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig tjänst. Om du inte har någon hjälpmedelstjänst att arbeta med kan du skapa en genom att följa självstudiekursen för [publicera en modell som en tjänst](./publish-model-service-ui.md).

## Konfigurera schemalagd poängsättning {#configure-scheduled-scoring}

Modellpoäng kan konfigureras till en automatiserad process på schemalagd basis. När en tjänst har skapats följer du stegen nedan för att konfigurera och tillämpa ett poängschema:

I Adobe Experience Platform väljer du **[!UICONTROL Services]** -fliken som finns i den vänstra navigeringskolumnen för att komma åt **[!DNL Service Gallery]**. Hitta den tjänst som du vill schemalägga poängsättningen för och välj **[!UICONTROL Open]** för att visa **[!UICONTROL Overview]** sida.

![](../images/models-recipes/schedule/select_service.png)

På sidan Översikt visas tjänstens poänginformation. Välj **[!UICONTROL Update Schedule]** för att konfigurera ett poängschema.

![](../images/models-recipes/schedule/update_scoring.png)

Konfigurera frekvens, startdatum, slutdatum, indatamängd och utdatamängd för poängsättningsschemat. När du är nöjd med konfigurationerna väljer du **[!UICONTROL Create]** för att uppdatera tjänstens poängplan.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Det uppdaterade poängschemat visas i tjänstens **[!UICONTROL Overview]** sida.

![](../images/models-recipes/schedule/scoring_set.png)

## Konfigurera schemalagd utbildning {#configure-scheduled-training}

Om du konfigurerar schemalagd utbildning för en tjänst uppdateras maskininlärningsmodellen till de senaste datamönstren. När en schemalagd utbildningskörning är avslutad används den resulterande tränade modellen för att driva tjänsten fram till nästa schemalagda utbildningskurs.

När en tjänst har skapats följer du stegen nedan för att konfigurera och tillämpa ett utbildningsschema:

I Adobe Experience Platform väljer du **[!UICONTROL Services]** -fliken som finns i den vänstra navigeringskolumnen för att komma åt **[!UICONTROL Service Gallery]**. Hitta den tjänst du vill boka utbildning för och välj **[!UICONTROL Open]** för att visa **[!UICONTROL Overview]** sida.

![](../images/models-recipes/schedule/select_service.png)

På sidan Översikt visas tjänstens utbildningsinformation. Välj **[!UICONTROL Update Schedule]** länk för att konfigurera ett utbildningsplan.

![](../images/models-recipes/schedule/update_training.png)

Konfigurera frekvens, startdatum, slutdatum och indatamängd som används för utbildningens schema. När du är nöjd med konfigurationerna väljer du **[!UICONTROL Create]** för att uppdatera tjänstens utbildningsschema.

![](../images/models-recipes/schedule/set_training_schedule.png)

Det uppdaterade utbildningsschemat visas i tjänstens **[!UICONTROL Overview]** sida.

![](../images/models-recipes/schedule/training_set.png)

## Nästa steg

Genom att följa den här självstudiekursen har du schemalagt automatiserad utbildning och poängsättning för en tjänst och slutfört [!DNL Data Science Workspace] självstudiekursens arbetsflöde. Om du inte redan har gjort det bör du överväga [starta om självstudiekursen](./create-retails-sales-dataset.md) och följa API-arbetsflödet för att skapa, utbilda, poängsätta och publicera en modell.
