---
keywords: ta bort destinationskonto, destinationskonton, ta bort konton
title: Ta bort destinationskonton
type: Tutorial
description: I den här självstudiekursen visas stegen för att ta bort målkonton i användargränssnittet i Adobe Experience Platform
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 1%

---

# Ta bort destinationskonton

## Översikt {#overview}

The **[!UICONTROL Accounts]** På -fliken visas information om anslutningar som du har upprättat med olika mål. Se [Kontoöversikt](../ui/destinations-workspace.md#accounts) för all information du kan få på varje destinationskonto.

I den här självstudiekursen beskrivs stegen för att ta bort destinationskonton som inte längre behövs med hjälp av användargränssnittet i Experience Platform.

![Fliken Konton](../assets/ui/update-accounts/destination-accounts.png)

## Ta bort konton {#delete}

>[!TIP]
>
>Innan du tar bort målkontot måste du först ta bort alla befintliga dataflöden som är kopplade till målkontot. Om du vill ta bort befintliga måldataflöden kan du läsa självstudiekursen om [ta bort måldataflöden i användargränssnittet](./delete-destinations.md).

Följ stegen nedan för att ta bort befintliga målkonton.

1. Logga in på [Experience Platform UI](https://platform.adobe.com/) och markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. Välj **[!UICONTROL Accounts]** från den övre rubriken för att visa dina befintliga konton.

   ![Fliken Konton](../assets/ui/delete-accounts/accounts-tab.png)

2. Markera filterikonen ![Filterikon](../assets/ui/update-accounts/filter.png) längst upp till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill se ett filtrerat urval konton som är associerade med de valda målen.

   ![Filtermål](../assets/ui/delete-accounts/filter-accounts.png)

3. Markera ellipserna (`...`) bredvid namnet på det konto du vill ta bort. En popup-panel visas med alternativ för att **[!UICONTROL Activate audiences]**, **[!UICONTROL Edit details]** och **[!UICONTROL Delete]** kontot. Välj ![Knappen Ta bort](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Delete]** om du vill ta bort kontot.

   ![Ta bort destinationskonto](../assets/ui/delete-accounts/delete-accounts.png)

4. En slutgiltig bekräftelsedialogruta visas. Välj **[!UICONTROL Delete]** för att slutföra processen.

![Bekräfta borttagning av konto](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Nästa steg

I den här självstudiekursen har du använt arbetsytan Mål för att ta bort befintliga konton.

För steg om hur du utför dessa åtgärder programmatiskt med [!DNL Flow Service] API, se självstudiekursen om [ta bort anslutningar med API:t för Flow Service](../api/delete-destination-account.md)
