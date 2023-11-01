---
keywords: Dubbelklicka på Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Google Display & Video 360-anslutning
description: Display & Video 360, tidigare DoubleClick Bid Manager, är ett verktyg som används för att utföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 1%

---

# [!DNL Google Display & Video 360] anslutning

## Översikt {#overview}

[!DNL Display & Video 360], tidigare känt som [!DNL DoubleClick Bid Manager], är ett verktyg som används för att skapa återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile.

## Destinationsspecifikationer {#specifics}

Observera följande information som gäller [!DNL Google Display & Video 360] mål:

* Aktiverade målgrupper skapas programmatiskt i Google.
* aktivering av eftersläpning av målgrupper till [!DNL Google Display & Video 360] målet beräknas inträffa 24-48 timmar efter att en målgrupp först har mappats till en målanslutning. Uppdateringen är ett svar på Google policy att vänta i 24 timmar tills data har importerats och är avsedd att förbättra matchningsfrekvensen mellan Real-Time CDP och [!DNL Google Display & Video 360]. Observera att detta är en backend-konfiguration som endast gäller för det här målet och som inte har något samband med några schemaläggningsalternativ som kan konfigureras av kunden i användargränssnittet.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Display &amp; Video 360 och inte har aktiverat [Synkroniseringsfunktion för ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) tidigare i Experience Cloud ID-tjänsten (med Adobe Audience Manager eller andra program), kontakta Adobe Consulting eller Kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager, överförs de ID-synkroniseringar du har konfigurerat till Platform.

## Identiteter som stöds {#supported-identities}

[!DNL Google Display & Video 360] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | [!DNL Apple ID for Advertisers] | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), även känt som [!DNL Device ID]. Ett numeriskt 38-siffrigt enhets-ID som Audience Manager associerar med varje enhet som det interagerar med. | Google använder [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) för användare i Kalifornien och Google Cookie ID för alla andra användare. |
| [!DNL Google] cookie-ID | [!DNL Google] cookie-ID | [!DNL Google] använder detta ID för att rikta sig till användare utanför Kalifornien. |
| RIDA | Roku-ID för annonsering. Detta ID identifierar Roku-enheter unikt. |  |
| MAID | Microsoft Advertising ID. Detta ID identifierar unikt enheter som kör Windows 10. |  |
| Amazon Fire TV-ID | Detta ID identifierar Amazon Fire TV-program unikt. |  |

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp till Google-destinationen. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

## Förutsättningar {#prerequisites}

### Tillåt listning {#allow-listing}

>[!NOTE]
>
>Du måste ange Tillåt innan du konfigurerar din första [!DNL Google Display & Video 360] mål i Platform. Se till att processen för att tillåta listning som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.
>Undantaget till den här regeln är för [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) kunder. Om du redan har skapat en anslutning till det här Google-målet i Audience Manager behöver du inte gå igenom processen för att tillåta listning igen och du kan fortsätta till nästa steg.

Innan du skapar [!DNL Google Display & Video 360] mål i Platform måste du kontakta Google för att få Adobe att finnas med i listan över tillåtna dataleverantörer och för att ditt konto ska läggas till i tillåtelselista. Kontakta Google och lämna följande information:

* **Konto-ID**: Adobe konto-ID med Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID med Google. Kund-ID: 89690775.
* **Din kontotyp**: use **[!DNL Invite advertiser]** för att tillåta att målgrupper delas endast till ett visst varumärke i ditt Display &amp; Video 360-konto eller använder **[!DNL Invite partner]** så att målgrupper kan delas med alla varumärken i ert Display &amp; Video 360-konto.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `Invite Advertiser` för att tillåta att målgrupper delas endast till ett visst varumärke i ert Display &amp; Video 360-konto.
   * Använd `Invite Partner` så att målgrupper kan delas med alla varumärken i ert Display &amp; Video 360-konto.
* **[!UICONTROL Account ID]**: Fyll i **[!DNL Invite partner]** eller **[!DNL Invite advertiser]** konto-ID med Google. Vanligtvis är detta ett ID med sex eller sju siffror.

>[!NOTE]
>
>När du konfigurerar en [!DNL Google Display & Video 360] mål, arbeta med [!DNL Google Account Manager] eller Adobe för att förstå vilken kontotyp du har.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för direktuppspelad målgruppsexport](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data

Verifiera om data har exporterats till [!DNL Google Display & Video 360] mål, kontrollera [!DNL Google Display & Video 360] konto. Om aktiveringen lyckades fylls målgrupperna i ditt konto.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kundkonton inte uppfyller [krav](#prerequisites). Kontakta Google och kontrollera att ditt konto är tillåtet för att åtgärda problemet.