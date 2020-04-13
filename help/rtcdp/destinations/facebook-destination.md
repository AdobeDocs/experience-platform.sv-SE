---
title: Facebook-mål
seo-title: Facebook-mål
description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
seo-description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Facebook-mål

>[!IMPORTANT]
>
>Facebook-målet i Adobe Real-time CDP är för närvarande i betaversion och är inte tillgängligt för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt

Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.

## Destinationsspecifikationer

### Aktiveringstyp

Segmentexport - du exporterar alla medlemmar i ett segment (publik) med sina identifierare (namn, telefonnummer osv.) används i Facebook-målet

## Förutsättningar

Innan du kan skicka målgruppssegment till [!DNL Facebook]kontrollerar du att du uppfyller följande krav:

1. Ditt [!DNL Facebook] användarkonto måste ha behörigheten **Hantera kampanjer** aktiverad för det annonskonto som du tänker använda.
2. Lägg till **Adobe Experience Cloud** -företagskontot som annonspartner i ert [!DNL Facebook Ad Account]företag. Använd `business ID=206617933627973`. Mer information finns i [Lägg till partners i din Business Manager](https://www.facebook.com/business/help/1717412048538897) .
   >[!IMPORTANT]
   > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera behörigheten **Hantera kampanjer** . Detta krävs för [!DNL Adobe Real-time CDP] integreringen.
3. Läs och signera [!DNL Facebook Custom Audiences] användarvillkoren. För att göra detta, gå till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, var `accountID` är din [!DNL Facebook Ad Account ID].


## Koppla mål

Mer information om hur du ansluter Facebook-målet finns i [autentiseringsarbetsflöde](/help/rtcdp/destinations/social-network-destinations-workflow.md)för mål för sociala nätverk.


## Aktivera segment till Facebook

Instruktioner om hur du aktiverar segment till Facebook finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).