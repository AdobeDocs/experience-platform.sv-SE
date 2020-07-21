---
title: Google Display & Video 360 Destination
seo-title: Google Display & Video 360 Destination
description: Display & Video 360, tidigare DoubleClick Bid Manager, är ett verktyg som används för att utföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile.
seo-description: 'Display & Video 360, tidigare DoubleClick Bid Manager, är ett verktyg som används för att utföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile. '
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] Destination

## Översikt

[!DNL Display & Video 360], tidigare kallat [!DNL DoubleClick Bid Manager], är ett verktyg som används för att genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display-, Video- och Mobile-material.

## Destinationsspecifikationer

Observera följande information som är specifik för [!DNL Google Display & Video 360] destinationer:

* Du kan skicka följande [identiteter](../../identity-service/namespaces.md) till [!DNL Google Display & Video 360] mål: **Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Aktiverade målgrupper skapas programmatiskt i Google-plattformen.
* Adobe CDP i realtid innehåller för närvarande inga mätvärden som validerar aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Display &amp; Video 360 och inte tidigare har aktiverat synkroniseringsfunktionen [för](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID i Experience Cloud ID Service (med Adobe Audience Manager eller andra program) kan du kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Adobe Real-time CDP.

## Förutsättningar

### Tillåtelselista

>[!NOTE]
>
>tillåtelselista är obligatoriskt innan du ställer in ditt första [!DNL Google Display & Video 360] mål i Adobe Real-time CDP. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts av Google innan du skapar ett mål.

Innan du skapar målet i Adobe Real-time CDP måste du kontakta Google och be om att Adobe finns med i listan över tillåtna dataleverantörer och att ditt konto läggs till i tillåtelselista. [!DNL Google Display & Video 360] Kontakta Google och lämna följande information:

* **Konto-ID** : detta är Adobes konto-ID med Google. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Kund-ID** : detta är Adobes kundkonto-ID med Google. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Kontotyp**: använd **[!DNL Invite advertiser]** för att tillåta att målgrupper delas till ett specifikt varumärke i ditt Display &amp; Video 360-konto eller för **[!DNL Invite partner]** att tillåta att målgrupper delas med alla varumärken i ditt Display &amp; Video 360-konto.

## Skapa mål

1. In **[!UICONTROL Connections > Destinations]**, select [!DNL Google Display & Video 360], and select **[!UICONTROL Create destination]**.
   ![Connect Google Display &amp; Video 360 destination](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. Under **Konfigurera** i arbetsflödet för att skapa mål fyller du i [!UICONTROL Basic Information] för destinationen samt i de användningsfall för marknadsföring som ska gälla för den här destinationen. <br>

   ![Grundläggande information, Google Display och Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Används `Invite Advertiser` för att tillåta att målgrupper delas endast till ett visst varumärke i ditt Display &amp; Video 360-konto.
   * Används `Invite Partner` för att tillåta målgrupper att delas med alla varumärken i ditt Display &amp; Video 360-konto.
* **[!UICONTROL Account ID]**: Fyll i ditt **[!DNL Invite partner]** - eller **[!DNL Invite advertiser]** konto-ID med Google. Vanligtvis är detta ett ID med sex eller sju siffror.
* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobes definierade användningsexempel för marknadsföring eller skapa ett eget exempel för marknadsföring. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Information om de enskilda användningsfallen för marknadsföring som definierats av Adobe finns i [översikten över](/help/data-governance/policies/overview.md#core-actions)dataanvändningspolicyn.

>[!NOTE]
>
>När du ställer in en [!DNL Google Display & Video 360] destination ska du samarbeta med din [!DNL Google Account Manager] eller Adobes representant för att ta reda på vilken kontotyp du har.

## Aktivera segment för att [!DNL Google Display & Video 360]

Instruktioner om hur du aktiverar segment [!DNL Google Display & Video 360]finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).