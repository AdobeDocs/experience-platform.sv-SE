---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager
title: Mål för Google Ad Manager
seo-title: Mål för Google Ad Manager
description: 'Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar. '
seo-description: 'Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar. '
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Översikt

[!DNL Google Ad Manager], tidigare känt [!DNL DoubleClick] för förlag eller [!DNL DoubleClick AdX], är en annonseringsplattform från [!DNL Google] vilken förläggarna kan hantera annonser på sina webbplatser, via video och i mobilappar.

## Destinationsspecifikationer

Observera följande information som är specifik för [!DNL Google Ad Manager] destinationer:

* Du kan skicka följande [identiteter](../../identity-service/namespaces.md) till [!DNL Google Ad Manager] mål: **Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Aktiverade målgrupper skapas programmatiskt på [!DNL Google] plattformen.
* CDP i realtid i Adobe innehåller för närvarande inga mätvärden som validerar den lyckade aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Google Ad Manager] och inte har aktiverat [ID-synkroniseringsfunktionen](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL Google] integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Adobe CDP i realtid.

## Förutsättningar

### Tillåtelselista

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du ställer in ditt första [!DNL Google Ad Manager] mål i Adobe Real-time CDP. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ad Manager] målet i realtid-CDP i Adobe måste du kontakta Adobe [!DNL Google] för att få vara med i listan över tillåtna dataleverantörer och för att ditt konto ska läggas till i tillåtelselista. Kontakta [!DNL Google] och lämna följande information:

* **Konto-ID** : det här är Adobe konto ID med [!DNL Google]. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Kund-ID** : det här är Adobe kundkonto-ID med [!DNL Google]. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Nätverks-ID** : det här är ditt konto med [!DNL Google Ad Manager]
* **Målgruppslänks-ID** : det här är ditt konto med [!DNL Google Ad Manager]
* Din kontotyp. **DFP av Google** eller **AdX-köpare**.

## Konfigurera mål

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select [!DNL Google Ad Manager], and select **[!UICONTROL Configure]**.
   ![Anslut Google Ad Manager-mål](/help/rtcdp/destinations/assets/google-1-destination.png)

   >[!NOTE]
   >
   >Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]** knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](/help/rtcdp/destinations/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

2. I **konfigurationssteget** för att skapa målarbetsflödet fyller du i [!UICONTROL Basic Information] för målet. <br>

   ![Grundläggande information Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `DFP by Google` för [!DNL DoubleClick] utgivare
   * Använd `AdX buyer` för [!DNL Google AdX]
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med [!DNL Google]. Detta kan vara ditt nätverks-ID eller ditt Audience Link-ID. Vanligtvis är detta ett åttasiffrigt ID.
* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](/help/data-governance/policies/overview.md#core-actions).

>[!NOTE]
>
> När du ställer in en [!DNL Google Ad Manager] destination ska du samarbeta med din [!DNL Google Account Manager] eller Adobe-representant för att förstå vilken kontotyp du har.

## Aktivera segment för att [!DNL Google Ad Manager]

Instruktioner om hur du aktiverar segment [!DNL Google Ad Manager]finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).

## Exporterade data

Kontrollera ditt [!DNL Google Ad Manager] konto om du vill verifiera om data har exporterats till [!DNL Google Ad Manager] målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.