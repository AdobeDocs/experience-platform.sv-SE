---
keywords: Google ad manager;google ad;dubbelklicka;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Google Ad Manager-anslutning
description: Google Ad Manager, som tidigare kallades DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 4df2e7ce9c7e94da4ea0be50ba21232c639e2587
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# [!DNL Google Ad Manager] anslutning

## Översikt {#overview}

[!DNL Google Ad Manager], f.d. DFP  [!DNL DoubleClick for Publishers] ( [!DNL DoubleClick AdX]DFP) eller  [!DNL Google] , är en annonseringsplattform frånvilken förläggarna kan hantera annonser på sina webbplatser, via video och i mobilappar.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Ad Manager]-mål:

* Aktiverade målgrupper skapas programmatiskt i [!DNL Google]-plattformen.
* [!DNL Platform] innehåller för närvarande inga mätvärden som validerar den lyckade aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

## Identiteter som stöds {#supported-identities}

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

## Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) till Google-målet.

## Förutsättningar

Om du vill skapa ditt första mål med [!DNL Google Ad Manager] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID-tjänsten tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL Google]-integreringar i Audience Manager överförs ID-synkroniseringarna du har konfigurerat till Platform.

## Tillåtelselista

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar ditt första [!DNL Google Ad Manager]-mål i Platform. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ad Manager]-målet i Platform måste du kontakta [!DNL Google] för att Adobe ska tas med i listan över tillåtna dataleverantörer och för att ditt konto ska läggas till i tillåtelselista. Kontakta [!DNL Google] och lämna följande information:

* **Konto-ID** : det här är Adobe konto ID med  [!DNL Google]. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Kund-ID** : det här är Adobe kundkonto-ID med  [!DNL Google]. Kontakta Adobe kundtjänst eller Adobe för att få detta ID.
* **Nätverks-ID** : det här är ditt konto med  [!DNL Google Ad Manager]
* **Audience Link ID** : det här är ditt konto med  [!DNL Google Ad Manager]
* Din kontotyp. DFP av Google eller AdX-köpare.

## Konfigurera mål

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du **[!DNL Google Ad Manager]** och väljer **[!UICONTROL Configure]**.

![Anslut Google Ad Manager-mål](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

I steget **Konfigurera** i arbetsflödet för att skapa mål fyller du i [!UICONTROL Basic Information] för målet.

![Grundläggande information Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `DFP by Google` för [!DNL DoubleClick] för utgivare
   * Använd `AdX buyer` för [!DNL Google AdX]
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med  [!DNL Google]. Detta kan vara ditt nätverks-ID eller ditt Audience Link-ID. Vanligtvis är detta ett åttasiffrigt ID.
* **[!UICONTROL Marketing action]**: Marknadsföringsåtgärder anger för vilken metod data ska exporteras till målet. Du kan välja bland Adobe-definierade marknadsföringsåtgärder eller skapa en egen marknadsföringsåtgärd. Mer information om marknadsföringsåtgärder finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>När du konfigurerar ett [!DNL Google Ad Manager]-mål ska du samarbeta med din [!DNL Google Account Manager]- eller Adobe-representant för att förstå vilken kontotyp du har.

## Aktivera segment till [!DNL Google Ad Manager]

Instruktioner om hur du aktiverar segment till [!DNL Google Ad Manager] finns i [Aktivera data till mål](../../ui/activate-destinations.md).

## Exporterade data

Kontrollera ditt [!DNL Google Ad Manager]-konto för att kontrollera om data har exporterats till [!DNL Google Ad Manager]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
