---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;attributbaserad åtkomstkontroll;ABAC
title: Attributbaserad åtkomstkontroll Skapa en roll
description: Det här dokumentet innehåller information om hur du hanterar roller via gränssnittet Behörigheter i Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Hantera roller

Roller definierar åtkomsten som en administratör, en specialist eller en slutanvändare har till resurser i organisationen. I en rollbaserad miljö för åtkomstkontroll är etableringen av användaråtkomst grupperad genom vanliga ansvarsområden och behov. En roll har en given uppsättning behörigheter och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilket synområde eller vilken skrivbehörighet de behöver.

## Skapa en ny roll

Om du vill skapa en ny roll väljer du **[!UICONTROL Roles]** i sidlisten och välj **[!UICONTROL Create Role]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

The **[!UICONTROL Create a new role]** visas där du uppmanas att ange ett namn och en valfri beskrivning.

När du är klar väljer du **[!UICONTROL Confirm]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Välj sedan de resursbehörigheter som du vill inkludera i rollen med hjälp av listrutan.

![flash-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Om du vill lägga till ytterligare resurser väljer du **[!UICONTROL Adobe Experience Platform]** från den vänstra navigeringspanelen, som visar en lista med resurser. Du kan också ange resursnamnet i sökfältet i den vänstra navigeringspanelen.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Klicka och dra den aktuella resursen och släpp den på huvudpanelen.

![flash-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

Välj de resursbehörigheter som du vill inkludera i rollen med hjälp av listrutan. Upprepa detta för alla resurser som du vill inkludera för rollen. När du är klar väljer du **[!UICONTROL Save and exit]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Den nya rollen har skapats och du omdirigeras till **[!UICONTROL Roles]** sidan där du ser den nya rollen visas i listan.

![sparad med nyckelroll](../../images/flac-ui/flac-role-saved.png)

Se avsnitten om [hantera behörigheter för en roll](#manage-permissions-for-a-role) om du vill ha mer information om hur du hanterar rollbehörigheter när de har skapats.

## Duplicera en roll

Om du vill duplicera en befintlig roll väljer du rollen från **[!UICONTROL Roles]** -fliken. Du kan också använda filteralternativet för att filtrera resultatet och hitta den roll du vill duplicera.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Nästa, välj **[!UICONTROL Duplicate]** från skärmens övre högra hörn.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

The **[!UICONTROL Duplicate role]** visas och du uppmanas att bekräfta dupliceringen.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Därefter kommer du till rollens detaljsida där du kan ändra rollens namn och behörigheter. Information, etiketter och sandlådor dupliceras från den tidigare rollen. Användare måste läggas till via fliken Användare. Du kan visa [hantera behörigheter för en roll](permissions.md) om du vill veta mer om hur du lägger till detaljer, etiketter, sandlådor och användare i en roll.

Klicka på vänsterpilen för att gå tillbaka till **[!UICONTROL Roles]** -fliken.

![flash-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

Den nya rollen visas i listan på **[!UICONTROL Roles]** sida.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Ta bort en roll

Markera ellipsen (`…`) bredvid en rolls namn och en listruta visar kontroller för att redigera, ta bort eller duplicera rollen. Välj Ta bort i listrutan.

![flash-role-delete](../../images/flac-ui/flac-role-delete.png)

The **[!UICONTROL Delete user role]** visas och du uppmanas att bekräfta borttagningen.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Du kommer tillbaka till **[!UICONTROL Roles]** -fliken.

## Nästa steg

När en ny roll har skapats kan du fortsätta till nästa steg i [hantera behörigheter för en roll](permissions.md).
