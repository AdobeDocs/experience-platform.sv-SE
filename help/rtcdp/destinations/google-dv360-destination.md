---
keywords: DoubleClick Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Google Display & Video 360 Destination
seo-title: Google Display & Video 360 Destination
description: Display & Video 360, tidigare DoubleClick Bid Manager, är ett verktyg som används för att utföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile.
seo-description: 'Display & Video 360, tidigare DoubleClick Bid Manager, är ett verktyg som används för att utföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile. '
translation-type: tm+mt
source-git-commit: c66fb4cf0a414e02ceb58becc9d9b59db3fe987b
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] Destination

## Översikt

[!DNL Display & Video 360], tidigare kallat [!DNL DoubleClick Bid Manager], är ett verktyg som används för att genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display-, Video- och Mobile-material.

## Destinationsspecifikationer

Observera följande information som är specifik för [!DNL Google Display & Video 360] destinationer:

* Du kan skicka följande [identiteter](../../identity-service/namespaces.md) till [!DNL Google Display & Video 360] mål: **Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Aktiverade målgrupper skapas programmatiskt i Google-plattformen.
* CDP i realtid i Adobe innehåller för närvarande inga mätvärden som validerar den lyckade aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Display &amp; Video 360 och inte tidigare har aktiverat synkroniseringsfunktionen [för](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID i Experience Cloud ID Service (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Adobe Real-time CDP.

### Exporttyp {#export-type}

**Segmentexport** - du exporterar alla medlemmar i ett segment (publik) till Google-målet.

## Förutsättningar

### Tillåtelselista

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du ställer in ditt första [!DNL Google Display & Video 360] mål i Adobe Real-time CDP. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts av Google innan du skapar ett mål.

Innan du skapar [!DNL Google Display & Video 360] målet i realtid-CDP i Adobe måste du kontakta Google och be Adobe att finnas med i listan över tillåtna dataleverantörer och att ditt konto läggs till i tillåtelselista. Kontakta Google och lämna följande information:

* **Konto-ID** : detta är Adobe-ID med Google. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Kund-ID** : det här är Adobe kundkonto-ID med Google. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Kontotyp**: använd **[!DNL Invite advertiser]** för att tillåta att målgrupper delas till ett specifikt varumärke i ditt Display &amp; Video 360-konto eller för **[!DNL Invite partner]** att tillåta att målgrupper delas med alla varumärken i ditt Display &amp; Video 360-konto.

## Konfigurera mål

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select [!DNL Google Display & Video 360], and select **[!UICONTROL Configure]**.
   ![Connect Google Display &amp; Video 360 destination](/help/rtcdp/destinations/assets/google-dv360-destination.png)

   >[!NOTE]
   >
   >Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]** knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](/help/rtcdp/destinations/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

2. Under **Konfigurera** i arbetsflödet för att skapa mål fyller du i [!UICONTROL Basic Information] för destinationen samt i de användningsfall för marknadsföring som ska gälla för den här destinationen. <br>

   ![Grundläggande information, Google Display och Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Används `Invite Advertiser` för att tillåta att målgrupper delas endast till ett visst varumärke i ditt Display &amp; Video 360-konto.
   * Används `Invite Partner` för att tillåta målgrupper att delas med alla varumärken i ditt Display &amp; Video 360-konto.
* **[!UICONTROL Account ID]**: Fyll i ditt **[!DNL Invite partner]** - eller **[!DNL Invite advertiser]** konto-ID med Google. Vanligtvis är detta ett ID med sex eller sju siffror.
* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](/help/data-governance/policies/overview.md#core-actions).

>[!NOTE]
>
>När du ställer in en [!DNL Google Display & Video 360] destination ska du samarbeta med din [!DNL Google Account Manager] eller Adobe-representant för att förstå vilken kontotyp du har.

## Aktivera segment för att [!DNL Google Display & Video 360]

Instruktioner om hur du aktiverar segment [!DNL Google Display & Video 360]finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).

## Exporterade data

Kontrollera ditt [!DNL Google Display & Video 360] konto om du vill verifiera om data har exporterats till [!DNL Google Display & Video 360] målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.