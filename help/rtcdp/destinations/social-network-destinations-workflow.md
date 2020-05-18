---
title: Målarbetsflöde för sociala nätverk
seo-title: Målarbetsflöde för sociala nätverk
description: Instruktioner för att ansluta till sociala nätverk och konton
seo-description: Instruktioner för att ansluta till sociala nätverk och konton
translation-type: tm+mt
source-git-commit: ab53e2efffed536e8028beabd64aee843d1eeee8
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Autentiseringsarbetsflöde för mål för sociala nätverk {#social-network-destinations-workflow}

## Arbetsflöde för att skapa mål för sociala nätverk

I den här självstudiekursen används Facebook som exempel, men arbetsflödet i Adobes kunddataplattform i realtid är detsamma för alla mål för sociala nätverk, när fler läggs till i produkten.

1. Bläddra **[!UICONTROL Destinations > Catalog]** till **[!UICONTROL Social]** kategorin i. Välj önskat mål för sociala nätverk och välj sedan **[!UICONTROL Connect destination]**.

   ![Anslut till mål för sociala nätverk](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Om du tidigare har konfigurerat en anslutning till ditt sociala nätverk i **autentiseringssteget** väljer du **[!UICONTROL Existing Account]** och väljer din befintliga anslutning. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till ditt sociala nätverk. Välj **[!UICONTROL Connect to destination]** så tar det dig till det valda sociala nätverkets mål för att logga in och ansluta Adobe Experience Cloud till ditt sociala nätverks annonskonto.

   >[!NOTE]
   >
   >Adobe CDP i realtid stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt konto-ID för sociala nätverk. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Anslut till mål för sociala nätverk - autentiseringssteg](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. När dina inloggningsuppgifter har bekräftats och Adobe Experience Cloud är anslutet till ditt sociala nätverk kan du välja **[!UICONTROL Next]** att fortsätta till **[!UICONTROL Setup]** steget.

   ![Autentiseringsuppgifterna har bekräftats](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. I **[!UICONTROL Setup]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet och fyller i **[!UICONTROL Account ID]** i det sociala nätverkets annonskonto. Välj alla användningsfall för marknadsföring som ska gälla för den här destinationen. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   >[!IMPORTANT]
   >
   > För Facebook-destinationer. **[!UICONTROL Account ID]** är ditt Facebook-konto-ID. Du hittar detta ID i Facebook Ads Manager. Lägg till följande ID `act_` som prefix:

   ![Anslut till mål för sociala nätverk - konfigurationssteg](/help/rtcdp/destinations/assets/social-network-setup-step.png)

5. Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment till sociala nätverk](#activate-segments), för resten av arbetsflödet.

## Aktivera segment i sociala nätverk {#activate-segments}

Instruktioner om hur du aktiverar segment till sociala nätverk finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).


<!--

// update IMPORTANT note in step 4 after marketing use cases are released for RTCDP

    >[!IMPORTANT]
    >
    > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed. 
    > * For Facebook destinations. **[!UICONTROL Account ID]** is your Facebook Ad Account ID. You can find this ID in the Facebook Ads Manager. Prefix the ID with `act_` as shown below: 

    ![Connect to social network destination - setup step](/help/rtcdp/destinations/assets/social-networks-setup-step.png)