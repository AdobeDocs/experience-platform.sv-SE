---
keywords: Facebook;facebook;Socialt nätverk;Socialt nätverk;Social autentisering;Social nätverksautentisering
title: Skapa ett socialt mål
type: Tutorial
description: Lär dig hur du ansluter till dina annonskonton för sociala medier i Adobe Experience Platform.
exl-id: a0cdf2b7-b1e8-4a8e-9d5b-58a118e7b689
translation-type: tm+mt
source-git-commit: e2af4fcfe232889f3f928c00c9f9b37cf9754ca1
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Skapa ett socialt mål {#social-network-destinations-workflow}

## Översikt {#overview}

I den här självstudien används [!DNL Facebook] som exempel, men Adobe Experience Platform-arbetsflödet är detsamma för alla sociala mål.

## Konfigurera social destination - videogenomgång {#video}

I videon nedan visas hur du konfigurerar ett socialt mål och aktiverar segment i Adobe Experience Platform. Stegen beskrivs också sekventiellt i de följande avsnitten.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Välj socialt mål {#select-destination}

Bläddra till kategorin **[!UICONTROL Social]** i **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**. Välj önskat socialt mål och välj sedan **[!UICONTROL Configure]**.

![Anslut till social destination](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

## Kontosteg {#account}

I steget **Konto** väljer du **[!UICONTROL Existing Account]** och väljer din befintliga anslutning om du tidigare har konfigurerat en anslutning till ditt sociala mål. Du kan också välja **[!UICONTROL New Account]** för att konfigurera en ny anslutning till ditt sociala mål. Välj **[!UICONTROL Connect to destination]** så dirigeras du till det valda sociala målet för att logga in och ansluta Adobe Experience Cloud till ditt sociala annonskonto.

>[!NOTE]
>
>Plattformen stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt konto-ID. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

![Anslut till socialt mål - autentiseringssteg](../../assets/catalog/social/workflow/pre-connect.png)

När dina inloggningsuppgifter har bekräftats och Adobe Experience Cloud är anslutet till ditt sociala nätverk kan du välja **[!UICONTROL Next]** för att fortsätta till **[!UICONTROL Authentication]**-steget.

![Autentiseringsuppgifterna har bekräftats](../../assets/catalog/social/workflow/post-connect.png)

## Autentiseringssteg {#authentication}

I steget **[!UICONTROL Authentication]** anger du [!UICONTROL Name] och [!UICONTROL Description] för aktiveringsflödet och fyller i [!UICONTROL Account ID] för ditt annonskonto i sociala nätverk.

>[!IMPORTANT]
>
> * För [!DNL Facebook]-mål är **[!UICONTROL Account ID]** din [!DNL Facebook Ad Account ID]. Du hittar detta ID i [!DNL Facebook Ads Manager]. Lägg till `act_` som prefix till ID:t enligt bilden nedan.
> * För [!DNL LinkedIn]-mål är **[!UICONTROL Account ID]** din [!DNL LinkedIn Campaign Manager Account ID]. Du hittar detta ID i [!DNL LinkedIn Campaign Manager].


![Anslut till socialt mål - autentiseringssteg](../../assets/catalog/social/workflow/authentication.png)

I det här steget kan du även välja alla **[!UICONTROL Marketing action]** som ska gälla för det här målet. Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller välja **[!UICONTROL Next]** om du vill fortsätta arbetsflödet och välja segment som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment till sociala mål](#activate-segments), för resten av arbetsflödet.

## Aktivera segment till sociala mål {#activate-segments}

Instruktioner om hur du aktiverar segment till sociala mål finns i [Aktivera data till mål](../../ui/activate-destinations.md).
