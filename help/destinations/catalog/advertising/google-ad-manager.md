---
keywords: Google ad manager;google ad;doubleClick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Google Ad Manager-anslutning
description: Google Ad Manager, tidigare DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivaren möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# [!DNL Google Ad Manager] anslutning

## Översikt {#overview}

[!DNL Google Ad Manager], tidigare känt som [!DNL DoubleClick for Publishers] (DFP) eller [!DNL DoubleClick AdX], är en annonseringsplattform från [!DNL Google] som ger utgivaren möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Ad Manager] mål:

* Aktiverade målgrupper skapas programmatiskt i [!DNL Google] plattform.
* [!DNL Platform] innehåller för närvarande inga mätvärden som validerar den lyckade aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

## Identiteter som stöds {#supported-identities}

[!DNL Google Ad Manager] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | [!DNL Apple ID for Advertisers] | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), även känt som [!DNL Device ID]. Ett numeriskt 38-siffrigt enhets-ID som Audience Manager associerar med varje enhet som det interagerar med. | Google använder [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) för användare i Kalifornien och Google Cookie ID för alla andra användare. |
| [!DNL Google] cookie-ID | [!DNL Google] cookie-ID | [!DNL Google] använder detta ID för att rikta sig till användare utanför Kalifornien. |
| RIDA | Roku-ID för annonsering. Detta ID identifierar Roku-enheter unikt. |  |
| MAID | Microsoft Advertising ID. Detta ID identifierar unikt enheter som kör Windows 10. |  |
| Amazon Fire TV-ID | Detta ID identifierar Amazon Fire TV-program unikt. |  |

## Exporttyp {#export-type}

**Segmentexport** - du exporterar alla medlemmar i ett segment (publik) till Google-destinationen.

## Förutsättningar

Om du vill skapa ditt första mål med [!DNL Google Ad Manager] och har inte aktiverat [Synkroniseringsfunktion för ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) tidigare i Experience Cloud ID-tjänsten (med Audience Manager eller andra program), kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du redan har konfigurerat [!DNL Google] integreringar i Audience Manager, de ID-synkroniseringar du har konfigurerat överförs till Platform.

## Tillåtelselista

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar din första [!DNL Google Ad Manager] mål i Platform. Se till att tillåtelselista-processen som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ad Manager] mål i plattform måste du kontakta [!DNL Google] för att Adobe ska föras upp på listan över tillåtna dataleverantörer och för att ditt konto ska läggas till tillåtelselista. Kontakt [!DNL Google] och lämna följande information:

* **Konto-ID**: Adobe konto-ID hos Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID hos Google. Kund-ID: 89690775.
* **Nätverks-ID**: det här är ditt konto med [!DNL Google Ad Manager]
* **Målgruppslänks-ID**: det här är ditt konto med [!DNL Google Ad Manager]
* Din kontotyp. DFP av Google eller AdX-köpare.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ beroende på ditt konto hos Google:
   * Använd `DFP by Google` for [!DNL DoubleClick] för utgivare
   * Använd `AdX buyer` for [!DNL Google AdX]
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med [!DNL Google]. Detta kan vara ditt nätverks-ID eller ditt Audience Link-ID. Vanligtvis är detta ett åttasiffrigt ID.

>[!NOTE]
>
>När du konfigurerar en [!DNL Google Ad Manager] mål, arbeta med [!DNL Google Account Manager] eller Adobe för att förstå vilken kontotyp du har.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data

Verifiera om data har exporterats till [!DNL Google Ad Manager] mål, kontrollera [!DNL Google Ad Manager] konto. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
