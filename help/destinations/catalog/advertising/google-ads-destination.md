---
title: Google Ads-anslutning
description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör det möjligt för företag att betala per klick för annonsering i textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appen.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# [!DNL Google Ads]-anslutning

## Översikt {#overview}

[!DNL Google Ads], som tidigare kallades [!DNL Google AdWords], är en onlinereklam som gör att företag kan betala annonser per klick för textbaserade sökningar, bildskärmar, [!DNL YouTube] videor och mobilskärmar i appen.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Ads] mål:

* Aktiverade målgrupper skapas programmatiskt i plattformen [!DNL Google].
* [!DNL Experience Platform] innehåller för närvarande inte något mätvärde för att validera aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Google Ads] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID-tjänsten tidigare (med Audience Manager eller andra program) kan du kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Experience Platform.

## Identiteter som stöds {#supported-identities}

[!DNL Google Ads] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | [!DNL Apple ID for Advertisers] | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
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
| Alla andra målgrupper kommer | Ja | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som genererats i andra Experience Platform-appar som Adobe Journey Optimizer, </li><li> med mera. </li></ul> |

{style="table-layout:auto"}



Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data som lagras i Adobe Experience Platform Data Lake. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp till Google-destinationen. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

### Befintligt [!DNL Google Ads]-konto {#existing-google-ads-account}

>[!IMPORTANT]
>
> [!DNL Google] har ersatt nya [!DNL Google Ads] cookie-integreringar med tredjepartsleverantörer. Om du vill utföra tillåtelselista-stegen i nästa avsnitt måste du ha en befintlig integrering med [!DNL Google Ads]. Därför rekommenderar vi att du använder [!DNL Google Ads] för att konfigurera en [!DNL Google Customer Match]-integrering. Mer information om hur du skapar en [!DNL Google Customer Match]-integrering finns i självstudiekursen om hur du skapar en [[!DNL Google Customer Match]](./google-customer-match.md)-anslutning.

### Tillåt listning {#allow-listing}

>[!NOTE]
>
>Tillåt-listning är obligatoriskt innan du konfigurerar ditt första [!DNL Google Ads]-mål i Experience Platform. Kontrollera att processen för att tillåta listning som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.
>Undantaget till den här regeln gäller [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html)-kunder. Om du redan har skapat en anslutning till det här Google-målet i Audience Manager behöver du inte gå igenom processen för att tillåta listning igen och du kan fortsätta till nästa steg.

Innan du skapar [!DNL Google Ads]-målet i Experience Platform måste du kontakta [!DNL Google] för att Adobe ska tas med i listan över tillåtna dataleverantörer och för att ditt konto ska läggas till i tillåtelselista. Kontakta [!DNL Google] och ange följande information:

* **Konto-ID**: Adobe konto-ID med Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID med Google. Kund-ID: 89690775.
* Din kontotyp: **AdWords**
* **Google AdWords ID**: Detta är ditt ID med [!DNL Google]. ID-formatet är vanligtvis 123-456-7890.

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: AdWords är det enda tillgängliga alternativet.
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med [!DNL Google Ads]. ID-formatet är vanligtvis 123-456-7890.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Google Ads]-konto om du vill verifiera om data har exporterats till målet [!DNL Google Ads]. Om aktiveringen lyckades fylls målgrupperna i ditt konto.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Det här felet inträffar antingen när kundkonton inte uppfyller [villkoren](#prerequisites) eller när kunder försöker konfigurera målet utan ett befintligt [!DNL Google Ads]-konto.

[!DNL Google] har ersatt nya [!DNL Google Ads] cookie-integreringar med tredjepartsleverantörer. Om du vill utföra [tillåtelselista](#allow-listing)-stegen måste du ha en befintlig integrering med [!DNL Google Ads].

Det rekommenderade sättet att använda [!DNL Google Ads] är att konfigurera en [[!DNL Google Customer Match]](google-customer-match.md)-integrering.
