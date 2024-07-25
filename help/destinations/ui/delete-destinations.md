---
keywords: ta bort mål, ta bort mål, ta bort mål
title: Ta bort mål
type: Tutorial
description: I den här självstudiekursen visas stegen för att ta bort ett befintligt mål i Adobe Experience Platform-gränssnittet
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Ta bort mål {#delete-destinations}

## Översikt {#overview}

I Adobe Experience Platform användargränssnitt kan du ta bort befintliga anslutningar till mål.

Om du tar bort ett mål tas alla befintliga dataflöden till det målet bort. Alla målgrupper som aktiveras för de mål som du tar bort mappas inte innan dataflödet tas bort.

Det finns två sätt att ta bort mål från [!DNL Platform] [!DNL UI]. Du kan:

* [Ta bort mål från fliken [!UICONTROL Browse]](#delete-browse-tab)
* [Ta bort mål från sidan med målinformation](#delete-destination-details-page)

## Ta bort mål från fliken Bläddra{#delete-browse-tab}

Följ stegen nedan för att ta bort ett mål från fliken [!UICONTROL Browse].

1. Logga in på [Experience Platform-gränssnittet](https://platform.adobe.com/) och välj **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Om du vill visa dina befintliga mål väljer du **[!UICONTROL Browse]** i det övre huvudet.

   ![Bläddra bland mål](../assets/ui/delete-destinations/browse-destinations.png)

2. Välj filterikonen ![Filterikon](/help/images/icons/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtrera mål](../assets/ui/delete-destinations/filter-destinations.png)

3. Markera knappen ![Mer](/help/images/icons/more.png) i kolumnen Namn och markera sedan knappen ![Ta bort](/help/images/icons/delete.png) **[!UICONTROL Delete]** för att ta bort en befintlig målanslutning.
   ![Ta bort mål](../assets/ui/delete-destinations/delete-destinations.png)

4. Välj **[!UICONTROL Delete]** för att bekräfta borttagningen av målanslutningen.

   ![Bekräfta borttagning av mål](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Ta bort mål från sidan med målinformation{#delete-destination-details-page}

Följ stegen nedan för att ta bort ett mål från sidan med målinformation.

1. Logga in på [Experience Platform-gränssnittet](https://platform.adobe.com/) och välj **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Om du vill visa dina befintliga mål väljer du **[!UICONTROL Browse]** i det övre huvudet.

   ![Bläddra bland mål](../assets/ui/delete-destinations/browse-destinations.png)

2. Välj filterikonen ![Filterikon](/help/images/icons/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill visa ett filtrerat urval av dataflöden som är kopplade till det valda målet.

   ![Filtrera mål](../assets/ui/delete-destinations/filter-destinations.png)

3. Markera namnet på målet som du vill ta bort.

   ![Välj mål](../assets/ui/delete-destinations/delete-destination-select.png)

   * Om målet har befintliga dataflöden kommer du till fliken [!UICONTROL Dataflow runs].

     ![Fliken Körs av dataflöde](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Om målet inte har några befintliga dataflöden kommer du till en tom sida där du kan börja aktivera målgrupper.

     ![Målinformation](../assets/ui/delete-destinations/destination-details-empty.png)

4. Välj **[!UICONTROL Delete]** i den högra listen.

   ![Ta bort mål](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Välj **[!UICONTROL Delete]** i bekräftelsedialogrutan om du vill ta bort målet.

   ![Ta bort målbekräftelse](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Beroende på serverinläsningen kan det ta några minuter för [!DNL Platform] att ta bort målet.
