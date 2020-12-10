---
keywords: Google ads;google ads;google adwords;Google AdWords;Google Adwords
title: Google AdsDestination
seo-title: Mål för Google Ads
description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör att företag kan betala per klick för annonsering vid textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.
seo-description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör att företag kan betala per klick för annonsering vid textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.
translation-type: tm+mt
source-git-commit: 7129a375b1bf4623f78989ed75fcd2bb5dad4a02
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---


# [!DNL Google Ads] Destination

## Översikt

[!DNL Google Ads], som tidigare kallades [!DNL Google AdWords], är en onlinereklam som gör det möjligt för företag att betala per klick för annonsering i textbaserade sökningar, grafiska displayer, [!DNL YouTube] videor och mobildisplayer i appen.

## Destinationsspecifikationer

Observera följande information som är specifik för [!DNL Google Ads] destinationer:

* Du kan skicka följande [identiteter](../../../identity-service/namespaces.md) till [!DNL Google Ads] mål: Google cookie ID, IDFA, GAID, Roku ID, Microsoft ID och Amazon Fire TV ID.
* Aktiverade målgrupper skapas programmatiskt på [!DNL Google] plattformen.
* CDP i realtid innehåller för närvarande inte någon mätmetod för validering av lyckad aktivering. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Google Ads] och inte har aktiverat [ID-synkroniseringsfunktionen](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till CDP i realtid.

### Exporttyp {#export-type}

**Segmentexport** - du exporterar alla medlemmar i ett segment (publik) till Google-målet.

## Förutsättningar

### Befintligt [!DNL Google Ads] konto

>[!IMPORTANT]
>
> [!DNL Google] har ersatt nya [!DNL Google Ads] cookie-integreringar med tredjepartsleverantörer. För att kunna utföra tillåtelselista-stegen i nästa avsnitt måste du ha en befintlig integrering med [!DNL Google Ads]. Därför rekommenderar vi att du [!DNL Google Ads] konfigurerar en [!DNL Google Customer Match] integrering. Mer information om hur du skapar en [!DNL Google Customer Match] integrering finns i självstudiekursen om hur du skapar en [[!DNL Google Customer Match]](./google-customer-match.md) anslutning.

### Tillåtelselista

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du ställer in ditt första [!DNL Google Ads] mål i CDP i realtid. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ads] målet i CDP i realtid måste du kontakta Adobe [!DNL Google] för att få vara med i listan över tillåtna dataleverantörer och för att ditt konto ska läggas till i tillåtelselista. Kontakta [!DNL Google] och lämna följande information:

* **Konto-ID** : det här är Adobe konto ID med [!DNL Google]. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Kund-ID** : det här är Adobe kundkonto-ID med [!DNL Google]. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* Kontotyp: **AdWords**
* **Google AdWords ID** : Detta är ditt ID med [!DNL Google]. ID-formatet är vanligtvis 123-456-7890.

## Konfigurera mål

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select [!DNL Google Ads], and select **[!UICONTROL Configure]**.

![Anslut Google Ads-mål](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]** knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

I **konfigurationssteget** för att skapa målarbetsflödet fyller du i [!UICONTROL Basic Information] för målet.

![Grundläggande information för Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: AdWords är det enda tillgängliga alternativet.
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med [!DNL Google Ads]. ID-formatet är vanligtvis 123-456-7890.
* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](../../../data-governance/policies/overview.md#core-actions).

## Aktivera segment för att [!DNL Google Ads]

Instruktioner om hur du aktiverar segment [!DNL Google Ads]finns i [Aktivera data till mål](../../ui/activate-destinations.md).

## Exporterade data

Kontrollera ditt [!DNL Google Ads] konto om du vill verifiera om data har exporterats till [!DNL Google Ads] målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.