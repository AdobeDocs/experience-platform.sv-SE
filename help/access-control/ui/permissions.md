---
keywords: Experience Platform;hem;populära ämnen;produktprofil;hantera behörigheter
solution: Experience Platform
title: Hantera behörigheter för en produktprofil
topic-legacy: user guide
description: Med åtkomstkontrollen i Adobe Experience Platform kan du hantera roller och behörigheter för olika plattformsfunktioner med Adobe Admin Console. Det här dokumentet är en guide till hur du hanterar behörigheter för en produktprofil för Platform.
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: 099bfc0098ebf5a2325f344215c6b21f1c347473
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Hantera behörigheter för en produktprofil

Omedelbart efter [att du har skapat en ny produktprofil](#create-a-new-product-profile) uppmanas du att konfigurera profilens behörigheter. Om du redigerar behörigheter för en befintlig profil markerar du profilen på fliken **[!UICONTROL Product Profiles]** för att öppna profilens informationssida och väljer sedan **[!UICONTROL Permissions]**.

![behörigheter](../images/permissions.png)

Behörigheterna är uppdelade i kategorier och listade på den här sidan. I listan visas kategorinamnet, antalet behörigheter (och hur många som är aktiva) och dess beskrivning.

Välj en kategori i listan för att öppna sidan **[!UICONTROL Edit Permissions]**.

![redigera-behörigheter](../images/edit-permissions.png)

Sidan **[!UICONTROL Edit Permissions]** innehåller en arbetsyta där du kan lägga till och ta bort behörigheter från den valda produktprofilen. Till vänster på skärmen visas en lista med behörighetskategorier. Om du väljer en kategori ändras behörigheterna som visas under **[!UICONTROL Available Permissions Items]**.

Om du till exempel vill uppdatera behörigheter för Profilhantering väljer du **[!UICONTROL Profile Management]**.

![profilhantering](../images/profile-management.png)

Om du vill lägga till en behörighet väljer du plusikonen **(+)** bredvid behörighetens namn. Du kan också välja **[!UICONTROL Add all]** om du vill lägga till alla behörigheter under den aktuella kategorin i profilen. Tillagda behörigheter visas under **[!UICONTROL Included Permission Items]**.

![add-permission](../images/add-permission.png)

>[!NOTE]
>
>Listan **[!UICONTROL Included Permissions Items]** visar bara tillagda behörigheter från den valda kategorin.

Om du vill ta bort en behörighet markerar du ikonen **X** bredvid behörighetens namn eller väljer **[!UICONTROL Remove all]** för att ta bort alla behörigheter i den aktuella kategorin. Borttagna behörigheter visas igen under **[!UICONTROL Available Permission Items]**.

Fortsätt gå igenom de tillgängliga kategorierna och lägg till behörigheter. När du är klar väljer du **[!UICONTROL Save]**.

![remove-permisson](../images/remove-permission.png)

Fliken **[!UICONTROL Permissions]** för produktprofilen visas igen och visar att de valda behörigheterna nu är aktiva.

![behörigheter-uppdaterade](../images/permissions-updated.png)

## Nästa steg

När behörigheter har fastställts kan du fortsätta till nästa steg för att [hantera information och tjänster för en produktprofil](details-and-services.md)
