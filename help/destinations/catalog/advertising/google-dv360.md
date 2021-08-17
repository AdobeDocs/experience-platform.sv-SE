---
keywords: Dubbelklicka på Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Google Display & Video 360-anslutning
description: Display & Video 360, tidigare DoubleClick Bid Manager, är ett verktyg som används för att utföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 1%

---

# [!DNL Google Display & Video 360] anslutning

## Översikt {#overview}

[!DNL Display & Video 360], tidigare kallat  [!DNL DoubleClick Bid Manager], är ett verktyg som används för att genomföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display-, Video- och Mobile-material.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Display & Video 360]-mål:

* Aktiverade målgrupper skapas programmatiskt i Google-plattformen.
* [!DNL Platform] innehåller för närvarande inga mätvärden som validerar den lyckade aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Display &amp; Video 360 och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Platform.

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

### Tillåtelselista

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar ditt första [!DNL Google Display & Video 360]-mål i Platform. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts av Google innan du skapar ett mål.

Innan du skapar målet [!DNL Google Display & Video 360] i Platform måste du kontakta Google och be om att Adobe finns med i listan över tillåtna dataleverantörer och att ditt konto läggs till i tillåtelselista. Kontakta Google och lämna följande information:

* **Konto-ID**: Adobe konto-ID med Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID med Google. Kund-ID: 89690775.
* **Kontotyp**: kan användas  **[!DNL Invite advertiser]** för att tillåta att målgrupper delas endast till ett visst varumärke i ditt Display &amp; Video 360-konto eller  **[!DNL Invite partner]** för att tillåta att målgrupper delas med alla varumärken i ditt Display &amp; Video 360-konto.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `Invite Advertiser` för att tillåta att målgrupper delas endast till ett visst varumärke i ditt Display &amp; Video 360-konto.
   * Använd `Invite Partner` för att tillåta att målgrupper delas med alla varumärken i ditt Display &amp; Video 360-konto.
* **[!UICONTROL Account ID]**: Fyll i ditt  **[!DNL Invite partner]** eller ditt  **[!DNL Invite advertiser]** konto-ID med Google. Vanligtvis är detta ett ID med sex eller sju siffror.

>[!NOTE]
>
>När du konfigurerar ett [!DNL Google Display & Video 360]-mål ska du samarbeta med din [!DNL Google Account Manager]- eller Adobe-representant för att förstå vilken kontotyp du har.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till den här destinationen.

## Exporterade data

Kontrollera ditt [!DNL Google Display & Video 360]-konto för att kontrollera om data har exporterats till [!DNL Google Display & Video 360]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
