---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;attributbaserad åtkomstkontroll;ABAC
title: Attributbaserad åtkomstkontroll Hantera rollbehörigheter
description: Det här dokumentet innehåller information om hur du konfigurerar behörigheter för en roll via gränssnittet Behörigheter i Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 0%

---

# Hantera behörigheter för en roll

>[!IMPORTANT]
>
>Åtkomstkontrollen använder användar-ID (ett internt unikt ID som tilldelats en användare) för att bevilja behörigheter. När en organisation migreras från Adobe ID till Business ID, kommer alla behörigheter som angetts för dess användare att gå förlorade eftersom användar-ID ändras och åtkomstkontrollen kommer att använda det nyligen genererade användar-ID:t. Om din organisation migreras till ditt företags-ID kontaktar du din Adobe-representant för att migrera ditt användar-ID från Adobe ID till ditt företags-ID.

Behörigheter är det område i Experience Cloud där administratörer kan definiera användarroller och åtkomstprinciper för att hantera åtkomstbehörigheter för funktioner och objekt i ett produktprogram.

Genom Behörigheter kan du skapa och hantera roller samt tilldela önskade resursbehörigheter för dessa roller. Med behörigheter kan du också hantera etiketter, sandlådor och användare som är kopplade till en viss roll.

Omedelbart efter [att du har skapat en ny roll](#create-a-new-role) återgår du till fliken **[!UICONTROL Roles]**. Om du redigerar behörigheter för en befintlig roll väljer du rollen på fliken **[!UICONTROL Roles]**. Du kan också använda filteralternativet för att filtrera resultaten för att hitta en roll.

## Filtrera roller

Markera trattikonen (![Filterikon](/help/images/icons/filter.png)) om du vill visa en lista med filterkontroller för att begränsa resultatet.

![flac-filters](../../images/flac-ui/flac-filters.png)

Följande filter är tillgängliga för roller i användargränssnittet:

| Filter | Beskrivning |
| --- | --- |
| [!UICONTROL Created between] | Välj ett startdatum och/eller ett slutdatum för att definiera ett datumintervall som resultaten ska filtreras efter. |
| [!UICONTROL Created by] | Filtrera efter rollskapare genom att välja en användare i listrutan. |
| [!UICONTROL Modified between] | Välj ett startdatum och/eller ett slutdatum för att definiera ett datumintervall som resultaten ska filtreras efter. |
| [!UICONTROL Modified by] | Filtrera efter rollmodifierare genom att välja en användare i listrutan. |

Om du vill ta bort ett filter väljer du X på ikonen för piller för filtret i fråga eller väljer **[!UICONTROL Clear all]** om du vill ta bort alla filter.

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## Rollinformation

Välj rollen på fliken **[!UICONTROL Roles]**, som öppnar rollens informationssida.

![flac-details](../../images/flac-ui/flac-details.png)

Fliken Detaljer innehåller en översikt över rollen. I översikten visas rollnamn, rollbeskrivning, namnet på den användare som skapade och ändrade rollen, när rollen skapades och ändrades samt behörigheter som är kopplade till rollen. Rollnamnet och rollbeskrivningen kan ändras om det behövs.

## Hantera etiketter för en roll

Välj fliken **[!UICONTROL Labels]** för att öppna sidan med rolletiketter och välj sedan **[!UICONTROL Add labels]** för att tilldela rollens etiketter.

![flac-labels](../../images/flac-ui/flac-labels.png)

Etiketter visas på den här sidan. I listan visas etikettnamn, eget namn, kategori och beskrivning.

Markera etiketterna i listan som du vill lägga till i rollen och välj sedan **[!UICONTROL Save]**

![flash-add-labels](../../images/flac-ui/flac-add-labels.png)

Tillagda etiketter visas under fliken **[!UICONTROL Labels]**.

![ej tillagda etiketter](../../images/flac-ui/flac-added-labels.png)

Om du vill ta bort en etikett från en roll väljer du ikonen **X** bredvid etikettens namn.

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## Hantera sandlådor för roll

Välj fliken **[!UICONTROL Sandboxes]** för att öppna sidan med rollsandlådor. Här visas en lista med sandlådor som har lagts till i rollen.

![flac-sandbox](../../images/flac-ui/flac-sandboxes.png)

Om du vill lägga till fler sandlådor i en roll väljer du **[!UICONTROL Edit]**.

![flash-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

På nästa skärm får du en fråga om du vill välja vilka resursbehörigheter som finns i sandlådor som ska inkluderas i rollen med hjälp av listrutan. När du är klar väljer du **[!UICONTROL Save and exit]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## Hantera användare för roll

Välj fliken **[!UICONTROL Users]** för att öppna sidan med roller och välj sedan **[!UICONTROL Add Users]** för att tilldela användare till rollen.

![flash-users](../../images/flac-ui/flac-users.png)

Välj de användare i listan som du vill lägga till i rollen. Du kan också använda sökfältet för att söka efter användaren genom att ange namn eller e-postadress och sedan välja **[!UICONTROL Save]**

![flash-add-users](../../images/flac-ui/flac-add-users.png)

Tillagda användare visas på fliken **[!UICONTROL Users]**.

![ej tillagda användare](../../images/flac-ui/flac-added-users.png)

Om du vill ta bort en användare från en roll väljer du ikonen **X** bredvid användarnamnet.

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

Följande video är tänkt att ge stöd för din förståelse för att skapa en ny roll och hantera användare för den rollen.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Hantera API-autentiseringsuppgifter för roll {#manage-api-credentials-for-role}

Välj fliken **[!UICONTROL API credentials]** för att öppna sidan för roller-API-autentiseringsuppgifter och välj sedan **[!UICONTROL Add API credentials]** för att tilldela API-autentiseringsuppgifter till rollen.

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

Välj API-autentiseringsuppgifterna i listan som du vill lägga till i rollen och välj sedan **[!UICONTROL Save]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

Tillagda API-autentiseringsuppgifter visas på fliken **[!UICONTROL API credentials]**.

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

Om du vill ta bort API-autentiseringsuppgifter från en roll väljer du ikonen **X** bredvid API-autentiseringsuppgiftens namn.

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

Dialogrutan **[!UICONTROL Remove API credentials]** visas och du uppmanas att bekräfta borttagningen.

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Du återgår till fliken **[!UICONTROL API credentials]**.

## Hantera användargrupper för roller

Användargrupper är flera användare som har grupperats tillsammans och har tillgång till samma funktioner.

Välj fliken **[!UICONTROL User groups]** för att öppna sidan med roller och användargrupper. Välj sedan **[!UICONTROL Add Groups]** för att tilldela användargrupper till rollen.

![flash-user-groups](../../images/flac-ui/flac-user-groups.png)

Markera användargrupperna i listan som du vill lägga till i rollen. Du kan också använda sökfältet för att söka efter användargruppen genom att ange namnet på gruppen och sedan välja **[!UICONTROL Save]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

Den tillagda användargruppen visas under fliken **[!UICONTROL User groups]**.

![flash-added-user-groups](../../images/flac-ui/flac-added-user-groups.png)

Om du vill ta bort en användargrupp från en roll väljer du ikonen **X** bredvid användargruppens namn.

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

Dialogrutan **[!UICONTROL Remove user group]** visas och du uppmanas att bekräfta borttagningen.

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Du återgår till fliken **[!UICONTROL User groups]**.

## Lägga till användare i Experience Platform via en roll

Om du vill lägga till en användare i en roll loggar du in på Admin Console och väljer **[!UICONTROL Add users]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

Dialogrutan **[!UICONTROL Add users to your team]** visas. Ange användarens e-postadress, förnamn (valfritt) och efternamn (valfritt).

Välj pennikonen för att välja produkter och användargrupper, välj **[!UICONTROL Adobe Experience Platform]**, välj **[!UICONTROL AEP-Default-All-Users]** och sedan **[!UICONTROL Save]**.

![product-profile](../../images/flac-ui/product-profile.png)

## Nästa steg

Med behörigheter upprättade kan du fortsätta till nästa steg för att [hantera användare](users.md).
