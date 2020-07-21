---
title: Google AdsDestination
seo-title: Mål för Google Ads
description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör att företag kan betala per klick för annonsering vid textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.
seo-description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör att företag kan betala per klick för annonsering vid textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# [!DNL Google Ads] Destination

## Översikt

[!DNL Google Ads], som tidigare kallades [!DNL Google AdWords], är en onlinereklam som gör det möjligt för företag att betala per klick för annonsering i textbaserade sökningar, grafiska displayer, [!DNL YouTube] videor och mobildisplayer i appen.

## Destinationsspecifikationer

Observera följande information som är specifik för [!DNL Google Ads] destinationer:

* Du kan skicka följande [identiteter](../../identity-service/namespaces.md) till [!DNL Google Ads] mål: **Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Aktiverade målgrupper skapas programmatiskt på [!DNL Google] plattformen.
* Adobe CDP i realtid innehåller för närvarande inga mätvärden som validerar aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Google Ads] och inte har aktiverat [ID-synkroniseringsfunktionen](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Adobe Real-time CDP.

## Förutsättningar

### Befintligt [!DNL Google Ads] konto

[!DNL Google] har pausat alla nya [!DNL Google Ads] integreringar med tredjepartsleverantörer. Du måste ha en befintlig integrering med [!DNL Google Ads] för att kunna utföra tillåtelselista-stegen i nästa avsnitt och skapa ett [!DNL Google Ads] mål i Adobe Real-time CDP.

### Tillåtelselista

>[!NOTE]
>
>tillåtelselista är obligatoriskt innan du ställer in ditt första [!DNL Google Ads] mål i Adobe Real-time CDP. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ads] destinationen i Adobe Real-time CDP måste du kontakta Adobe [!DNL Google] för att få vara med på listan över tillåtna dataleverantörer och för att ditt konto ska kunna läggas till i tillåtelselista. Kontakta [!DNL Google] och lämna följande information:

* **Konto-ID** : detta är Adobes konto-ID med [!DNL Google]. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Kund-ID** : detta är Adobes kundkonto-ID med [!DNL Google]. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* Kontotyp: **AdWords**
* **Google AdWords ID** : Detta är ditt ID med [!DNL Google]. ID-formatet är vanligtvis 123-456-7890.

## Skapa mål

1. In **[!UICONTROL Connections > Destinations]**, select [!DNL Google Ads], and select **[!UICONTROL Create destination]**.
   ![Anslut Google Ads-mål](/help/rtcdp/destinations/assets/google-2-destination.png)

2. I **konfigurationssteget** för att skapa målarbetsflödet fyller du i [!UICONTROL Basic Information] för målet. <br>

   ![Grundläggande information för Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: AdWords är det enda tillgängliga alternativet.
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med [!DNL Google Ads]. ID-formatet är vanligtvis 123-456-7890.
* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobes definierade användningsexempel för marknadsföring eller skapa ett eget exempel för marknadsföring. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Information om de enskilda användningsfallen för marknadsföring som definierats av Adobe finns i [översikten över](/help/data-governance/policies/overview.md#core-actions)dataanvändningspolicyn.

## Aktivera segment för att [!DNL Google Ads]

Instruktioner om hur du aktiverar segment [!DNL Google Ads]finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).

