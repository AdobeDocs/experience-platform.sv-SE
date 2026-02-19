---
keywords: Experience Platform;home;populära topics;access control;attribute-based access control;ABAC
title: Attributbaserad åtkomstkontroll Hantera användare
description: Hantera användare och användargrupper via behörighetsgränssnittet i Adobe Experience Cloud.
exl-id: 16450867-040a-4be1-a6c0-f03d0a1b90ba
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 0%

---

# Hantera användare och lägga till användargrupper {#manage-users}

>[!CONTEXTUALHELP]
>id="platform_permissions_users_about"
>title="Vad är användare?"
>abstract="Användare är de personer som har tillgång till Experience Platform. En enskild användares åtkomst till en organisations resurser hanteras via roller."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/permissions-ui/roles" text="Hantera roller"

Användare är de personer som har tillgång till Adobe Experience Platform. En enskild användares åtkomst till en organisations resurser hanteras via [roller](./roles.md){target="_blank"}. En organisation kan också skapa [användargrupper](#user-groups) för att ge sömlös åtkomst till flera användares samtidigt. Användare hanteras i Admin Console och användare som är kopplade till Adobe Experience Platform produktkort visas som en del av användarlistan i Experience Platform.

## Hantera användare

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform users. To add users to Experience Platform, navigate to Adobe Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add users through the Admin Console, follow the [adding users to Experience Platform](...){#target="_blank"} guide.
-->

Navigera till **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"} om du vill visa organisationens användare. Välj **[!UICONTROL Users]** i den vänstra panelen.

![Arbetsytan Användare i behörigheter.](../../images/ui/users/users-overview.png){zoomable="yes"}

En lista över användare visas. Välj den användare du vill visa i listan. Du kan också använda sökfältet för att söka efter användaren genom att ange användarens namn eller e-postadress.

Fliken **[!UICONTROL Details]** innehåller en översikt över användaren. I översikten visas användarens **[!UICONTROL Name]**, **[!UICONTROL Preferred languages]**, **[!UICONTROL Account Type]**, **[!UICONTROL Authentication ID]**, **[!UICONTROL Email]**, **[!UICONTROL Email verified]** status, **[!UICONTROL Country code]** och **[!UICONTROL Phone number]**.

![En användares arbetsyta Detaljer.](../../images/ui/users/user-details.png){zoomable="yes"}

Välj fliken **[!UICONTROL Roles]** för att visa de roller som användaren är tilldelad till.

![En användares arbetsyta för roller.](../../images/ui/users/user-roles.png){zoomable="yes"}

### Lägga till en roll för en användare {#add-user-role}

Om du vill lägga till en roll för användaren väljer du **[!UICONTROL Add Roles]**.

![Användarens rollarbetsyta med alternativet Lägg till roller markerat.](../../images/ui/users/user-add-roles.png){zoomable="yes"}

Dialogrutan **[!UICONTROL Add Roles]** visas. Markera de roller du vill lägga till för användaren och välj sedan **[!UICONTROL Save]**.

![Dialogrutan Lägg till roller med valda roller och alternativet Spara markerat.](../../images/ui/users/user-roles-add-roles-confirm.png){zoomable="yes"}

### Ta bort en roll från en användare {#remove-user-role}

Om du vill ta bort en roll från användaren markerar du **X** bredvid rollens namn.

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW

>[!NOTE]
>
>Role's that have been added to a user through a user group cannot be removed through the user's role workspace. Role's that have been added through a user group will have an [!Info icon](/help/images/icons/info.png) beside the **X** containing information about the associated user group. To remove the role, the role would need to be [removed from the user group](#remove-user-group-role).
-->

![En användares arbetsyta för roller med borttagningsalternativet för en roll markerat.](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

En bekräftelsedialogruta visas. Välj **[!UICONTROL Confirm]** om du vill ta bort rollen.

![Bekräftelsedialogrutan för att ta bort en roll med alternativet Bekräfta markerat.](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

## Hantera användargrupper {#user-groups}

Användargrupper är flera användare som har grupperats tillsammans och har tillgång till samma funktioner.

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform user groups. To add user groups to Experience Platform, navigate to Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add user groups in the Admin Console, follow the [adding user groups to Experience Platform](...){#target="_blank"} guide.
 -->

Om du vill visa organisationens användare går du till **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}.Välj **[!UICONTROL Groups]** i avsnittet **[!UICONTROL Users]** i den vänstra panelen.

![Arbetsytan för användargrupper i behörigheter.](../../images/ui/users/user-groups-overview.png){zoomable="yes"}

En lista över användargrupper visas. Markera gruppen som du vill visa i listan.

Fliken **[!UICONTROL Details]** innehåller en översikt över användargruppen. I översikten visas gruppernas **[!UICONTROL Name]**, **[!UICONTROL Description]**, **[!UICONTROL User Count]** och **[!UICONTROL Admin count]**.

![Användargruppens arbetsyta Detaljer.](../../images/ui/users/user-group-details.png){zoomable="yes"}

Välj fliken **[!UICONTROL Users]** om du vill visa en lista över användare som har tilldelats gruppen.

![En användargrupps arbetsyta Användare.](../../images/ui/users/user-group-users.png){zoomable="yes"}

Välj fliken **[!UICONTROL Roles]** om du vill visa en lista över de roller som för närvarande är tilldelade gruppen.

![En användargrupps arbetsyta Roller.](../../images/ui/users/user-group-roles.png){zoomable="yes"}

### Lägga till roller i en användargrupp {#add-user-group-role}

Om du vill lägga till en ny roll i gruppen väljer du **[!UICONTROL Add Roles]**.

![En användargrupps arbetsyta Roller med alternativet Lägg till roller markerat.](../../images/ui/users/user-group-add-roles.png){zoomable="yes"}

Dialogrutan **[!UICONTROL Add Roles]** visas. Markera de roller du vill lägga till och välj sedan **[!UICONTROL Save]**. Rollerna läggs till för alla användare som tillhör användargruppen.

![Dialogrutan Lägg till roller med en vald roll och alternativet Spara markerat.](../../images/ui/users/user-group-add-roles-select.png){zoomable="yes"}

### Ta bort roller från en användargrupp {#remove-user-group-role}

Om du vill ta bort en roll från användargruppen markerar du **X** bredvid rollens namn.

![En användargrupps arbetsyta Roller med borttagningsalternativet för en roll markerat.](../../images/ui/users/user-group-remove-role.png){zoomable="yes"}

En bekräftelsedialogruta visas. Välj **[!UICONTROL Confirm]** om du vill ta bort rollen.

![Bekräftelsedialogrutan för att ta bort en roll med alternativet Bekräfta markerat.](../../images/ui/users/user-group-remove-role-confirm.png){zoomable="yes"}

## API-autentiseringsuppgifter

>[!IMPORTANT]
>
>Det är bara systemadministratörer som kan visa och hantera API-autentiseringsuppgifter i behörigheter.

Om du vill använda Experience Platform API:er som användare eller utvecklare måste en systemadministratör lägga till API-autentiseringsuppgifter utöver en rolls angivna behörighetsgrupp. Med behörigheter kan du tilldela roller tidigare skapade API-autentiseringsuppgifter som tilldelats Experience Platform-produkten. En fullständig guide om hur du skapar och tilldelar API-autentiseringsuppgifter samt de behörigheter som behövs finns i den stegvisa självstudiekursen i [autentisera och få åtkomst till Experience Platform API:er](/help/landing/api-authentication.md){target="_blank"}.

Navigera till **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"} om du vill visa dina organisations-API-autentiseringsuppgifter som är kopplade till Experience Platform. Välj **[!UICONTROL API Credentials]** i avsnittet **[!UICONTROL Users]** i den vänstra panelen.

![Arbetsytan API-autentiseringsuppgifter i behörigheter.](../../images/ui/users/api-credentials-overview.png){zoomable="yes"}

>[!NOTE]
>
> Välj **[!UICONTROL Edit in admin console]** om du vill visa organisationens API-autentiseringsuppgifter för alla produkter i organisationen eller om du vill ha mer information om autentiseringsuppgifterna.

En lista över API-autentiseringsuppgifter visas. Välj de API-autentiseringsuppgifter som du vill visa i listan.

Fliken **[!UICONTROL Details]** innehåller en översikt över API-autentiseringsuppgifterna. I översikten visas inloggningsuppgifterna **[!UICONTROL Name]**, **[!UICONTROL Modified]** date, **[!UICONTROL Modified By]** attribute, **[!UICONTROL Created]** date, **[!UICONTROL Created by]** attribute, **[!UICONTROL API key]**, **[!UICONTROL Technical ID]** och **[!UICONTROL Email]**.

![En API-autentiseringsuppgifts informationsyta.](../../images/ui/users/api-credential-details.png){zoomable="yes"}

Klicka på fliken **[!UICONTROL Roles]**.  En lista över roller som är associerade med API-autentiseringsuppgifterna visas.

![En API-autentiseringsuppgiftens arbetsyta Roller.](../../images/ui/users/api-credential-roles.png){zoomable="yes"}

### Lägg till en roll i en API-autentiseringsuppgift {#add-api-credential-role}

Om du vill lägga till en roll i API-autentiseringsuppgifterna väljer du **[!UICONTROL Add Roles]**.

![API-autentiseringsuppgiftens arbetsyta med alternativet Lägg till roller markerat.](../../images/ui/users/api-credential-add-roles.png){zoomable="yes"}

Dialogrutan **[!UICONTROL Add Roles]** visas. Markera de roller du vill lägga till för användaren och välj sedan **[!UICONTROL Save]**.

![Dialogrutan Lägg till roller med valda roller och alternativet Spara markerat.](../../images/ui/users/api-credential-add-roles-select.png){zoomable="yes"}

### Ta bort en roll från en API-referens {#remove-api-credential-role}

Om du vill ta bort en roll från API-autentiseringsuppgifterna markerar du **X** bredvid API-autentiseringsuppgiftens namn.

![En arbetsyta för roller för API-autentiseringsuppgifter med borttagningsalternativet för en roll markerat.](../../images/ui/users/api-credential-remove-role.png){zoomable="yes"}

En bekräftelsedialogruta visas. Välj **[!UICONTROL Confirm]** om du vill ta bort rollen.

![Bekräftelsedialogrutan för att ta bort en roll med alternativet Bekräfta markerat.](../../images/ui/users/api-credential-remove-role-confirm.png){zoomable="yes"}

## Nästa steg

Nu vet du hur du visar information och roller för en användare, en användargrupp och API-autentiseringsuppgifter. Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontroll](../overview.md).

<!--
The following video is intended to support your understanding of developer and API credentials.

>[!VIDEO](https://video.tv.adobe.com/v/3426407/?learn=on)
-->