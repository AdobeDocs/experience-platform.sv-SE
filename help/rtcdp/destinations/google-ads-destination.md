---
title: Google AdsDestination
seo-title: Mål för Google Ads
description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör att företag kan betala per klick för annonsering vid textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.
seo-description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör att företag kan betala per klick för annonsering vid textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Mål för Google Ads

## Översikt

Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör att företag kan betala per klick för annonsering vid textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.

## Destinationsspecifikationer

Observera följande information som är specifik för Google Ads-destinationer:

* Du kan skicka följande [identiteter](../../identity-service/namespaces.md) till Google Ads-mål: **Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Aktiverade målgrupper skapas programmatiskt i Google-plattformen.
* Adobe CDP i realtid innehåller för närvarande inga mätvärden som validerar aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Ads och inte har aktiverat [ID-synkroniseringsfunktionen](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Audience Manager eller andra program) ber du dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Adobe CDP i realtid.

## Förutsättningar

### Befintligt Google Ads-konto

Google har pausat alla nya Google Ads-integreringar med tredjepartsleverantörer. Du måste ha en befintlig integrering med Google Ads för att kunna utföra vitlistningsstegen i nästa avsnitt och skapa ett Google Ads-mål i Adobe Real-time CDP.

### Vitlista

>[!NOTE]
>
>Vitlistning är obligatoriskt innan du konfigurerar ditt första Google Ads-mål i Adobe Real-time CDP. Kontrollera att vitlistningsprocessen som beskrivs nedan har slutförts av Google innan du skapar ett mål.

Innan du skapar Google Ads-målet i Adobe Real-time CDP måste du kontakta Google och be om att Adobe ska vitlistas som dataleverantör och ditt konto ska vitlistas. Kontakta Google och lämna följande information:

* **Konto-ID** : detta är Adobes konto-ID med Google. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* **Kund-ID** : detta är Adobes kundkonto-ID med Google. Kontakta Adobes kundtjänst eller din Adobe-representant för att få detta ID.
* Kontotyp: **AdWords**
* **Google AdWords ID** : Detta är ditt ID med Google. ID-formatet är vanligtvis 123-456-7890.

## Skapa mål

1. I **[!UICONTROL Connections > Destinations]** väljer du Google Ads och sedan **[!UICONTROL Create destination]**.
   ![Anslut Google Ads-mål](/help/rtcdp/destinations/assets/google-2-destination.png)

2. I arbetsflödet Skapa mål fyller du i [!UICONTROL Basic Information] för målet.
   ![Grundläggande information för Google Ads](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: AdWords är det enda tillgängliga alternativet.
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med Google Ads. ID-formatet är vanligtvis 123-456-7890.

## Aktivera segment för Google Ads

Instruktioner om hur du aktiverar segment till Google Ads finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).

