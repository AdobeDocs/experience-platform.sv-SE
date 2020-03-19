---
title: Google Destination
seo-title: Google Destination
description: Adobe CDP integreras i realtid med Google så att ni kan köra och aktivera data i DV360, Google Ad Manager, Google AdWords och Google AdX.
seo-description: Adobe CDP integreras i realtid med Google så att ni kan köra och aktivera data i DV360, Google Ad Manager, Google AdWords och Google AdX.
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Google Destination

## Översikt

Adobe CDP integreras i realtid med Google så att ni kan köra och aktivera data i DV360, Google Ad Manager, Google AdWords Display och Google AdX.

## Destinationsspecifikationer

Observera följande information som är specifik för Google-destinationer:

* Du kan skicka följande [identiteter](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) till Google-mål: **Google cookie ID, IDFA, GAID**.
* Aktiverade målgrupper skapas programmatiskt i Google-plattformen.
* Adobe CDP i realtid innehåller för närvarande inga mätvärden som validerar aktiveringen. Se antalet målgrupper i Google för att validera integreringen och förstå hur data tas bort.

## Förutsättningar

### Vitlista

Innan du ansluter Google-destinationen i Adobe Real-time CDP måste du kontakta Google och be om att ditt konto vitlistas. Kontakta Google och lämna följande information:

* **Konto-ID** : detta är Adobes konto-ID med Google. Kontakta Adobe Support för att få detta ID.
* **Kund-ID** : detta är Adobes kundkonto-ID med Google. Kontakta Adobe Support för att få detta ID.
* **Partner-ID** : Detta är ditt tresiffriga partner-ID hos Google;
* **Nätverks-ID** : detta är ditt konto hos Google;
* **Målgruppslänks-ID** : detta är ditt konto hos Google;
* Din kontotyp. Det kan vara **Bjud in annonsörer**, **Bjud in partner**, **DFP**, **AdWords**, **AdX**.


## Koppla mål

1. I **[!UICONTROL Anslutningar > Destinationer]** väljer du Google och sedan **[!UICONTROL Skapa mål]**.
   ![Anslut Google-mål](/help/rtcdp/destinations/assets/google-destination.png)

2. Fyll i Grundläggande information för målet i guiden Anslut till mål.
   ![Grundläggande information Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Namn**: Fyll i det önskade namnet för det här målet.
* **Beskrivning**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **Kontotyp**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `Invite advertiser` för Google DV360
   * Använd `Invite partner` för Google DV360
   * Använd `DFP by Google` för Google Ad Manager
   * Använd `AdWords` för Google AdWords Display
   * Använd `AdX buyer` för Google AdX
* **Konto-ID**: Fyll i ditt konto-ID med Google.

>[!NOTE]
>
>När du konfigurerar en Google-destination ska du samarbeta med din Google Account Manager eller Adobe-representant för att ta reda på vilken produkttyp ditt konto tillhör. För Google DV360 kan du fråga din kontohanterare för Google vilken produkttyp ditt konto tillhör. 

## Aktivera segment till Google

Instruktioner om hur du aktiverar segment till Google finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).