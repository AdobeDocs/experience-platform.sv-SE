---
keywords: Facebook;facebook;Social network;Social Network;social network authentication;Social network authentication
title: Målarbetsflöde för sociala nätverk
type: Tutorial
seo-title: Målarbetsflöde för sociala nätverk
description: Instruktioner för att ansluta till sociala nätverk och konton
seo-description: Instruktioner för att ansluta till sociala nätverk och konton
translation-type: tm+mt
source-git-commit: 85e6a65e1407ca60e7b63681c045fadaaa24aef9
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Autentiseringsarbetsflöde för mål för sociala nätverk {#social-network-destinations-workflow}

## Arbetsflöde för att skapa mål för sociala nätverk

I den här självstudiekursen används [!DNL Facebook] som exempel, men arbetsflödet i kunddataplattformen i realtid är detsamma för alla mål för sociala nätverk, när mer har lagts till i produkten.

Bläddra till **[!UICONTROL Destinations]** kategorin i **[!UICONTROL Catalog]**> **[!UICONTROL Social]** . Välj önskat mål för sociala nätverk och välj sedan **[!UICONTROL Configure]**.

![Anslut till mål för sociala nätverk](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]** knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

Om du tidigare har konfigurerat en anslutning till ditt sociala nätverk i **autentiseringssteget** väljer du **[!UICONTROL Existing Account]** och väljer din befintliga anslutning. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till ditt sociala nätverk. Välj **[!UICONTROL Connect to destination]** så tar det dig till det valda sociala nätverkets mål för att logga in och ansluta Adobe Experience Cloud till ditt sociala nätverk och annonskonto.

>[!NOTE]
>
>CDP stöder validering av autentiseringsuppgifter i realtid i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt konto-ID för det sociala nätverket. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

![Anslut till mål för sociala nätverk - autentiseringssteg](../../assets/catalog/social/workflow/pre-connect.png)

När dina inloggningsuppgifter har bekräftats och Adobe Experience Cloud är anslutet till ditt sociala nätverk kan du välja **[!UICONTROL Next]** att fortsätta till **[!UICONTROL Setup]** steget.

![Autentiseringsuppgifterna har bekräftats](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

I **[!UICONTROL Setup]** steget anger du ett [!UICONTROL Name] och ett [!UICONTROL Description] för aktiveringsflödet och fyller i [!UICONTROL Account ID] i det sociala nätverkets annonskonto.

I det här steget kan du även välja vilket som helst **[!UICONTROL Marketing use case]** som ska gälla för det här målet. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](../../../data-governance/policies/overview.md#core-actions).

Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

>[!IMPORTANT]
>
> * Marknadsföringsexemplet *Single Identity Personalization* är valt som standard för mål för sociala nätverk och kan inte tas bort.
> * För [!DNL Facebook] destinationer. **[!UICONTROL Account ID]** är din [!DNL Facebook Ad Account ID]. Du hittar detta ID i [!DNL Facebook Ads Manager]. Lägg till följande ID `act_` som prefix:


![Anslut till mål för sociala nätverk - konfigurationssteg](../../assets/catalog/social/workflow/setup.png)

Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment till sociala nätverk](#activate-segments), för resten av arbetsflödet.

## Aktivera segment i sociala nätverk {#activate-segments}

Instruktioner om hur du aktiverar segment till sociala nätverk finns i [Aktivera data till mål](../../ui/activate-destinations.md).