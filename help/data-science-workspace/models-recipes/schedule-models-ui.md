---
keywords: Experience Platform;schemalägg en modell;Datavetenskap, arbetsyta;populära ämnen;schemaläggning;schemalägga utbildning
solution: Experience Platform
title: Schemalägg en modell i gränssnittet för datavetenskapen
topic: tutorial
type: Tutorial
description: Med Adobe Experience Platform Data Science Workspace kan du skapa schemalagda kurser i maskininlärning. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# Schemalägg en modell i gränssnittet för datavetenskapen

Med Adobe Experience Platform [!DNL Data Science Workspace] kan du ställa in schemalagda poängsättnings- och utbildningskörningar på en maskininlärningstjänst. Genom att automatisera utbildnings- och poängprocessen kan du behålla och förbättra en tjänsts effektivitet genom att hålla jämna steg med era datamönster.

Den här självstudiekursen går igenom stegen för att konfigurera utbildnings- och poängsättningsscheman för en befintlig tjänst via [!UICONTROL Service Gallery]. Den delas in i följande huvudavsnitt:

- [Konfigurera schemalagd poängsättning](#configure-scheduled-scoring)
- [Konfigurera schemalagd utbildning](#configure-scheduled-training)

## Komma igång

Du måste ha tillgång till [!DNL Experience Platform] för att kunna slutföra den här självstudiekursen. Om du inte har tillgång till en IMS-organisation i [!DNL Experience Platform], ska du tala med systemadministratören innan du fortsätter.

Den här självstudiekursen kräver en befintlig tjänst. Om du inte har någon tillgänglig tjänst att arbeta med kan du skapa en genom att följa självstudiekursen [Publicera din modell som en tjänst i användargränssnittet](./publish-model-service-ui.md).

## Konfigurera schemalagd poängsättning {#configure-scheduled-scoring}

Modellpoäng kan konfigureras till en automatiserad process på schemalagd basis. När en tjänst har skapats kan du följa stegen nedan för att konfigurera och tillämpa ett poängschema:

1. I Adobe Experience Platform klickar du på fliken **[!UICONTROL Services]** i den vänstra navigeringskolumnen för att komma åt **[!DNL Service Gallery]**. Hitta den tjänst du vill schemalägga poängsättningen för och klicka på **[!UICONTROL Open]** för att visa sidan **Översikt**.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. På sidan Översikt visas tjänstens poänginformation. Klicka på länken **[!UICONTROL Update Schedule]** för att konfigurera ett poängschema.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Konfigurera frekvens, startdatum, slutdatum, indatamängd och utdatamängd för poängsättningsschemat. När du är nöjd med konfigurationerna klickar du på **[!UICONTROL Create]** för att uppdatera tjänstens poängschema.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Det uppdaterade poängschemat visas på sidan **Översikt** för tjänsten.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Konfigurera schemalagd utbildning {#configure-scheduled-training}

När schemalagd utbildning konfigureras körs på en tjänst säkerställer du att maskininlärningsmodellen uppdateras till de senaste datamönstren. När en schemalagd utbildningskörning är avslutad används den resulterande utbildade modellen för att driva tjänsten fram till nästa schemalagda utbildningskurs.

När en tjänst har skapats följer du stegen nedan för att konfigurera och tillämpa ett utbildningsschema:

1. I Adobe Experience Platform klickar du på fliken **[!UICONTROL Services]** i den vänstra navigeringskolumnen för att komma åt **[!UICONTROL Service Gallery]**. Hitta den tjänst som du vill schemalägga kurser för och klicka på **[!UICONTROL Open]** för att visa sidan **Översikt**.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. På sidan Översikt visas tjänstens utbildningsinformation. Klicka på länken **[!UICONTROL Update Schedule]** för att konfigurera ett utbildningsschema.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Konfigurera frekvens, startdatum, slutdatum och indatamängd som används för utbildningens schema. När du är nöjd med konfigurationerna klickar du på **[!UICONTROL Create]** för att uppdatera tjänstens utbildningsschema.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Det uppdaterade utbildningsschemat visas på sidan **Översikt** för tjänsten.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Nästa steg

Genom att följa den här självstudiekursen har du schemalagt automatiserad utbildning och poängsättning för en tjänst och slutfört arbetsflödet för självstudiekursen [!DNL Data Science Workspace]. Om du inte redan har gjort det kan du överväga att starta om självstudiekursen](./create-retails-sales-dataset.md) och följa API-arbetsflödet för att skapa, utbilda, poängsätta och publicera en modell.[
