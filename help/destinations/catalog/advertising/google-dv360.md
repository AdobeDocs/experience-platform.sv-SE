---
title: Google Display & Video 360-anslutning
description: Display & Video 360, tidigare DoubleClick Bid Manager, är ett verktyg som används för att utföra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 2%

---

# [!DNL Google Display & Video 360]-anslutning

>[!IMPORTANT]
>
> Google släpper ändringar i [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [kundmatchning](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) och [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) för att stödja de kompatibilitetskrav och medgivanderelaterade krav som definieras i [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) i EU ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). Tvingande av dessa ändringar av medgivandekraven gäller från och med den 6 mars 2024.
><br/>
>För att kunna följa EU:s policy för användargodkännande och fortsätta att skapa målgruppslistor för användare i Europeiska ekonomiska samarbetsområdet (EES) måste annonsörer och partners se till att slutanvändarnas samtycke skickas när målgruppsdata överförs. Som Google-partner tillhandahåller Adobe verktygen som krävs för att uppfylla dessa krav på medgivande enligt DMA i Europeiska unionen.
><br/>
>Kunder som har köpt Adobe sekretess- och säkerhetssköld och har konfigurerat en [medgivandeprincip](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för att filtrera bort profiler som inte godkänts behöver inte vidta några åtgärder.
><br/>
>Kunder som inte har köpt Adobe sekretess- och säkerhetssköld måste använda [segmentdefinitionsfunktionerna](../../../segmentation/home.md#segment-definitions) i [Segment Builder](../../../segmentation/ui/segment-builder.md) för att filtrera bort profiler som inte godkänts, så att de kan fortsätta använda Real-Time CDP Google-destinationer utan avbrott.

[!DNL Display & Video 360], som tidigare kallades [!DNL DoubleClick Bid Manager], är ett verktyg som används för att köra återannonsering och målgruppsanpassade digitala kampanjer i olika källor för Display, Video och Mobile.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Display & Video 360] mål:

* Aktiverade målgrupper skapas programmatiskt i Google.
* Aktivering av målgruppsåsidosättningar till målet [!DNL Google Display & Video 360] är schemalagd till 24-48 timmar efter att en målgrupp först har mappats till en målanslutning. Den här uppdateringen svarar på Google policy att vänta i 24 timmar tills data har importerats och är avsedd att förbättra matchningsfrekvensen mellan Real-Time CDP och [!DNL Google Display & Video 360]. Det här är en serverdelskonfiguration som endast gäller för det här målet och som inte har något samband med några schemaläggningsalternativ som kan konfigureras av kunden i användargränssnittet.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med Google Display &amp; Video 360 och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=sv-SE) i Experience Cloud ID Service tidigare (med Adobe Audience Manager eller andra program) kan du kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Experience Platform.

## Identiteter som stöds {#supported-identities}

[!DNL Google Display & Video 360] stöder aktivering av målgrupper baserat på de identiteter som visas i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Identitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=sv-SE), även kallat [!DNL Device ID]. Ett numeriskt 38-siffrigt enhets-ID som Audience Manager associerar med varje enhet som det interagerar med. | Google använder [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=sv-SE) för målanvändare i Kalifornien och Google Cookie-ID för alla andra användare. |
| [!DNL Google] cookie-ID | [!DNL Google] cookie-ID | [!DNL Google] använder det här ID:t för användare utanför Kalifornien. |
| RIDA | Roku-ID för Advertising. Detta ID identifierar Roku-enheter unikt. |  |
| MAID | Microsoft Advertising ID. Detta ID identifierar unikt enheter som kör Windows 10. |  |
| Amazon Fire TV-ID | Detta ID identifierar Amazon Fire TV-program unikt. |  |

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp till Google-destinationen. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

## Förhandskrav {#prerequisites}

### Tillåt listning {#allow-listing}

>[!NOTE]
>
>Tillåt-listning är obligatoriskt innan du konfigurerar ditt första [!DNL Google Display & Video 360]-mål i Experience Platform. Kontrollera att processen för att tillåta listning som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.
>Undantaget till den här regeln gäller [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=sv-SE)-kunder. Om du redan har skapat en anslutning till det här Google-målet i Audience Manager behöver du inte gå igenom processen för att tillåta listning igen och du kan fortsätta till nästa steg.

Innan du skapar [!DNL Google Display & Video 360]-målet i Experience Platform måste du kontakta Google och be om att Adobe finns med i listan över tillåtna dataleverantörer och att ditt konto läggs till i tillåtelselista. Kontakta Google och lämna följande information:

* **Konto-ID**: Adobe konto-ID med Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID med Google. Kund-ID: 89690775.
* **Din kontotyp**: använd **[!DNL Invite advertiser]** för att tillåta att målgrupper delas endast till ett visst varumärke i ditt Display &amp; Video 360-konto eller använd **[!DNL Invite partner]** för att tillåta att målgrupper delas med alla varumärken i ditt Display &amp; Video 360-konto.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `Invite Advertiser` om du vill tillåta att målgrupper endast delas med ett visst varumärke i ditt Display &amp; Video 360-konto.
   * Använd `Invite Partner` om du vill tillåta att målgrupper delas med alla varumärken i ditt Display &amp; Video 360-konto.
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID för **[!DNL Invite partner]** eller **[!DNL Invite advertiser]** med Google. Vanligtvis är detta ett ID med sex eller sju siffror.

>[!NOTE]
>
>När du konfigurerar ett [!DNL Google Display & Video 360]-mål bör du samarbeta med din [!DNL Google Account Manager]- eller Adobe-representant för att ta reda på vilken kontotyp du har.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data

Kontrollera ditt [!DNL Google Display & Video 360]-konto om du vill verifiera om data har exporterats till målet [!DNL Google Display & Video 360]. Om aktiveringen lyckades fylls målgrupperna i ditt konto.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Det här felet inträffar när kundkonton inte uppfyller [kraven](#prerequisites). Kontakta Google och kontrollera att ditt konto är tillåtet för att åtgärda problemet.