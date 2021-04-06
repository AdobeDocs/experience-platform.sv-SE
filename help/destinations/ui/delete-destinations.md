---
keywords: radera destinationer, ta bort mål
title: Ta bort mål
type: Självstudiekurs
description: I den här självstudiekursen visas stegen för att ta bort ett befintligt mål i Adobe Experience Platform-gränssnittet
translation-type: tm+mt
source-git-commit: ebe2a35e66b78acf6a9ffa20664877913cd35648
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# Ta bort mål {#delete-destinations}

## Översikt {#overview}

I Adobe Experience Platform användargränssnitt kan du ta bort befintliga anslutningar till mål.

Om du tar bort ett mål tas alla befintliga dataflöden till det målet bort. Alla segment som aktiveras för de mål som du tar bort mappas inte innan dataflödet tas bort.

Det finns två sätt att ta bort mål från [!DNL Platform] [!DNL UI]. Ni kan:

* [Ta bort mål från  [!UICONTROL Browse] fliken](#delete-browse-tab)
* [Ta bort mål från sidan med målinformation](#delete-destination-details-page)

## Ta bort mål från fliken Bläddra{#delete-browse-tab}

Följ stegen nedan för att ta bort ett mål från fliken [!UICONTROL Browse].

1. Logga in på användargränssnittet [Experience Platform och välj **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. ](https://platform.adobe.com/) Om du vill visa dina befintliga mål väljer du **[!UICONTROL Browse]** i det övre huvudet.

   ![Bläddra bland mål](../assets/ui/delete-destinations/browse-destinations.png)

2. Välj filterikonen ![Filterikon](../assets/ui/delete-destinations/filter.png) uppe till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtermål](../assets/ui/delete-destinations/filter-destinations.png)

3. Markera knappen ![Ta bort](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]** i kolumnen **[!UICONTROL Platform]** om du vill ta bort ett befintligt mål.
   ![Ta bort mål](../assets/ui/delete-destinations/delete-destinations.png)

4. Välj **[!UICONTROL Delete]** för att bekräfta borttagningen av målet.

   ![Bekräfta borttagning av mål](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## Ta bort mål från målinformationssidan{#delete-destination-details-page}

Följ stegen nedan för att ta bort ett mål från sidan med målinformation.

1. Logga in på användargränssnittet [Experience Platform och välj **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. ](https://platform.adobe.com/) Om du vill visa dina befintliga mål väljer du **[!UICONTROL Browse]** i det övre huvudet.

   ![Bläddra bland mål](../assets/ui/delete-destinations/browse-destinations.png)

2. Välj filterikonen ![Filterikon](../assets/ui/delete-destinations/filter.png) uppe till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtermål](../assets/ui/delete-destinations/filter-destinations.png)

3. Markera namnet på målet som du vill ta bort.

   ![Välj mål](../assets/ui/delete-destinations/delete-destination-select.png)

   * Om målet har befintliga dataflöden öppnas fliken [!UICONTROL Dataflow runs].

      ![Fliken Dataflöden körs](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Om målet inte har några befintliga dataflöden kommer du till en tom sida där du kan börja aktivera målgrupper.

      ![Destinationsinformation](../assets/ui/delete-destinations/destination-details-empty.png)


4. Välj **[!UICONTROL Delete]** i den högra listen.

   ![Ta bort mål](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Välj **[!UICONTROL Delete]** i bekräftelsedialogrutan för att ta bort målet.

   ![Bekräfta borttagning av mål](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Beroende på serverinläsningen kan det ta några minuter för [!DNL Platform] att ta bort målet.