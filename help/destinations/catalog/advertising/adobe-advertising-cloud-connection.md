---
title: Adobe Advertising DSP
description: Lär dig hur du delar autentiserade och oautentiserade förstahandsmålgrupper med Adobe Advertising Demand-Side Platform (DSP) med hjälp av flera identitetstyper.
feature: Destinations
exl-id: 0ff80d38-993f-4609-bf2a-01a3e6cfe10b
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 0%

---

# Adobe Advertising DSP

## Översikt {#overview}

Adobe Advertising Demand-Side Platform-målet (DSP) gör det möjligt för användare att dela både autentiserade och oautentiserade förstapartsmålgrupper med ett DSP-konto eller en viss annonsörer inom ett konto.

Med den här destinationen kan kunder dela förstapartsmålgrupper med något eller alla av dessa ID:n:

* Hash-kodat e-post-ID, som konverteras till [!DNL LiveRamp RampID] eller [!DNL Unified ID 2.0] (UID2.0) för målinriktning i DSP

* Experience Cloud ID (ECID) och Adobe Advertising cookies från tredje part

* ID för mobilannonsering (MAID):

   * [!DNL Google] Advertising ID (GAID) för [!DNL Android] enheter

   * Identifierare för annonsörer (IDFA) för [!DNL Apple iOS] enheter

Den här anslutningen ersätter den [gamla Adobe Advertising Cloud DSP-anslutningen](adobe-advertising-cloud-connection-legacy.md), som bara stöder hash-kodade e-postadresser.

>[!IMPORTANT]
>
>Den här sidan har skapats av Adobe Advertising [!DNL DSP]-teamet. Kontakta Advertising support direkt på `adcloud_support@adobe.com` om du har frågor eller uppdateringsfrågor.

## Användningsfall {#use-cases}

Med den här destinationen kan annonsörer nå sin publik i olika webbläsare med hjälp av cookies och utan cookies.

Annonsörer kan dela segment antingen med autentiserade förstapartidentifierare (som [!DNL RampID] och [!DNL UID2.0]) eller som oautentiserade ID:n (som cookies och MAID:n).

## Förutsättningar {#prerequisites}

* För [!DNL RampID activation], [!DNL DSP] kontonivå- och kampanjnivåinställningar för att aktivera målgruppsdelning med [!DNL LiveRamp RampID], som översätter kunddata till [!DNL RampIDs] för att skapa målgruppssegment. Ditt Adobe-kontoteam kommer att utföra den här konfigurationen. [!DNL RampID] är tillgängligt via ett partnerskap mellan [!DNL DSP] och [!DNL LiveRamp], och du behöver inte ett eget [!DNL LiveRamp]-medlemskap för att använda det.

