---
keywords: uppdatera destinationskonto, destinationskonton, uppdatera konton, uppdatera destinationskonto
title: Uppdatera destinationskonton
type: Tutorial
description: I den här självstudiekursen visas stegen för att uppdatera målkonton i användargränssnittet i Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
translation-type: tm+mt
source-git-commit: 5b72433fcf2318f98538278c6d2650b366e391a2
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Uppdatera destinationskonton

## Översikt {#overview}

På fliken **[!UICONTROL Accounts]** visas information om anslutningar som du har upprättat med olika mål. Se tabellen nedan för all information du kan få på varje mål:

![Fliken Konton](../assets/ui/update-accounts/destination-accounts.png)

| Element | Beskrivning |
|---|---|
| [!UICONTROL Platform] | Det mål som du har konfigurerat anslutningen för. |
| [!UICONTROL Connection Type] | Representerar anslutningstypen för din lagringsbucket eller destination. <ul><li>För e-postmarknadsföringsmål: Kan vara S3 eller FTP.</li><li>För reklamdestinationer i realtid: Server-till-server</li><li>För molnlagringsmål för Amazon S3: Åtkomstnyckel </li><li>För SFTP-molnlagringsmål: Grundläggande autentisering för SFTP</li></ul> |
| [!UICONTROL Username] | Användarnamnet som du valde i [guiden för anslutningsmål](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Representerar antalet unika lyckade målflöden som är kopplade till grundläggande information som skapats för ett mål. |
| [!UICONTROL Authorized] | Det datum då anslutningen till det här målet auktoriserades. |

## Uppdatera konton {#update}

Följ stegen nedan för att uppdatera anslutningsinformationen till befintliga mål.

1. Logga in på användargränssnittet [Experience Platform och välj **[!UICONTROL Destinations]** i det vänstra navigeringsfältet. ](https://platform.adobe.com/) Välj **[!UICONTROL Accounts]** i den övre rubriken om du vill visa dina befintliga konton.

   ![Fliken Konton](../assets/ui/update-accounts/accounts-tab.png)

2. Välj filterikonen ![Filterikon](../assets/ui/update-accounts/filter.png) uppe till vänster för att öppna sorteringspanelen. På sorteringspanelen finns en lista med alla mål. Du kan markera mer än ett mål i listan om du vill se ett filtrerat urval konton som är associerade med de valda målen.

   ![Filtermål](../assets/ui/update-accounts/filter-accounts.png)

3. Välj knappen ![Redigera konto](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit]** i kolumnen **[!UICONTROL Platform]** om du vill redigera kontoinformationen.

   ![Fliken Konton](../assets/ui/update-accounts/accounts-edit.png)

4. Ange dina uppdaterade kontoinloggningsuppgifter.

   * För konton som använder en `OAuth2`-anslutningstyp väljer du **[!UICONTROL Reconnect OAuth]** för att förnya dina kontoinloggningsuppgifter.

      ![Redigera information OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * För konton som använder en `Access Key`- eller `ConnectionString`-anslutningstyp kan du redigera din kontoautentiseringsinformation, inklusive information som åtkomst-ID, hemliga nycklar eller anslutningssträngar.

      ![Redigera åtkomstnyckel för detaljer](../assets/ui/update-accounts/edit-details-key.png)

5. Välj **[!UICONTROL Save]** om du vill slutföra uppdateringen av autentiseringsuppgifterna.
