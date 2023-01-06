---
keywords: Experience Platform;hem;populära ämnen;produktprofil;hantera behörigheter
solution: Experience Platform
title: Hantera behörigheter för en produktprofil
description: Med åtkomstkontrollen i Adobe Experience Platform kan du hantera roller och behörigheter för olika plattformsfunktioner med Adobe Admin Console. Det här dokumentet är en guide till hur du hanterar behörigheter för en produktprofil för Platform.
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Hantera behörigheter för en produktprofil

Omedelbart efter [skapa en ny produktprofil](#create-a-new-product-profile)uppmanas du att konfigurera profilens behörigheter. Om du redigerar behörigheter för en befintlig profil väljer du profilen på menyn **[!UICONTROL Product Profiles]** för att öppna profilens informationssida och sedan välja **[!UICONTROL Permissions]**.

![behörigheter](../images/permissions.png)

Behörigheterna är uppdelade i kategorier och listade på den här sidan. I listan visas kategorinamnet, antalet behörigheter (och hur många som är aktiva) och dess beskrivning.

Välj en kategori i listan för att öppna **[!UICONTROL Edit Permissions]** sida.

![redigera-behörigheter](../images/edit-permissions.png)

The **[!UICONTROL Edit Permissions]** På sidan finns en arbetsyta där du kan lägga till och ta bort behörigheter från den valda produktprofilen. Till vänster på skärmen visas en lista med behörighetskategorier. Om du väljer en kategori ändras behörigheterna som visas under **[!UICONTROL Available Permissions Items]**.

Om du till exempel vill uppdatera behörigheter för datamodellering väljer du **[!UICONTROL Data Modeling]**.

![profilhantering](../images/profile-management.png)

Om du vill lägga till en behörighet väljer du plugin-programmet **(+)** -ikon bredvid behörighetens namn. Du kan också välja **[!UICONTROL Add all]** om du vill lägga till alla behörigheter i den aktuella kategorin i profilen. Tillagda behörigheter visas under **[!UICONTROL Included Permission Items]**.

![add-permission](../images/add-permission.png)

>[!NOTE]
>
>The **[!UICONTROL Included Permissions Items]** visas endast tillagda behörigheter från den markerade kategorin.

Om du vill ta bort en behörighet väljer du **X** -ikon bredvid behörighetens namn, eller välj **[!UICONTROL Remove all]** om du vill ta bort alla behörigheter i den aktuella kategorin. Borttagna behörigheter visas igen under **[!UICONTROL Available Permission Items]**.

Fortsätt gå igenom de tillgängliga kategorierna och lägg till behörigheter. När du är klar väljer du **[!UICONTROL Save]**.

![remove-permisson](../images/remove-permission.png)

The **[!UICONTROL Permissions]** för produktprofilen visas igen och visar att de valda behörigheterna nu är aktiva.

![behörigheter-uppdaterade](../images/permissions-updated.png)

## Nästa steg

När behörigheter har fastställts kan du fortsätta till nästa steg i [hantera detaljer och tjänster för en produktprofil](details-and-services.md)
