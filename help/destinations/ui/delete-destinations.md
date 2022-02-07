---
keywords: ta bort mål, ta bort mål, ta bort mål
title: Ta bort mål
type: Tutorial
description: I den här självstudiekursen visas stegen för att ta bort ett befintligt mål i Adobe Experience Platform-gränssnittet
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Ta bort mål {#delete-destinations}

## Översikt {#overview}

I Adobe Experience Platform användargränssnitt kan du ta bort befintliga anslutningar till mål.

Om du tar bort ett mål tas alla befintliga dataflöden till det målet bort. Alla segment som aktiveras för de mål som du tar bort mappas inte innan dataflödet tas bort.

Det finns två sätt att ta bort mål från [!DNL Platform] [!DNL UI]. Du kan:

* [Ta bort mål från [!UICONTROL Browse] tab](#delete-browse-tab)
* [Ta bort mål från sidan med målinformation](#delete-destination-details-page)

## Ta bort mål från fliken Bläddra{#delete-browse-tab}

Följ stegen nedan för att ta bort ett mål från [!UICONTROL Browse] -fliken.

1. Logga in på [Experience Platform UI](https://platform.adobe.com/) och markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Om du vill visa dina befintliga mål väljer du **[!UICONTROL Browse]** i det övre sidhuvudet.

   ![Bläddra bland mål](../assets/ui/delete-destinations/browse-destinations.png)

2. Markera filterikonen ![Filterikon](../assets/ui/delete-destinations/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtermål](../assets/ui/delete-destinations/filter-destinations.png)

3. Välj ![Knappen Mer](../assets/ui/delete-destinations/more-icon.png) i kolumnen Namn och sedan markera ![Knappen Ta bort](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]** för att ta bort en befintlig målanslutning.
   ![Ta bort mål](../assets/ui/delete-destinations/delete-destinations.png)

4. Välj **[!UICONTROL Delete]** för att bekräfta borttagningen av målanslutningen.

   ![Bekräfta borttagning av mål](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Ta bort mål från sidan med målinformation{#delete-destination-details-page}

Följ stegen nedan för att ta bort ett mål från sidan med målinformation.

1. Logga in på [Experience Platform UI](https://platform.adobe.com/) och markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Om du vill visa dina befintliga mål väljer du **[!UICONTROL Browse]** i det övre sidhuvudet.

   ![Bläddra bland mål](../assets/ui/delete-destinations/browse-destinations.png)

2. Markera filterikonen ![Filterikon](../assets/ui/delete-destinations/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtermål](../assets/ui/delete-destinations/filter-destinations.png)

3. Markera namnet på målet som du vill ta bort.

   ![Välj mål](../assets/ui/delete-destinations/delete-destination-select.png)

   * Om målet har befintliga dataflöden tas du till [!UICONTROL Dataflow runs] -fliken.

      ![Fliken Dataflöden körs](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Om målet inte har några befintliga dataflöden kommer du till en tom sida där du kan börja aktivera målgrupper.

      ![Destinationsinformation](../assets/ui/delete-destinations/destination-details-empty.png)

4. Välj **[!UICONTROL Delete]** i rätt spår.

   ![Ta bort mål](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Välj **[!UICONTROL Delete]** i bekräftelsedialogrutan för att ta bort målet.

   ![Bekräfta borttagning av mål](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Beroende på serverbelastningen kan det ta några minuter i [!DNL Platform] för att ta bort målet.
