---
keywords: Facebook;facebook;Socialt nätverk;Socialt nätverk;autentisering av sociala nätverk;Autentisering av sociala nätverk
title: Målarbetsflöde för sociala nätverk
type: Tutorial
seo-title: Målarbetsflöde för sociala nätverk
description: Instruktioner för att ansluta till sociala nätverk och konton
seo-description: Instruktioner för att ansluta till sociala nätverk och konton
translation-type: tm+mt
source-git-commit: d1aa2c825cd679d593cf97d84506058482a7fe8f
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Autentiseringsarbetsflöde för mål för sociala nätverk {#social-network-destinations-workflow}

## Arbetsflöde för att skapa mål för sociala nätverk

I den här självstudiekursen används [!DNL Facebook] som exempel, men arbetsflödet i Adobe Experience Platform är detsamma för alla mål för sociala nätverk när fler läggs till i produkten.

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

I det här steget kan du även välja alla **[!UICONTROL Marketing use case]** som ska gälla för det här målet. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

>[!IMPORTANT]
>
> * För [!DNL Facebook]-mål. **[!UICONTROL Account ID]** är din  [!DNL Facebook Ad Account ID]. Du hittar detta ID i [!DNL Facebook Ads Manager]. Ange `act_` som prefix för ID:t enligt nedan:


![Anslut till mål för sociala nätverk - konfigurationssteg](../../assets/catalog/social/workflow/setup.png)

Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller välja **[!UICONTROL Next]** om du vill fortsätta arbetsflödet och välja segment som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment till sociala nätverk](#activate-segments), för resten av arbetsflödet.

## Aktivera segment i sociala nätverk {#activate-segments}

Instruktioner om hur du aktiverar segment till sociala nätverk finns i [Aktivera data till mål](../../ui/activate-destinations.md).