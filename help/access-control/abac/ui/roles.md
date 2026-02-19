---
keywords: Experience Platform;home;populära topics;access control;attribute-based access control;ABAC
title: Attributbaserad åtkomstkontroll Skapa en roll
description: Hantera roller via behörighetsgränssnittet i Adobe Experience Cloud.
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Hantera roller

<!-- UPDATE ROLES WITH A MORE COMPREHENSIVE EXPLANATION -->

Om du vill börja hantera roller går du till **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"} och väljer **[!UICONTROL Roles]** i den vänstra panelen.

![Arbetsytan Roller i Behörigheter.](../../images/ui/roles/roles-overview.png)

## Skapa en ny roll {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Skapa ny roll"
>abstract="Skapa nya roller för att kategorisera användare som interagerar med din Experience Platform-instans bättre. Du kan t.ex. skapa en roll för ett internt marknadsföringsteam och tillämpa etiketten för reglerade hälsodata (RHD) på den rollen, så att ditt interna marknadsföringsteam kan komma åt skyddad hälsoinformation (PHI). Du kan också skapa en roll för en extern byrå och neka rollåtkomst till PHI-data genom att inte använda RHD-etiketten på den rollen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=sv-SE" text="Hantera en roll"
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="Använd etiketter för en roll"

Om du vill skapa en ny roll väljer du **[!UICONTROL Create role]**.

>[!TIP]
>
>Skrivskyddade roller är tillgängliga direkt. En skrivskyddad roll är en roll som ger en användare möjlighet att visa data, konfiguration och gränssnittsfunktioner utan möjlighet att ändra systemtillståndet. Administratörer kan inte redigera dessa roller, men kan associera användare med rollerna.

![Rollens arbetsyta med alternativet Skapa roll markerat.](../../images/ui/roles/roles-create-role.png)

Dialogrutan **[!UICONTROL Create new role]** visas. Ange en **[!UICONTROL Name]** för rollen, och eventuellt en **[!UICONTROL Description]**, och välj sedan **[!UICONTROL Confirm]**.

![Dialogrutan Skapa nya roller med namnet och beskrivningen ifylld och alternativet Bekräfta markerat.](../../images/ui/roles/roles-create-new-role.png)

Arbetsytan **[!UICONTROL Resources]** visas. Leta reda på resursen som du behöver genom att bläddra, eller genom att ange resursens namn i sökfältet i den vänstra panelen. Lägg till resurser genom att välja ![plusikonen](/help/images/icons/plus.png) bredvid resursens namn.

![Arbetsytan Resurser med alternativet Lägg till för en enskild resurs markerat.](../../images/ui/roles/roles-resources.png)

<!-- ADD IN NOTE ABOUT THE DEFAULT SANDBOX - THIS SHOULD BE MENTIONED IN THE HIGHER LEVEL DOCS, WE MAY BE ABLE TO LINK TO IT -->

Resursen läggs till på huvudarbetsytan. Markera listrutan bredvid resursens namn och välj de behörigheter du vill lägga till i rollen. Du kan välja dem var för sig, välja **[!UICONTROL Add all]** eller leta upp specifika behörigheter genom att ange behörighetsnamnet i sökfältet.

![Arbetsytan Resurser med en enskild resurs listruta utökad och markerad.](../../images/ui/roles/roles-resources-permissions.png)

Fortsätt att välja alla resurser och behörigheter som du vill lägga till i rollen. När du är klar väljer du **[!UICONTROL Save]**.

![Arbetsytan Resurser med alternativet Spara markerat.](../../images/ui/roles/roles-resources-permissions-save.png)

Du får en varning om att rollen har sparats. Välj **[!UICONTROL Close]** om du vill återgå till arbetsytan för **[!UICONTROL Roles]**.

![Arbetsytan Resurser med meddelandet om att åtgärden lyckades och alternativet Stäng markerat.](../../images/ui/roles/roles-resources-permissions-close.png)

Den nya rollen har skapats och du omdirigeras till sidan **[!UICONTROL Roles]** där du ser den nya rollen i listan.

<!-- The following video is intended to support your understanding of creating a new role and managing users for that role.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on) -->

## Duplicera en roll

Om du duplicerar en roll kopieras den över detaljer, behörigheter, etiketter och sandlådor. Användare, användargrupper och API-autentiseringsuppgifter **kopieras inte** och måste läggas till manuellt i rollen.

Om du vill duplicera en befintlig roll söker du efter den roll du vill duplicera på fliken **[!UICONTROL Roles]**. Välj ikonen ![Mer](/help/images/icons/more.png) bredvid rollens namn och välj sedan **[!UICONTROL Duplicate]** i listrutan.

![Arbetsytan Roller med rollens nedrullningsbara meny utökad och alternativet Duplicera markerat.](../../images/ui/roles/role-duplicate.png)

Bekräftelsedialogrutan för kopian visas. Välj **[!UICONTROL Confirm]** för att slutföra dupliceringen av rollen. Den nya rollen sparas under samma namn med `_Copy` som suffix.

![Den duplicerade bekräftelsedialogrutan med alternativet Bekräfta markerat.](../../images/ui/roles/role-duplicate-confirm.png)

Du kan också duplicera en roll från en enskild rolls arbetsyta. Välj den roll du vill duplicera från arbetsytan **[!UICONTROL Roles]** och välj sedan **[!UICONTROL Duplicate]**.

![En enskild rolls arbetsyta med alternativet Duplicera markerat.](../../images/ui/roles/role-duplicate-alt.png)

Bekräftelsedialogrutan för kopian visas. Välj **[!UICONTROL Confirm]** för att slutföra dupliceringen av rollen. Du omdirigeras till den nya rollen.

![Den duplicerade bekräftelsedialogrutan med alternativet Bekräfta markerat.](../../images/ui/roles/role-duplicate-alt-confirm.png)

## Ta bort en roll

Om du vill ta bort en roll kan du hitta rollen som du vill ta bort på fliken **[!UICONTROL Roles]**. Välj ikonen ![Mer](/help/images/icons/more.png) bredvid rollens namn och välj sedan **[!UICONTROL Delete]** i listrutan.

![Arbetsytan Roller med rollens nedrullningsbara meny utökad och alternativet Duplicera markerat.](../../images/ui/roles/role-delete.png)

Bekräftelsedialogrutan för borttagning visas. Välj **[!UICONTROL Confirm]** om du vill ta bort rollen.

![Den duplicerade bekräftelsedialogrutan med alternativet Bekräfta markerat.](../../images/ui/roles/role-duplicate-confirm.png)

Du kan också ta bort en roll från en enskild rolls arbetsyta. Markera den roll du vill ta bort från arbetsytan **[!UICONTROL Roles]** och välj sedan **[!UICONTROL Delete]**.

![En enskild rolls arbetsyta med alternativet Ta bort markerat.](../../images/ui/roles/role-delete-alt.png)

Bekräftelsedialogrutan för borttagning visas. Välj **[!UICONTROL Confirm]** om du vill ta bort rollen.

![Bekräftelsedialogrutan för borttagning med alternativet Bekräfta markerat.](../../images/ui/roles/role-delete-alt-confirm.png)

<!-- ADD PERMISSIONS TO THIS PAGE -->

## Nästa steg

När en ny roll har skapats kan du fortsätta till nästa steg för att [hantera behörigheter för en roll](permissions.md).