* Målgrupps-ID:

   * För [!DNL RampID] och [!DNL UID2.0] måste profilerna innehålla hash-kodade e-post-ID:n.

   * För cookies skapar du en cookie-synkroniseringsprocess med antingen [!DNL Web SDK] datastreams eller [!DNL Experience Cloud ID Service]. Se [Konfigurera ID-synkronisering för att dela cookies](#cookie-sync) nedan.

   * För profiler med MAID:

      * Inkludera värdet `GAID` i en IdentityMap-kolumn för varje GAID.

      * Inkludera värdet `IDFA` i en IdentityMap-kolumn för varje IDFA.

* Experience Cloud organisations-ID för Experience Platform-kontot. Du kan hitta ditt ID på din profilsida för Adobe [!DNL Real-Time Customer Data Platform] ([!DNL Real-Time CDP]).

* En [[!DNL Real-Time CDP] källa i DSP](https://experienceleague.adobe.com/sv/docs/advertising/dsp/audiences/sources/source-manage) som tar emot målgrupper för kampanjaktivering. Ditt Adobe-kontoteam skapar källan med ditt Experience Cloud organisations-ID.

* Källnyckeln för kontot eller annonsören [!DNL DSP], som genereras när en [[!DNL Real-Time CDP] källa skapas i  [!DNL DSP]](https://experienceleague.adobe.com/sv/docs/advertising/dsp/audiences/sources/source-manage). Kontoteamet på [!DNL DSP] delar nyckeln med dig. Du kommer att använda den i Experience Platform för att skapa en målanslutning till Advertising DSP-målet, vilket förklaras nedan.

### Konfigurera ID-synkronisering för delning av cookies {#cookie-sync}

Synkronisering av ID är en förutsättning för delning av cookies från tredje part. Konfigurera en cookie-synkroniseringsprocess med antingen [!DNL Web SDK] datastreams eller [!DNL Experience Cloud ID Service]. Mer information om identitetshantering för cookies från tredje part finns i [Advertising-mål som förlitar sig på cookie-integreringar från tredje part](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations).

**Aktivera synkronisering av tredjeparts-ID med[!DNL Web SDK]**

Om du använder [!DNL Experience Platform Web SDK] aktiverar du synkronisering av tredjeparts-ID på ditt datastream genom att konfigurera alternativet [!UICONTROL Third Party ID Sync] i de avancerade inställningarna. Instruktioner finns i [Konfigurera avancerade alternativ](/help/datastreams/configure.md#advanced-options) i datastreams-dokumentationen.

**Aktivera synkronisering av tredjeparts-ID med[!DNL Experience Cloud ID Service]**

Om du använder [!DNL Experience Platform]-taggar med [!DNL Experience Cloud ID Service] konfigurerar du synkroniseringen av tredjeparts-ID med [Experience Cloud ID-tjänsttillägget](/help/tags/extensions/client/id-service/overview.md). Detta gör att den matchande Adobe Advertising-cookien för angivet ECID är tillgänglig när du aktiverar målgruppen från [!DNL Real-Time CDP].

## Identiteter som stöds {#supported-identities}

Adobe Advertising DSP-målet stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | E-postadresser som hashas med SHA256-algoritmen | Experience Platform har stöd för både oformaterad text och SHA256-hashade e-postadresser. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att Experience Platform automatiskt hash-kodar data vid aktiveringen. |
| `ECID` | Första part-cookie för Experience Cloud | Krävs för att skapa cookie-baserade segment. |
| `adcloud` | Tredjeparts-cookie för Adobe Advertising | Krävs för att skapa cookie-baserade segment. |
| `GAID` | [!DNL Android] enhets-ID | Krävs för [!DNL Android] enheter som mål. |
| `IDFA` | [!DNL iOS] enhets-ID | Krävs för [!DNL iOS] enheter som mål. |

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
| -------------------- | --------- | ----------- | --------- |
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data lagrade i datasjön [!DNL Adobe Experience Platform]. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

I följande tabell finns information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
| ---- | ---- | ----- |
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de valda identifierarna. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. När en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions) för Experience Platform. Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till målet följer du instruktionerna för att [skapa en målanslutning](/help/destinations/ui/connect-destination.md) med Experience Platform användargränssnitt. I arbetsflödet för målkonfiguration fyller du i fälten som anges i underavsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill ansluta till målet anger du följande parameter i avsnittet [!UICONTROL Connection type] och väljer sedan **[!UICONTROL Connect to destination]**:

* **[!UICONTROL Account or Advertiser Key]**: [!UICONTROL Source Key] genereras när en [[!DNL Real-Time CDP] källa skapas i DSP-användargränssnittet](https://experienceleague.adobe.com/sv/docs/advertising/dsp/audiences/sources/source-manage). Ditt Adobe-kontoteam delar nyckeln med dig när de har skapat källan.

![Skärmbild av avsnittet Anslutningstyp som visar fältet Konto eller Advertiser-nyckel.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

![Skärmbild av målinformationsfälten med indata för namn och beskrivning.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_adcloud_dsp"
>title="Förkonfigurerade mappningsuppsättningar"
>abstract="Vi har förkonfigurerat de här två mappningsuppsättningarna åt dig: ECID och [!DNL adcloud] cookie. När du aktiverar data till Adobe Advertising DSP måste profilerna som är kvalificerade för de aktiverade målgrupperna ha minst en ECID-identitet kopplad till sin profil för att kunna exporteras till målet."
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/advertising/adobe-advertising-cloud-connection#preconfigured-mappings" text="Läs mer om förkonfigurerade mappningar"

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera identiteter måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa attribut och identiteter {#map}

Identitetsmappningarna för det här målet är delvis förkonfigurerade. Granska de förkonfigurerade mappningarna nedan och lägg till valfria identiteter som du vill inkludera.

### Förkonfigurerade mappningar {#preconfigured-mappings}

Följande identitetsmappningar är **förkonfigurerade och fyllda i automatiskt** under målgruppsaktiveringen:

* **`ECID`** (Experience Cloud-ID)
* **`adcloud`** (Adobe Advertising cookie från tredje part)

![Skärmbild av avsnittet för identitetsmappning som visar cookie-identifierare, hashed-e-post, IDFA och GAID-alternativ.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

De här mappningarna är nedtonade och skrivskyddade. Du behöver inte konfigurera något i det här steget. Du kan också lägga till följande mappningar:

* **`email_lc_sha256`** (hash-kodad e-post)
* **IDFA** ([!DNL Apple iOS] enhets-ID)
* **GAID** ([!DNL Android] enhets-ID)

Välj **[!UICONTROL Next]** om du vill fortsätta.

>[!IMPORTANT]
>
>**ECID krävs för att cookie-baserad export ska lyckas.** profiler utan ECID inkluderas inte i cookie-baserade segment. För autentiserade målgruppssegment som använder [!DNL RampID] eller [!DNL UID2.0] måste profilerna innehålla hash-kodade e-post-ID:n.

Instruktioner finns i [Mappa attribut och identiteter](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

## Validera dataexport {#exported-data}

Kontrollera följande om du vill verifiera att målgruppsdata delats med Adobe Advertising:

* Dataflödet i [!DNL Real-Time CDP]-målet har slutförts.

* I DSP är målgruppen tillgänglig när du skapar eller redigerar en målgrupp från **[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]** eller från avsnittet **[!UICONTROL Audience Targeting]** i placeringsinställningarna. Publiken ska vara synlig på fliken [!UICONTROL Adobe Segments] under mappen [!UICONTROL Real-Time CDP].

![Skärmbild av DSP Audiences-gränssnittet som visar en [!DNL Real-Time CDP]-mapp med importerade målgruppssegment som listas under fliken Adobe-segment.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).
