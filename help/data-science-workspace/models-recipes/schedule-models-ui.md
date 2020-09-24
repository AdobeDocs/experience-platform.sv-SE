---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics;schedule scoring;schedule training
solution: Experience Platform
title: Schemalägg en modell (UI)
topic: tutorial
type: Tutorial
description: Med Adobe Experience Platform Data Science Workspace kan du skapa schemalagda kurser i maskininlärning. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Schemalägg en modell (UI)

Med Adobe Experience Platform [!DNL Data Science Workspace] kan du konfigurera schemalagda kurser i maskininlärning. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster.

Den här självstudiekursen går igenom stegen för att konfigurera utbildnings- och poängsättningsscheman för en befintlig tjänst via **[!UICONTROL Service Gallery]**. Den delas in i följande huvudavsnitt:

- [Konfigurera schemalagd poängsättning](#configure-scheduled-scoring)
- [Konfigurera schemalagd utbildning](#configure-scheduled-training)

## Komma igång

Du måste ha tillgång till den här självstudiekursen för att kunna slutföra den [!DNL Experience Platform]. Om du inte har tillgång till en IMS-organisation i [!DNL Experience Platform]kontaktar du systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig tjänst. Om du inte har någon tillgänglig tjänst att arbeta med kan du skapa en genom att följa [Publicera din modell som en tjänst i](./publish-model-service-ui.md) självstudiekursen.

## Konfigurera schemalagd poängsättning {#configure-scheduled-scoring}

Modellpoäng kan konfigureras till en automatiserad process på schemalagd basis. När en tjänst har skapats kan du följa stegen nedan för att konfigurera och tillämpa ett poängschema:

1. I Adobe Experience Platform klickar du på den **[!UICONTROL Services]** flik som finns i den vänstra navigeringskolumnen för att komma åt *[!DNL Service Gallery]*. Hitta den tjänst som du vill schemalägga poängsättningen för och klicka på **[!UICONTROL Open]** för att visa *översiktssidan* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. På sidan Översikt visas tjänstens poänginformation. Klicka på **[!UICONTROL Update Schedule]** länken för att konfigurera ett poängschema.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Konfigurera frekvens, startdatum, slutdatum, indatamängd och utdatamängd för poängsättningsschemat. När du är nöjd med konfigurationerna klickar du på **[!UICONTROL Create]** för att uppdatera tjänstens poängschema.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Det uppdaterade poängschemat visas på sidan *Översikt* över tjänsten.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Konfigurera schemalagd utbildning {#configure-scheduled-training}

När schemalagd utbildning konfigureras körs på en tjänst säkerställer du att maskininlärningsmodellen uppdateras till de senaste datamönstren. När en schemalagd utbildningskörning är avslutad används den resulterande utbildade modellen för att driva tjänsten fram till nästa schemalagda utbildningskurs.

När en tjänst har skapats följer du stegen nedan för att konfigurera och tillämpa ett utbildningsschema:

1. I Adobe Experience Platform klickar du på den **[!UICONTROL Services]** flik som finns i den vänstra navigeringskolumnen för att komma åt **[!UICONTROL Service Gallery]**. Hitta den tjänst som du vill schemalägga kurser för och klicka på **[!UICONTROL Open]** sidan *Översikt* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. På sidan Översikt visas tjänstens utbildningsinformation. Klicka på **[!UICONTROL Update Schedule]** länken för att konfigurera ett utbildningsschema.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Konfigurera frekvens, startdatum, slutdatum och indatamängd som används för utbildningens schema. När du är nöjd med konfigurationerna klickar du på **[!UICONTROL Create]** för att uppdatera tjänstens utbildningsschema.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Det uppdaterade utbildningsschemat visas på sidan *Översikt* för tjänsten.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Nästa steg

Genom att följa den här självstudiekursen har du schemalagt automatiserad utbildning och poängsättning för en tjänst och slutfört arbetsflödet för [!DNL Data Science Workspace] självstudiekursen. Om du inte redan har gjort det, överväg att [starta om självstudiekursen](./create-retails-sales-dataset.md) och följ API-arbetsflödet för att skapa, utbilda, poängsätta och publicera en modell.
