---
keywords: Facebook;facebook;Socialt nätverk;Socialt nätverk;autentisering av sociala nätverk;Autentisering av sociala nätverk
title: Skapa ett mål för sociala nätverk
type: Självstudiekurs
description: Lär dig hur du ansluter till annonskonton för sociala nätverk i Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 19e38faa84d365682e97c2ec1c6352d127c0ac29
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---


# Skapa ett mål för sociala nätverk {#social-network-destinations-workflow}

I den här självstudien används [!DNL Facebook] som exempel, men Adobe Experience Platform-arbetsflödet är detsamma för alla mål för sociala nätverk.

Bläddra till kategorin **[!UICONTROL Social]** i **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**. Välj önskat mål för sociala nätverk och välj sedan **[!UICONTROL Configure]**.

![Anslut till mål för sociala nätverk](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

I steget **Autentisering**, om du tidigare har konfigurerat en anslutning till målet för det sociala nätverket, väljer du **[!UICONTROL Existing Account]** och väljer din befintliga anslutning. Du kan också välja **[!UICONTROL New Account]** för att konfigurera en ny anslutning till målet för det sociala nätverket. Välj **[!UICONTROL Connect to destination]** så dirigeras du till det valda sociala nätverkets mål för att logga in och ansluta Adobe Experience Cloud till ditt sociala nätverks-Ad-konto.

>[!NOTE]
>
>Plattformen stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt konto-ID för det sociala nätverket. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

![Anslut till mål för sociala nätverk - autentiseringssteg](../../assets/catalog/social/workflow/pre-connect.png)

När dina inloggningsuppgifter har bekräftats och Adobe Experience Cloud är anslutet till ditt sociala nätverk kan du välja **[!UICONTROL Next]** för att fortsätta till **[!UICONTROL Setup]**-steget.

![Autentiseringsuppgifterna har bekräftats](../../assets/catalog/social/workflow/post-connect.png)

I steget **[!UICONTROL Setup]** anger du [!UICONTROL Name] och [!UICONTROL Description] för aktiveringsflödet och fyller i [!UICONTROL Account ID] för ditt annonskonto i sociala nätverk.

>[!IMPORTANT]
>
> För [!DNL Facebook]-mål är **[!UICONTROL Account ID]** din [!DNL Facebook Ad Account ID]. Du hittar detta ID i [!DNL Facebook Ads Manager]. Ange `act_` som prefix för ID:t enligt nedan:

![Anslut till mål för sociala nätverk - konfigurationssteg](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> För [!DNL LinkedIn]-mål är **[!UICONTROL Account ID]** din [!DNL LinkedIn Campaign Manager Account ID]. Du hittar detta ID i [!DNL LinkedIn Campaign Manager].

I det här steget kan du även välja alla **[!UICONTROL Marketing action]** som ska gälla för det här målet. Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller välja **[!UICONTROL Next]** om du vill fortsätta arbetsflödet och välja segment som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment till sociala nätverk](#activate-segments), för resten av arbetsflödet.

## Aktivera segment i sociala nätverk {#activate-segments}

Instruktioner om hur du aktiverar segment till sociala nätverk finns i [Aktivera data till mål](../../ui/activate-destinations.md).