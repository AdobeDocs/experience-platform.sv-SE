---
title: Mål för Google Ad Manager
seo-title: Mål för Google Ad Manager
description: 'Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar. '
seo-description: 'Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar. '
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Översikt

[!DNL Google Ad Manager], tidigare känt [!DNL DoubleClick] för förlag eller [!DNL DoubleClick AdX], är en annonseringsplattform från [!DNL Google] vilken förläggarna kan hantera annonser på sina webbplatser, via video och i mobilappar.

## Destinationsspecifikationer

Observera följande information som är specifik för [!DNL Google Ad Manager] destinationer:

* Du kan skicka följande [identiteter](../../identity-service/namespaces.md) till [!DNL Google Ad Manager] mål: **Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Aktiverade målgrupper skapas programmatiskt på [!DNL Google] plattformen.
* Adobe CDP i realtid innehåller för närvarande inga mätvärden som validerar aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Google Ad Manager] och inte har aktiverat [ID-synkroniseringsfunktionen](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL Google] integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Adobe Real-time CDP.

## Förutsättningar

### Tillåtelselista

>[!NOTE]
>
>tillåtelselista är obligatoriskt innan du ställer in ditt första [!DNL Google Ad Manager] mål i Adobe Real-time CDP. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ad Manager] destinationen i Adobe Real-time CDP måste du kontakta Adobe [!DNL Google] för att få vara med på listan över tillåtna dataleverantörer och för att ditt konto ska kunna läggas till i tillåtelselista. Kontakta [!DNL Google] och lämna följande information:

* **Konto-ID** : detta är Adobes konto-ID med [!DNL Google]. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Kund-ID** : detta är Adobes kundkonto-ID med [!DNL Google]. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Nätverks-ID** : det här är ditt konto med [!DNL Google Ad Manager]
* **Målgruppslänks-ID** : det här är ditt konto med [!DNL Google Ad Manager]
* Din kontotyp. **DFP av Google** eller **AdX-köpare**.

## Skapa mål

1. In **[!UICONTROL Connections > Destinations]**, select [!DNL Google Ad Manager], and select **[!UICONTROL Create destination]**.
   ![Anslut Google Ad Manager-mål](/help/rtcdp/destinations/assets/google-1-destination.png)

2. I **konfigurationssteget** för att skapa målarbetsflödet fyller du i [!UICONTROL Basic Information] för målet. <br>

   ![Grundläggande information Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `DFP by Google` för [!DNL DoubleClick] utgivare
   * Använd `AdX buyer` för [!DNL Google AdX]
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med [!DNL Google]. Detta kan vara ditt nätverks-ID eller ditt Audience Link-ID. Vanligtvis är detta ett åttasiffrigt ID.
* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobes definierade användningsexempel för marknadsföring eller skapa ett eget exempel för marknadsföring. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Information om de enskilda användningsfallen för marknadsföring som definierats av Adobe finns i [översikten över](/help/data-governance/policies/overview.md#core-actions)dataanvändningspolicyn.

> [!NOTE]
>
> När du ställer in en [!DNL Google Ad Manager] destination ska du samarbeta med din [!DNL Google Account Manager] eller Adobes representant för att ta reda på vilken kontotyp du har.

## Aktivera segment för att [!DNL Google Ad Manager]

Instruktioner om hur du aktiverar segment [!DNL Google Ad Manager]finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).