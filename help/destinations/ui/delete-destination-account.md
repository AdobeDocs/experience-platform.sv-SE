---
keywords: ta bort destinationskonto, destinationskonton, ta bort konton
title: Ta bort destinationskonton
type: Tutorial
description: I den här självstudiekursen visas stegen för att ta bort målkonton i användargränssnittet i Adobe Experience Platform
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Ta bort destinationskonton

## Översikt {#overview}

Fliken **[!UICONTROL Accounts]** innehåller information om de anslutningar du har upprättat med olika mål. Se [Kontoöversikten](../ui/destinations-workspace.md#accounts) för all information du kan få om varje målkonto.

I den här självstudiekursen beskrivs stegen för att ta bort destinationskonton som inte längre behövs med hjälp av användargränssnittet i Experience Platform.

![Fliken Konton](../assets/ui/update-accounts/destination-accounts.png)

## Ta bort konton {#delete}

>[!TIP]
>
>Innan du tar bort målkontot måste du först ta bort alla befintliga dataflöden som är kopplade till målkontot. Om du vill ta bort befintliga måldataflöden kan du läsa självstudiekursen om att [ta bort måldataflöden i användargränssnittet](./delete-destinations.md).

Följ stegen nedan för att ta bort befintliga målkonton.

1. Logga in på [Experience Platform-gränssnittet](https://platform.adobe.com/) och välj **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Välj **[!UICONTROL Accounts]** i den övre rubriken om du vill visa dina befintliga konton.

   ![Fliken Konton](../assets/ui/delete-accounts/accounts-tab.png)

2. Välj filterikonen ![Filterikon](/help/images/icons/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill se ett filtrerat urval konton som är associerade med de valda målen.

   ![Filtrera mål](../assets/ui/delete-accounts/filter-accounts.png)

3. Markera ellipserna (`...`) bredvid namnet på kontot som du vill ta bort. En popup-panel visas med alternativ för **[!UICONTROL Activate audiences]**, **[!UICONTROL Edit details]** och **[!UICONTROL Delete]** kontot. Markera knappen ![Ta bort](/help/images/icons/delete.png) **[!UICONTROL Delete]** om du vill ta bort kontot.

   ![Ta bort målkonto](../assets/ui/delete-accounts/delete-accounts.png)

4. En slutgiltig bekräftelsedialogruta visas. Välj **[!UICONTROL Delete]** för att slutföra processen.

![Bekräfta borttagning av konto](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Nästa steg

I den här självstudiekursen har du använt arbetsytan Mål för att ta bort befintliga konton.

Anvisningar om hur du utför de här åtgärderna programmatiskt med API:t [!DNL Flow Service] finns i självstudiekursen [Ta bort anslutningar med API:t för Flow Service ](../api/delete-destination-account.md)
