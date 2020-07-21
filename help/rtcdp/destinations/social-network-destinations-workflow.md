---
title: Målarbetsflöde för sociala nätverk
seo-title: Målarbetsflöde för sociala nätverk
description: Instruktioner för att ansluta till sociala nätverk och konton
seo-description: Instruktioner för att ansluta till sociala nätverk och konton
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# Autentiseringsarbetsflöde för mål för sociala nätverk {#social-network-destinations-workflow}

## Arbetsflöde för att skapa mål för sociala nätverk

I den här självstudiekursen används [!DNL Facebook] som exempel, men arbetsflödet i Adobe Customer Data Platform i realtid är detsamma för alla mål för sociala nätverk när mer har lagts till i produkten.

1. Bläddra **[!UICONTROL Destinations > Catalog]** till **[!UICONTROL Social]** kategorin i. Välj önskat mål för sociala nätverk och välj sedan **[!UICONTROL Connect destination]**.

   ![Anslut till mål för sociala nätverk](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Om du tidigare har konfigurerat en anslutning till ditt sociala nätverk i **autentiseringssteget** väljer du **[!UICONTROL Existing Account]** och väljer din befintliga anslutning. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till ditt sociala nätverk. Välj **[!UICONTROL Connect to destination]** så tar det dig till vald destination för sociala nätverk för att logga in och ansluta Adobe Experience Cloud till ditt annonskonto för sociala nätverk.

   >[!NOTE]
   >
   >Adobe CDP i realtid stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt konto-ID för sociala nätverk. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Anslut till mål för sociala nätverk - autentiseringssteg](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. När dina inloggningsuppgifter har bekräftats och Adobe Experience Cloud är anslutet till ditt sociala nätverk kan du välja **[!UICONTROL Next]** att fortsätta till **[!UICONTROL Setup]** steget.

   ![Autentiseringsuppgifterna har bekräftats](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. I **[!UICONTROL Setup]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet och fyller i **[!UICONTROL Account ID]** i det sociala nätverkets annonskonto. <br> I det här steget kan du även välja vilket som helst **[!UICONTROL Marketing use case]** som ska gälla för det här målet. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobes definierade användningsexempel för marknadsföring eller skapa ett eget exempel för marknadsföring. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Information om de enskilda användningsfallen för marknadsföring som definierats av Adobe finns i [översikten över](/help/data-governance/policies/overview.md#core-actions)dataanvändningspolicyn. <br> Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   >[!IMPORTANT]
   >
   > * Marknadsföringsexemplet *Single Identity Personalization* är valt som standard för mål för sociala nätverk och kan inte tas bort.
   > * För [!DNL Facebook] destinationer. **[!UICONTROL Account ID]** är din [!DNL Facebook Ad Account ID]. Du hittar detta ID i [!DNL Facebook Ads Manager]. Lägg till följande ID `act_` som prefix:


   ![Anslut till mål för sociala nätverk - konfigurationssteg](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment till sociala nätverk](#activate-segments), för resten av arbetsflödet.

## Aktivera segment i sociala nätverk {#activate-segments}

Instruktioner om hur du aktiverar segment till sociala nätverk finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).