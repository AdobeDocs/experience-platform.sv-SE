---
keywords: annonsering, microsoft ads; kundmatchning;
title: Microsoft Ads - anslutning för kundmatchning
description: Använd destinationen Microsoft Ads Customer Match för att matcha kunder med e-postadresser och återengagera dem i Microsoft Advertising Network, inklusive sök- och målgruppsannonser.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 6f246d87f44cd1fa9b22e40e9ee7b5d8250452e7
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---

# [!DNL Microsoft Ads Customer Match]-anslutning {#microsoft-ads-customer-match-destination}

>[!AVAILABILITY]
>
>Den här målkopplingen är för närvarande begränsad. Kontakta din Adobe-representant för att få åtkomst.</br>

## Översikt {#overview}

Använd målet [!DNL Microsoft Ads Customer Match] för att matcha kunder med e-postadress och återengagera dem i alla [!DNL Microsoft Advertising Network], inklusive sök- och målgruppsannonser. Länka ditt [!DNL Microsoft Advertising]-konto till Real-Time CDP för att automatisera skapandet och hanteringen av kundmatchningslistor direkt från Experience Platform.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Microsoft Ads Customer Match] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa med den här funktionen.

### Använd skiftläge 1

Ett e-handelsmärke vill nå befintliga kunder via [!DNL Microsoft Search] och [!DNL Microsoft Audience Network] för att anpassa erbjudanden baserat på deras tidigare köp och webbhistorik. Varumärket kan importera e-postadresser från sin egen CRM till Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till [!DNL Microsoft Ads Customer Match] för användning i sök- och målgruppsannonser, vilket optimerar deras annonsutgifter.

### Använd skiftläge 2

Ett teknikföretag lanserade en ny produkt. För att marknadsföra den nya produkten vill de öka medvetenheten bland kunder som tidigare köpt relaterade produkter. De överför e-postadresser från sin CRM-databas till Experience Platform med e-postadresserna som identifierare. Målgrupper skapas utifrån kunder som äger relaterade produkter. Dessa målgrupper skickas till [!DNL Microsoft Ads Customer Match], så att företaget kan inrikta sig på befintliga kunder och liknande kunder i hela [!DNL Microsoft Advertising Network].

## Identiteter som stöds {#supported-identities}

[!DNL Microsoft Ads Customer Match] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `email` | E-postadresser med oformaterad text | Endast e-postadresser med normal text stöds av anslutningen [!DNL Microsoft Ads Customer Match]. Experience Platform skickar automatiskt e-postadresser vid exporten så att de matchar Microsoft krav. |

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
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (e-postadresser) som används i målet [!DNL Microsoft Ads Customer Match]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

