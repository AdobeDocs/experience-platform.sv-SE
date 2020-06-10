---
title: Mål för Google Ad Manager
seo-title: Mål för Google Ad Manager
description: 'Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar. '
seo-description: 'Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar. '
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# Mål för Google Ad Manager

## Översikt

Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.

## Destinationsspecifikationer

Observera följande information som är specifik för Google Ad Manager-mål:

* Du kan skicka följande [identiteter](../../identity-service/namespaces.md) till Google Ad Manager-mål: **Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Aktiverade målgrupper skapas programmatiskt i Google-plattformen.
* Adobe CDP i realtid innehåller för närvarande inga mätvärden som validerar aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Ad Manager och inte har aktiverat [ID-synkroniseringsfunktionen](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Adobe CDP i realtid.

## Förutsättningar

### Tillåt lista

>[!NOTE]
>
>Listan över tillåtna är obligatorisk innan du konfigurerar ditt första Google Ad Manager-mål i Adobe Real-time CDP. Kontrollera att processen Tillåt som beskrivs nedan har slutförts av Google innan du skapar ett mål.

Innan du skapar Google Ad Manager-målet i Adobe Real-time CDP måste du kontakta Google för att Adobe ska tas med i listan över tillåtna dataleverantörer och ditt konto ska läggas till i listan över tillåtna. Kontakta Google och lämna följande information:

* **Konto-ID** : detta är Adobes konto-ID med Google. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Kund-ID** : detta är Adobes kundkonto-ID med Google. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Nätverks-ID** : det här är ditt konto hos Google Ad Manager
* **Målgruppslänks-ID** : det här är ditt konto hos Google Ad Manager
* Din kontotyp. **DFP av Google** eller **AdX-köpare**.

## Skapa mål

1. I **[!UICONTROL Connections > Destinations]** väljer du Google Ad Manager och sedan **[!UICONTROL Create destination]**.
   ![Anslut Google Ad Manager-mål](/help/rtcdp/destinations/assets/google-1-destination.png)

2. I arbetsflödet Skapa mål fyller du i [!UICONTROL Basic Information] för målet. <br>
   ![Grundläggande information Google Ad Manager](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `DFP by Google` för DoubleClick för utgivare
   * Använd `AdX buyer` för Google AdX
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med Google. Detta kan vara ditt nätverks-ID eller ditt Audience Link-ID. Vanligtvis är detta ett åttasiffrigt ID.

>[!NOTE]
>
>När du konfigurerar en Google Ad Manager-destination ska du samarbeta med din kontohanterare för Google eller Adobe-representant för att ta reda på vilken kontotyp du har.

## Aktivera segment till Google Ad Manager

Instruktioner om hur du aktiverar segment till Google Ad Manager finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).