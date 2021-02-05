---
keywords: Dubbelklicka på Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Google Display & Video 360 Connection Destination
description: Display & Video 360, tidigare DoubleClick Bid Manager, är ett verktyg som används för att utföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] anslutning

[!DNL Display & Video 360], tidigare kallat  [!DNL DoubleClick Bid Manager], är ett verktyg som används för att genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display-, Video- och Mobile-material.

## Destinationsspecifikationer

Observera följande information som är specifik för [!DNL Google Display & Video 360]-mål:

* Du kan skicka följande [identiteter](../../../identity-service/namespaces.md) till [!DNL Google Ads] mål: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), Google cookie ID, IDFA, GAID, Roku ID:n, Microsoft ID:n och Amazon Fire TV ID:n.
   * Google använder [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) för målanvändare i Kalifornien och Google Cookie-ID för alla andra användare.
* Aktiverade målgrupper skapas programmatiskt i Google-plattformen.
* Plattformen har för närvarande inte något mätvärde för att validera aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Display &amp; Video 360 och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Platform.

### Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) till Google-målet.

## Förutsättningar

### Tillåtelselista

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar ditt första [!DNL Google Display & Video 360]-mål i Platform. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts av Google innan du skapar ett mål.

Innan du skapar målet [!DNL Google Display & Video 360] i Platform måste du kontakta Google och be om att Adobe finns med i listan över tillåtna dataleverantörer och att ditt konto läggs till i tillåtelselista. Kontakta Google och lämna följande information:

* **Konto-ID** : detta är Adobe-ID med Google. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Kund-ID** : det här är Adobe kundkonto-ID med Google. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Kontotyp**: kan bara användas  **[!DNL Invite advertiser]** för att låta målgrupper delas med ett visst varumärke i ditt Display &amp; Video 360-konto eller  **[!DNL Invite partner]** för att tillåta att målgrupper delas med alla varumärken i ditt Display &amp; Video 360-konto.

## Konfigurera mål

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du [!DNL Google Display & Video 360] och väljer **[!UICONTROL Configure]**.

![Connect Google Display &amp; Video 360 destination](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan [!UICONTROL Activate] och [!UICONTROL Configure] finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

I steget **Konfigurera** i arbetsflödet för att skapa mål fyller du i [!UICONTROL Basic Information] för målet samt i de användningsfall för marknadsföring som ska gälla för det här målet.

![Grundläggande information, Google Display och Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `Invite Advertiser` för att tillåta att målgrupper delas endast till ett visst varumärke i ditt Display &amp; Video 360-konto.
   * Använd `Invite Partner` för att tillåta att målgrupper delas med alla varumärken i ditt Display &amp; Video 360-konto.
* **[!UICONTROL Account ID]**: Fyll i ditt  **[!DNL Invite partner]** eller ditt  **[!DNL Invite advertiser]** konto-ID med Google. Vanligtvis är detta ett ID med sex eller sju siffror.
* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>När du konfigurerar ett [!DNL Google Display & Video 360]-mål ska du samarbeta med din [!DNL Google Account Manager]- eller Adobe-representant för att förstå vilken kontotyp du har.

## Aktivera segment till [!DNL Google Display & Video 360]

Instruktioner om hur du aktiverar segment till [!DNL Google Display & Video 360] finns i [Aktivera data till mål](../../ui/activate-destinations.md).

## Exporterade data

Kontrollera ditt [!DNL Google Display & Video 360]-konto för att kontrollera om data har exporterats till [!DNL Google Display & Video 360]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.