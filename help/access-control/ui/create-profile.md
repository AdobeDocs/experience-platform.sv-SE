---
keywords: Experience Platform;home;populära topics;product profile
solution: Experience Platform
title: Skapa en ny produktprofil i Adobe Admin Console
description: Det här dokumentet innehåller de steg som krävs för att skapa en ny produktprofil i Adobe Admin Console. Om du vill börja skapa en ny profil går du till fliken Produktprofiler och klickar på Ny profil.
exl-id: 47558f03-c3f7-4ead-affb-fcbfd7f1e918
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Skapa en ny produktprofil i Adobe Admin Console

Om du vill börja skapa en ny profil går du till fliken **[!UICONTROL Product Profiles]** och väljer **[!UICONTROL New Profile]**.

![ny profil](../images/new-profile.png)

Dialogrutan **[!UICONTROL Create a new product profile]** öppnas och du uppmanas att ange en profil, ett valfritt visningsnamn och en valfri beskrivning. Under **[!UICONTROL User Notifications]** kan du växla om användare ska meddelas via e-post när de läggs till eller tas bort från profilen.

När du är klar väljer du **[!UICONTROL Next]**.

![create-new-product-profile](../images/create-new-product-profile.png)

Nästa skärm uppmanar dig att välja vilka Experience Platform-tjänster som ska ingå i profilen. Markera växlingsknappen bredvid en tjänst för att inaktivera den. Om en tjänst är inaktiverad är inte alla funktioner som är kopplade till den tjänsten tillgängliga för användare som är tilldelade den här produktprofilen. När du är klar väljer du **[!UICONTROL Save]**.

![enable-services](../images/enable-services.png)

Kunder som är berättigade till B2B- eller B2P-versionen har tillgång till B2B-gränssnittet. B2B-gränssnittet kan etableras för användare via [!UICONTROL Enable services menu]. Markera växlingsknappen bredvid [!UICONTROL B2B UI] för att aktivera tjänsten för en viss produktprofil och välj sedan **[!UICONTROL Save]**.

Med användargränssnittet för B2B kan användare visa B2B-arbetsflöden för att hantera konton och affärsmöjligheter samt skapa B2B-relaterade segment. Mer information finns i dokumentationen om [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)

Den nya produktprofilen har skapats och du omdirigeras till profilens [sida för redigeringsbehörigheter](#edit-permissions). Mer information om hur du hanterar produktprofiler när de har skapats finns i avsnitten [Hantera behörigheter](#manage-permissions-for-a-product-profile) och [hantera användare](#manage-users-for-a-product-profile).

## Nästa steg

När en ny produktprofil har skapats kan du fortsätta till nästa steg för att [hantera behörigheter för en produktprofil](permissions.md)
