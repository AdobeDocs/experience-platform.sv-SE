---
keywords: Google ads;Google ads;Google Adwords;Google AdWords;Google Adwords
title: Google Ads-anslutning
description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör att företag kan betala per klick för annonsering vid textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.
translation-type: tm+mt
source-git-commit: 0759919dc458798ca4bc5f233a9cb319194ea534
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---


# [!DNL Google Ads] anslutning

[!DNL Google Ads], som tidigare kallades  [!DNL Google AdWords], är en onlinereklam som gör det möjligt för företag att betala per klick för annonsering över textbaserade sökningar, grafiska skärmar,  [!DNL YouTube] videor och mobilskärmar i appen.

## Destinationsspecifikationer

Observera följande information som är specifik för [!DNL Google Ads]-mål:

* Aktiverade målgrupper skapas programmatiskt i [!DNL Google]-plattformen.
* Plattformen har för närvarande inte något mätvärde för att validera aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Google Ads] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID-tjänsten tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Platform.

### Identiteter som stöds {#supported-identities}

[!DNL Google Ad Manager] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | [!DNL Apple ID for Advertisers] | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), även kallat  [!DNL Device ID]. Ett numeriskt 38-siffrigt enhets-ID som Audience Manager associerar med varje enhet som det interagerar med. | Google använder [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) för målanvändare i Kalifornien och Google Cookie ID för alla andra användare. |
| [!DNL Google] cookie-ID | [!DNL Google] cookie-ID | [!DNL Google] använder detta ID för att rikta sig till användare utanför Kalifornien. |
| RIDA | Roku-ID för annonsering. Detta ID identifierar Roku-enheter unikt. |  |
| MAID | Microsoft Advertising ID. Detta ID identifierar unikt enheter som kör Windows 10. |  |
| Amazon Fire TV-ID | Detta ID identifierar Amazon Fire TV-program unikt. |  |

### Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) till Google-målet.

## Förutsättningar

### Befintligt [!DNL Google Ads]-konto

>[!IMPORTANT]
>
> [!DNL Google] har ersatt nya  [!DNL Google Ads] cookie-integreringar med tredjepartsleverantörer. För att kunna utföra tillåtelselista-stegen i nästa avsnitt måste du ha en befintlig integrering med [!DNL Google Ads]. Därför rekommenderar vi att du använder [!DNL Google Ads] för att konfigurera en [!DNL Google Customer Match]-integrering. Mer information om hur du skapar en [!DNL Google Customer Match]-integration finns i självstudiekursen om hur du skapar en [[!DNL Google Customer Match]](./google-customer-match.md)-anslutning.

### Tillåtelselista

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar ditt första [!DNL Google Ads]-mål i Platform. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ads]-målet i Platform måste du kontakta [!DNL Google] för att Adobe ska tas med i listan över tillåtna dataleverantörer och för att ditt konto ska läggas till i tillåtelselista. Kontakta [!DNL Google] och lämna följande information:

* **Konto-ID** : det här är Adobe konto ID med  [!DNL Google]. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Kund-ID** : det här är Adobe kundkonto-ID med  [!DNL Google]. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* Kontotyp: **AdWords**
* **Google AdWords-ID** : Detta är ditt ID med  [!DNL Google]. ID-formatet är vanligtvis 123-456-7890.

## Konfigurera mål

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du [!DNL Google Ads] och väljer **[!UICONTROL Configure]**.

![Anslut Google Ads-mål](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

I steget **Konfigurera** i arbetsflödet för att skapa mål fyller du i [!UICONTROL Basic Information] för målet.

![Grundläggande information för Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: AdWords är det enda tillgängliga alternativet.
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med  [!DNL Google Ads]. ID-formatet är vanligtvis 123-456-7890.
* **[!UICONTROL Marketing action]**: Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

## Aktivera segment till [!DNL Google Ads]

Instruktioner om hur du aktiverar segment till [!DNL Google Ads] finns i [Aktivera data till mål](../../ui/activate-destinations.md).

## Exporterade data

Kontrollera ditt [!DNL Google Ads]-konto för att kontrollera om data har exporterats till [!DNL Google Ads]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.