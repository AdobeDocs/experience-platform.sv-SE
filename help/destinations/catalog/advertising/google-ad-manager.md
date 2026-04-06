---
keywords: Google ad manager;google ad;dubbelklickning;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager;DFP
title: Google Ad Manager-anslutning
description: Google Ad Manager, tidigare DoubleClick for Publishers eller DoubleClick AdX, är en annonseringsplattform från Google som ger utgivaren möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 3%

---

# [!DNL Google Ad Manager]-anslutning

>[!IMPORTANT]
>
> Google släpper ändringar i [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Kundmatchning](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) och [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) som stöder de kompatibilitetsrelaterade och medgivanderelaterade krav som definieras i [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) i EU ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). Tvingande av dessa ändringar av medgivandekraven gäller från och med den 6 mars 2024.
><br/>
>För att kunna följa EU:s policy för användargodkännande och fortsätta att skapa målgruppslistor för användare i Europeiska ekonomiska samarbetsområdet (EES) måste annonsörer och partners se till att slutanvändarnas samtycke skickas när målgruppsdata överförs. Som Google-partner tillhandahåller Adobe verktygen som krävs för att uppfylla dessa krav på medgivande enligt DMA i Europeiska unionen.
><br/>
>Kunder som har köpt Adobe sekretess- och säkerhetssköld och har konfigurerat en [medgivandeprincip](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för att filtrera bort profiler som inte godkänts behöver inte vidta några åtgärder.
><br/>
>Kunder som inte har köpt Adobe sekretess- och säkerhetssköld måste använda [segmentdefinitionsfunktionerna](../../../segmentation/home.md#segment-definitions) i [Segment Builder](../../../segmentation/ui/segment-builder.md) för att filtrera bort profiler som inte godkänts, för att fortsätta använda de befintliga [!DNL Real-Time CDP] Google-målsättningarna utan avbrott.


[!DNL Google Ad Manager], som tidigare kallades [!DNL DoubleClick for Publishers] (DFP) eller [!DNL DoubleClick AdX], är en annonseringsplattform från [!DNL Google] som ger utgivare möjlighet att hantera visningen av annonser på sina webbplatser, via video och i mobilappar.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Ad Manager] mål:

* Aktiverade målgrupper skapas programmatiskt i plattformen [!DNL Google].
* [!DNL Experience Platform] innehåller för närvarande inte något mätvärde för att validera aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.
* När en målgrupp har mappats till ett [!DNL Google Ad Manager]-mål visas målgruppsnamnet omedelbart i användargränssnittet i [!DNL Google Ad Manager].
* Segmentpopulationen behöver 24-48 timmar för att visas i [!DNL Google Ad Manager]. Dessutom måste målgrupperna ha en målgruppsstorlek på minst 50 profiler för att kunna visas i [!DNL Google Ad Manager]. Publiker som är mindre än 50 profiler fylls inte i i [!DNL Google Ad Manager].

## Identiteter som stöds {#supported-identities}

[!DNL Google Ad Manager] stöder aktivering av målgrupper baserat på de identiteter som visas i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Identitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), även kallat [!DNL Device ID]. Ett numeriskt 38-siffrigt enhets-ID som Audience Manager associerar med varje enhet som det interagerar med. | Google använder [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) för målanvändare i Kalifornien och Google Cookie-ID för alla andra användare. |
| [!DNL Google] cookie-ID | [!DNL Google] cookie-ID | [!DNL Google] använder det här ID:t för användare utanför Kalifornien. |
| RIDA | Roku-ID för Advertising. Detta ID identifierar Roku-enheter unikt. |  |
| MAID | Microsoft Advertising ID. Detta ID identifierar unikt enheter som kör Windows 10. |  |
| Amazon Fire TV-ID | Detta ID identifierar Amazon Fire TV-program unikt. |  |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Ja | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som har genererats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer], </li><li> med mera. </li></ul> |

{style="table-layout:auto"}



Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data lagrade i datasjön [!DNL Adobe Experience Platform]. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp till Google-destinationen. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

Om du vill skapa ditt första mål med [!DNL Google Ad Manager] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID Service tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller Kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL Google]-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Experience Platform.

### Tillåt listning {#allow-listing}

Tillåt-listning är obligatoriskt innan du konfigurerar ditt första [!DNL Google Ad Manager]-mål i Experience Platform. Se till att du slutför processen för att tillåta listning som beskrivs nedan innan du skapar ditt mål.

1. Följ stegen som beskrivs i [Google Ad Manager-dokumentationen](https://support.google.com/admanager/answer/3289669?hl=en) för att lägga till Adobe som en länkad datahanteringsplattform (DMP).
2. I gränssnittet [!DNL Google Ad Manager] går du till **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** och aktiverar skjutreglaget **[!UICONTROL API Access]**.

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Bifoga målgrupps-ID till målgruppsnamn"
>abstract="Välj det här alternativet om målgruppsnamnet i Google Ad Manager ska innehålla målgrupps-ID:t från Experience Platform, så här: `Audience Name (Audience ID)`"

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account ID]**: Ange [!DNL Audience Link ID] från ditt [!DNL Google]-konto. Detta är en specifik identifierare som är associerad med ditt [!DNL Google Ad Manager]-nätverk (inte din [!DNL Network code]). Du hittar detta under **[!UICONTROL Admin > Global settings]** i gränssnittet [!DNL Google Ad Manager].
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på ditt konto hos Google:
   * Använd `DFP by Google` för [!DNL DoubleClick] för utgivare
   * Använd `AdX buyer` för [!DNL Google AdX]
* **[!UICONTROL Append audience ID to audience name]**: Välj det här alternativet om du vill att målgruppsnamnet i Google Ad Manager ska innehålla målgrupps-ID:t från Experience Platform, enligt följande: `Audience Name (Audience ID)`.

>[!NOTE]
>
>När du konfigurerar ett [!DNL Google Ad Manager]-mål bör du samarbeta med din [!DNL Google Account Manager]- eller Adobe-representant för att ta reda på vilken kontotyp du har.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Google Ad Manager]-konto om du vill verifiera om data har exporterats till målet [!DNL Google Ad Manager]. Om aktiveringen lyckades fylls målgrupperna i ditt konto.

## Felsökning {#troubleshooting}

Om du råkar ut för några fel när du använder det här målet och behöver kontakta Adobe eller Google, ska du ha följande ID:n till hands.

Detta är Adobe Google konto-ID:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775