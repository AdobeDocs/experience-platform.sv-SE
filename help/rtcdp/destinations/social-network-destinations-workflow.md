---
title: Målarbetsflöde för sociala nätverk
seo-title: Målarbetsflöde för sociala nätverk
description: Instruktioner för att ansluta till sociala nätverk och konton
seo-description: Instruktioner för att ansluta till sociala nätverk och konton
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Autentiseringsarbetsflöde för mål för sociala nätverk {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>Arbetsflödet för att skapa mål för sociala nätverk i Adobe Real-time CDP är för närvarande i betaversion och är inte tillgängligt för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

## Arbetsflöde för att skapa molnlagringsmål

I den här självstudiekursen används Facebook som exempel, men arbetsflödet i Adobes kunddataplattform i realtid kommer att vara detsamma för alla mål för sociala nätverk, när fler läggs till i produkten.

1. Bläddra **[!UICONTROL Connections > Destinations]** till **[!UICONTROL Social]** kategorin i. Välj önskat mål för sociala nätverk och välj sedan **[!UICONTROL Connect destination]**.

   ![Anslut till mål för sociala nätverk](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Om du tidigare har konfigurerat en anslutning till ditt sociala nätverk i **autentiseringssteget** väljer du **[!UICONTROL Existing Account]** och väljer din befintliga anslutning. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till ditt sociala nätverk. Välj **[!UICONTROL Connect to destination]** så tar det dig till vald destination för sociala nätverk för att logga in och ansluta Adobe Experience Cloud till ditt annonskonto för sociala nätverk.

   >[!NOTE]
   >
   >Adobe CDP i realtid stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt konto-ID för sociala nätverk. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Anslut till mål för sociala nätverk - autentiseringssteg](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. När dina inloggningsuppgifter har bekräftats och Adobe Experience Cloud är anslutet till ditt sociala nätverk kan du välja **[!UICONTROL Next]** att fortsätta till **[!UICONTROL Setup]** steget.

   ![Autentiseringsuppgifterna har bekräftats](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. I **[!UICONTROL Setup]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet och fyller i **[!UICONTROL Account ID]** i det sociala nätverkets annonskonto. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   >[!IMPORTANT]
   >
   >För Facebook-destinationer. **[!UICONTROL Account ID]** är ditt Facebook-konto-ID. Du hittar detta ID i Facebook Ads Manager. Lägg till följande ID `act_` som prefix:

   ![Anslut till mål för sociala nätverk - konfigurationssteg](/help/rtcdp/destinations/assets/social-network-step.png)

5. Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment till sociala nätverk](#activate-segments), för resten av arbetsflödet.

## Aktivera segment i sociala nätverk {#activate-segments}

Instruktioner om hur du aktiverar segment till sociala nätverk finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).