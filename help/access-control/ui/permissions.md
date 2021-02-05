---
keywords: Experience Platform;hem;populära ämnen;produktprofil;hantera behörigheter
solution: Experience Platform
title: Hantera behörigheter för en produktprofil
topic: user guide
description: Med åtkomstkontrollen i Adobe Experience Platform kan du hantera roller och behörigheter för olika plattformsfunktioner med Adobe Admin Console. Det här dokumentet är en guide till hur du hanterar behörigheter för en produktprofil för Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Hantera behörigheter för en produktprofil

Omedelbart efter [att du har skapat en ny produktprofil](#create-a-new-product-profile) uppmanas du att konfigurera profilens behörigheter. Om du redigerar behörigheter för en befintlig profil markerar du profilen på fliken **[!UICONTROL Product Profiles]** för att öppna profilens informationssida och klickar sedan på **[!UICONTROL Permissions]**.

![profile-permissions](../images/profile-permissions.png)

Behörigheterna är uppdelade i kategorier och listade på den här sidan. I listan visas kategorinamnet, antalet behörigheter (och hur många som är aktiva) och dess beskrivning.

Välj en kategori i listan för att öppna sidan **[!UICONTROL Edit Permissions]**.

![redigera-behörigheter](../images/edit-permissions.png)

Sidan **[!UICONTROL Edit Permissions]** innehåller en arbetsyta där du kan lägga till och ta bort behörigheter från den valda produktprofilen. Till vänster på skärmen visas en lista med behörighetskategorier. Om du väljer en kategori ändras behörigheterna som visas under **[!UICONTROL Available Permissions Items]**.

![change-permissions-category](../images/change-permissions-category.png)

Om du vill lägga till en behörighet väljer du ikonen **plus (+)** bredvid behörighetens namn. Du kan också välja **[!UICONTROL Add all]** om du vill lägga till alla behörigheter under den aktuella kategorin i profilen. Tillagda behörigheter visas under **[!UICONTROL Included Permission Items]**.

![add-permissions](../images/add-permissions.png)

>[!NOTE]
>
>Listan **[!UICONTROL Included Permissions Items]** visar bara tillagda behörigheter från den valda kategorin.

Om du vill ta bort en behörighet markerar du ikonen **X** bredvid behörighetens namn eller väljer **[!UICONTROL Remove all]** för att ta bort alla behörigheter i den aktuella kategorin. Borttagna behörigheter visas igen under **[!UICONTROL Available Permission Items]**.

Fortsätt gå igenom de tillgängliga kategorierna och lägg till behörigheter. När du är klar väljer du **[!UICONTROL Save]**.

![behörigheter-avsluta](../images/permissions-finish.png)

Fliken **[!UICONTROL Permissions]** för produktprofilen visas igen och visar att de valda behörigheterna nu är aktiva.

![added-permissions](../images/added-permissions.png)

## Nästa steg

När behörigheter har fastställts kan du fortsätta till nästa steg för att [hantera information och tjänster för en produktprofil](details-and-services.md)