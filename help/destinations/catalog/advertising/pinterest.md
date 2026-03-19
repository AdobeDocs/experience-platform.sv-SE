---
title: Pinterest Customer List Connection
description: Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 3%

---

# [!DNL Pinterest Customer List]-anslutning

## Översikt {#overview}

Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.

>[!IMPORTANT]
>
>Det här målet har byggts av Pinterest team. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på https://help.pinterest.com/en/contact.

## Förutsättningar {#prerequisites}

* Användaren måste autentisera med ett Pinterest-konto som har åtkomst till annonskontot som han/hon vill lägga till en målgrupp i. Information om delning av annonseringskonton finns [här](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Användaren skulle behöva åtkomstnivåerna &quot;målgrupp&quot;.
* Information om identitetsformat för kundlista finns [här](https://help.pinterest.com/en/business/article/audience-targeting).

## Identiteter som stöds {#supported-identities}

Målet [!DNL Pinterest Customer List] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=sv-SE#getting-started).

I [mappningssteget](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) i arbetsflödet för målaktivering mappar du önskade identiteter till målfältet *pinterest_audition*. Identiteter särskiljs och löses vid datainhämtning till Pinterest.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mappa *GAID*-källidentitetens namnområde till målidentitetsfältet *pinterest_audience*. |
| IDFA | [!DNL Apple ID for Advertisers] | Mappa *IDFA*-källidentitetens namnområde till målidentitetsfältet *pinterest_audience*. |
| E-POST | E-postadresser (klartext eller hashas med SHA256-algoritmen) | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. <br> Mappa *Email* eller *Email_LC_SHA256*-källidentitetsnamnområdet till målidentitetsfältet *pinterest_audience*. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Nej | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som genererats i andra Experience Platform-appar som Adobe Journey Optimizer, </li><li> med mera. </li></ul> |

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
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i Pinterest kundlista. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Pinterest Customer List] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Användningsfall 1 {#use-case-1}

Skapa målgrupper utifrån kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest.

## Anslut till mål {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Ad Account ID]**: Ditt Pinterest-annonser-ID.

### Uppdatera autentiseringsuppgifter {#refresh-authentication-credentials}

Pinterest-token upphör att gälla var 30:e dag. Du kan övervaka förfallotiden för dina tokens från kolumnen **[!UICONTROL Account expiration date]** på flikarna **[[!UICONTROL Accounts]](../../ui/destinations-workspace.md#accounts)** eller **[[!UICONTROL Browse]](../../ui/destinations-workspace.md#browse)**.

När token har gått ut slutar dataexporten till målet att fungera. Du kan förhindra detta genom att utföra följande steg:

1. Navigera till **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**
2. (Valfritt) Använd de tillgängliga filtren på sidan om du bara vill visa Pinterest-konton.
   ![Filtrera så att endast Pinterest-konton visas](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-filters.png)
3. Markera det konto som du vill uppdatera, markera ellipsen och välj **[!UICONTROL Edit details]**.
   ![Välj kontrollen Redigera information](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-edit-details.png)
4. I det modala fönstret väljer du **[!UICONTROL Reconnect OAuth]** och autentiserar igen med dina Pinterest-autentiseringsuppgifter.
   ![Modalt fönster med alternativet Återanslut OAuth](/help/destinations/assets/catalog/advertising/pinterest-customer-list/reconnect-oauth-control.png)

>[!SUCCESS]
>
>Dina autentiseringsuppgifter uppdateras och deras förfallotid återställs till 30 dagar.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=sv-SE).

## Ytterligare resurser {#additional-resources}

Mer information finns på sidan [Pinterest Help Center](https://help.pinterest.com/en/business/article/audience-targeting).

+++ Visa ändringslogg


| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| November 2023 | Funktioner och dokumentation | Pinterest-målet i Real-Time CDP använder nu API:t för v5-annonsering. |

{style="table-layout:auto"}


+++