Om du vill skicka målgruppsdata till [!DNL Microsoft Ads] måste du ha ett aktivt [!DNL Microsoft Advertising]-konto. Mer information om hur du skapar ett konto finns i [Microsoft Advertising-dokumentationen](https://help.ads.microsoft.com/#apex/ads/en/53090/0).

### Godkänn villkor för kundmatchning {#accept-customer-match-terms}

Innan du aktiverar målgrupper via det här målet måste du skapa en kundmatchningslista manuellt i ditt [!DNL Microsoft Advertising]-konto. Denna första manuella skapelse krävs för att acceptera kundens matchningsvillkor, som gör att målgrupper som skickas från Experience Platform kan skapas automatiskt. Om du inte slutför det här steget kan det uppstå fel när målgrupper aktiveras.

### Kontokonfiguration {#account-configuration}

När du konfigurerar målet måste du ange följande information:

* [!UICONTROL Customer ID]: ditt [!DNL Microsoft Ads] kund-ID (CID) i heltalsformat. Se [Microsoft Advertising-dokumentationen](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) för mer information om hur du hittar ditt kund-ID.
* [!UICONTROL Customer Account ID]: ditt [!DNL Microsoft Ads] kundkonto-ID. Se [Microsoft Advertising-dokumentationen](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) för mer information om hur du hittar ditt konto-ID.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Fyll i målinformation {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_id"
>title="Kund-ID"
>abstract="Ditt Microsoft Advertising-kund-ID, även kallat hanterarkonto-ID. Detta är den identifierare på den översta nivån i Microsoft Advertising som kan ha flera annonserkonton (kundkonto-ID) under."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Hitta ditt kund-ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_account_id"
>title="Kundkonto-ID"
>abstract="Ditt Microsoft Advertising kundkonto-ID, även kallat Advertiser-konto-ID. Detta identifierar ett specifikt annonserarkonto under ditt Kund-ID."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Hitta ditt kundkonto-ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_membership_duration"
>title="Varaktighet för medlemskap"
>abstract="Antalet dagar som en användare finns kvar i kundmatchningslistan. Godkända värden är mellan 1 och 390 dagar."

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_list_availability"
>title="Tillgänglighet för kundmatchningslista"
>abstract="Välj om kundmatchningslistan är tillgänglig för ett enskilt annonserarkonto eller för alla konton under chefskontot. Välj Kund-ID för att göra listan tillgänglig för alla annonserarkonton under ditt Kund-ID. Välj Kundkonto-ID om du vill begränsa listan till det specifika kundkonto-ID:t."
>additional-url="https://help.ads.microsoft.com/apex/index/3/en/56727" text="Läs mer om delning av målgruppslistor i Microsoft Advertising"

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Customer ID]**: Ditt [!DNL Microsoft Ads] kund-ID (CID). Se [Microsoft Advertising-dokumentationen](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) för mer information om hur du hittar ditt kund-ID.
* **[!UICONTROL Customer Account ID]**: Ditt [!DNL Microsoft Ads] kundkonto-ID. Se [Microsoft Advertising-dokumentationen](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) för mer information om hur du hittar ditt konto-ID.
* **[!UICONTROL Membership Duration]**: Antalet dagar som en användare finns kvar i kundmatchningslistan. Godkända värden är mellan 1 och 390 dagar.
* **[!UICONTROL Customer Match List Availability]**: Välj tillgängligheten för kundmatchningslistan. I [!DNL Microsoft Advertising] kan ett kund-ID ha flera kundkonto-ID:n (annonserkonton) under det. Välj **[!UICONTROL Customer ID (all advertising accounts)]** om du vill göra listan tillgänglig för alla annonserarkonton under ditt kund-ID, eller **[!UICONTROL Customer Account ID (single advertising account)]** om du vill begränsa listan till det specifika kundkonto-ID som du angav ovan. Mer information finns i [Microsoft Advertising-dokumentationen](https://help.ads.microsoft.com/apex/index/3/en/56727).

![Plattformsgränssnittsbild som visar målinformationsfälten för Microsoft Ads kundmatchningsmål.](../../assets/catalog/advertising/microsoft-ads-customer-match/destination-details.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* till mål måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappning {#mapping}

I steget **[!UICONTROL Mapping]** måste du mappa e-postidentiteten från källprofilerna till målidentiteten i [!DNL Microsoft Ads Customer Match].

* **Source-fält**: Välj `IdentityMap: Email` som källfält för att mappa e-postidentiteter från dina profiler. Du kan också välja ett XDM-attribut som `personalEmail.address` som källfält.
* **Målfält**: Välj `Identity: email` som målfält.

>[!IMPORTANT]
>
>Du måste använda källfält utan hash-kodade (oformaterad text). Använd inte förhash-kodade källidentifierare som `Emails (SHA256, lowercased)`. Experience Platform skickar automatiskt e-postadresserna vid exporten så att de matchar Microsoft krav.

![Gränssnittsbild som visar mappningssteget med e-post för identitetskarta mappad till e-post för identitet.](../../assets/catalog/advertising/microsoft-ads-customer-match/mapping.png)

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Microsoft Ads Customer Match]-konto om du vill verifiera om data har exporterats till målet [!DNL Microsoft Advertising]. Om aktiveringen lyckades fylls målgrupperna i ditt konto som kundmatchningslistor.

## Ytterligare resurser {#additional-resources}

Mer information finns i [Microsoft Advertising Help Center](https://help.ads.microsoft.com/).
