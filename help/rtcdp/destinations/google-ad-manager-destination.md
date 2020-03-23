---
title: Mål för Google Ad Manager
seo-title: Mål för Google Ad Manager
description: 'Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar. '
seo-description: 'Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar. '
translation-type: tm+mt
source-git-commit: d42e4d60d273b08824e177f9aca0f208578ff099

---


# Mål för Google Ad Manager

## Översikt

Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.

## Destinationsspecifikationer

Observera följande information som är specifik för Google Ad Manager-mål:

* Du kan skicka följande [identiteter](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) till Google Ad Manager-mål: **Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Aktiverade målgrupper skapas programmatiskt i Google-plattformen.
* Adobe CDP i realtid innehåller för närvarande inga mätvärden som validerar aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Ad Manager och inte har aktiverat [ID-synkroniseringsfunktionen](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Adobe CDP i realtid.

## Förutsättningar

### Vitlista

>[!NOTE]
>
>Vitlistning är obligatoriskt innan du konfigurerar ditt första Google Ad Manager-mål i Adobe Real-time CDP. Kontrollera att vitlistningsprocessen som beskrivs nedan har slutförts av Google innan du skapar ett mål.

Innan du skapar Google Ad Manager-målet i Adobe Real-time CDP måste du kontakta Google och be om att Adobe vitlistas som dataleverantör och ditt konto vitlistas. Kontakta Google och lämna följande information:

* **Konto-ID** : detta är Adobes konto-ID med Google. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Kund-ID** : detta är Adobes kundkonto-ID med Google. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Nätverks-ID** : det här är ditt konto hos Google Ad Manager
* **Målgruppslänks-ID** : det här är ditt konto hos Google Ad Manager
* Din kontotyp. **DFP av Google** eller **AdX-köpare**.

## Skapa mål

1. Välj Google Ad Manager i **[!UICONTROL Anslutningar > Destinationer]** och välj **[!UICONTROL Skapa mål]**.
   ![Anslut Google Ad Manager-mål](/help/rtcdp/destinations/assets/google-ad-manager-destination.png)

2. Fyll i Grundläggande information för målet i guiden Skapa mål.
   ![Grundläggande information Google Ad Manager](/help/rtcdp/destinations/assets/google-ad-manager-basic-information.png)
* **Namn**: Fyll i det önskade namnet för det här målet.
* **Beskrivning**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **Kontotyp**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `DFP by Google` för DoubleClick för utgivare
   * Använd `AdX buyer` för Google AdX
* **Konto-ID**: Fyll i ditt konto-ID med Google. Detta kan vara ditt nätverks-ID eller ditt Audience Link-ID. Vanligtvis är detta ett åttasiffrigt ID.

>[!NOTE]
>
>När du konfigurerar en Google Ad Manager-destination ska du samarbeta med din kontohanterare för Google eller Adobe-representant för att ta reda på vilken kontotyp du har.

## Aktivera segment till Google Ad Manager

Instruktioner om hur du aktiverar segment till Google Ad Manager finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).