---
keywords: Google ad manager;google ad;doubleClick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Google Ad Manager-anslutning
description: Google Ad Manager, tidigare DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivaren möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 5174c65970aa8df9bc3f2c8d612c26c72c20e81f
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 1%

---

# [!DNL Google Ad Manager] anslutning

## Översikt {#overview}

[!DNL Google Ad Manager], tidigare känt som [!DNL DoubleClick for Publishers] (DFP) eller [!DNL DoubleClick AdX], är en annonseringsplattform från [!DNL Google] som ger utgivaren möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Ad Manager] mål:

* Aktiverade målgrupper skapas programmatiskt i [!DNL Google] plattform.
* [!DNL Platform] innehåller för närvarande inga mätvärden som validerar den lyckade aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.
* Efter mappning av ett segment till ett [!DNL Google Ad Manager] mål visas segmentnamnet omedelbart i [!DNL Google Ad Manager] användargränssnitt.
* Segmentpopulationen behöver 24-48 timmar att vara [!DNL Google Ad Manager]. Dessutom måste segment ha en målgruppsstorlek på minst 50 profiler för att kunna visas i [!DNL Google Ad Manager]. Segment som är mindre än 50 profiler fylls inte i i [!DNL Google Ad Manager].

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

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) till Google-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

Om du vill skapa ditt första mål med [!DNL Google Ad Manager] och har inte aktiverat [Synkroniseringsfunktion för ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) tidigare i Experience Cloud ID-tjänsten (med Audience Manager eller andra program), kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du redan har konfigurerat [!DNL Google] integreringar i Audience Manager, de ID-synkroniseringar du har konfigurerat överförs till Platform.

### Tillåt listning {#allow-listing}

Du måste ange Tillåt innan du konfigurerar din första [!DNL Google Ad Manager] mål i Platform. Se till att du slutför processen för att tillåta listning som beskrivs nedan innan du skapar ditt mål.

1. Följ stegen som beskrivs i [Dokumentation för Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) att lägga till Adobe som en länkad datahanteringsplattform (DMP).
2. I [!DNL Google Ad Manager] gränssnitt, gå till **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** och aktivera **[!UICONTROL API Access]** skjutreglage.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Lägg till segment-ID till segmentnamn"
>abstract="Välj det här alternativet om du vill att segmentnamnet i Google Ad Manager ska innehålla segment-ID:t från Experience Platform: `Segment Name (Segment ID)`"

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account ID]**: Ange [!DNL Audience Link ID] från [!DNL Google] konto. Detta är en specifik identifierare som är associerad med din [!DNL Google Ad Manager] nätverk (inte ditt [!DNL Network code]). Du hittar den här under **[!UICONTROL Admin > Global settings]** i [!DNL Google Ad Manager] gränssnitt.
* **[!UICONTROL Account Type]**: Välj ett alternativ beroende på ditt konto hos Google:
   * Använd `DFP by Google` for [!DNL DoubleClick] för utgivare
   * Använd `AdX buyer` for [!DNL Google AdX]
* **[!UICONTROL Append segment ID to segment name]**: Välj det här alternativet om du vill att segmentnamnet i Google Ad Manager ska innehålla segment-ID:t från Experience Platform: `Segment Name (Segment ID)`.

>[!NOTE]
>
>När du konfigurerar en [!DNL Google Ad Manager] mål, arbeta med [!DNL Google Account Manager] eller Adobe för att förstå vilken kontotyp du har.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

Verifiera om data har exporterats till [!DNL Google Ad Manager] mål, kontrollera [!DNL Google Ad Manager] konto. Om aktiveringen lyckades fylls målgrupperna i ditt konto.

## Felsökning {#troubleshooting}

Om du råkar ut för några fel när du använder det här målet och behöver kontakta antingen Adobe eller Google, ska du ha följande ID:n till hands.

Följande är Adobe Google konto-ID:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775