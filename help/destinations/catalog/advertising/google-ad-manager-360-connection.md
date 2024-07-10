---
title: (Beta) [!DNL Google Ad Manager 360] anslutning
description: Google Ad Manager 360 är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 0%

---

# (Beta) [!DNL Google Ad Manager 360] anslutning

>[!IMPORTANT]
>
> Google släpper ändringar i [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Kundmatchning](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)och [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) för att stödja de krav på efterlevnad och samtycke som anges i [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) i Europeiska unionen ([Policy för EU-användarsamtycke](https://www.google.com/about/company/user-consent-policy/)). Tvingande av dessa ändringar av medgivandekraven gäller från och med den 6 mars 2024.
><br/>
>För att kunna följa EU:s policy för användargodkännande och fortsätta att skapa målgruppslistor för användare i Europeiska ekonomiska samarbetsområdet (EES) måste annonsörer och partners se till att slutanvändarnas samtycke skickas när målgruppsdata överförs. Som Google-partner tillhandahåller Adobe de verktyg som krävs för att uppfylla dessa krav på medgivande enligt DMA i Europeiska unionen.
><br/>
>Kunder som har köpt skölden för skydd och säkerhet av Adobe och konfigurerat en [samtyckespolicy](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) om du vill filtrera bort profiler som inte är godkända behöver du inte göra något.
><br/>
>Kunder som inte har köpt Adobe Privacy &amp; Security Shield måste använda [segmentdefinition](../../../segmentation/home.md#segment-definitions) funktioner inom [Segment Builder](../../../segmentation/ui/segment-builder.md) för att filtrera bort profiler som inte godkänts, så att du kan fortsätta använda de befintliga Real-Time CDP Google-måltiderna utan avbrott.

The [!DNL Google Ad Manager 360] anslutning aktiverar batchöverföring för [!DNL publisher provided identifiers] (PPID) till [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Mer information om hur utgivarens identifierare fungerar i Google Ad Manager 360 finns i [officiell Google-dokumentation](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Den här destinationen finns för närvarande i Beta och är endast tillgänglig för ett begränsat antal kunder. Om du vill begära åtkomst till [!DNL Google Ad Manager 360] kontakta din Adobe-representant och uppge [!DNL organization ID].

The [!DNL Google Ad Manager 360] destinationsexport [!DNL CSV] filer till [!DNL Google Cloud Storage] bucket. När du har exporterat [!DNL CSV] -filer måste du importera dem till [!DNL Google Ad Manager 360] konto.

## Destinationsspecifikationer {#specifics}

Observera följande information som gäller [!DNL Google Ad Manager 360] destinationer.

* Aktiverade målgrupper skapas programmatiskt i Google-plattformen och fylls i i CSV-filen.

## Identiteter som stöds {#supported-identities}

[!DNL This integration] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Välj den här målidentiteten för att skicka målgrupper till [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med tillämpliga schemafält (till exempel ditt PPID), som du väljer på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Förhandskrav {#prerequisites}

### Tillåt listning {#allow-listing}

Du måste ange Tillåt innan du konfigurerar din första [!DNL Google Ad Manager 360] mål i Platform. Se till att du slutför processen för att tillåta listning som beskrivs nedan innan du skapar ditt mål.

>[!NOTE]
>
>Undantaget till den här regeln gäller för befintlig [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) kunder. Om du redan har skapat en anslutning till det här Google-målet i Audience Manager behöver du inte gå igenom processen för att tillåta listning igen och du kan fortsätta till nästa steg.

1. Följ stegen som beskrivs i [Dokumentation för Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) att lägga till Adobe som en länkad datahanteringsplattform (DMP).
2. I [!DNL Google Ad Manager] gränssnitt, gå till **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** och aktivera **[!UICONTROL API Access]** skjutreglage.


## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Access key ID]**: En alfanumerisk sträng på 61 tecken som används för att autentisera [!DNL Google Cloud Storage] konto till plattform.
* **[!UICONTROL Secret access key]**: En 40-tecken, base64-kodad sträng som används för att autentisera [!DNL Google Cloud Storage] konto till plattform.

Mer information om dessa värden finns i [Google Cloud Storage HMAC-nycklar](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guide. Anvisningar om hur du skapar ditt eget ID för åtkomstnyckel och hemlig åtkomstnyckel finns i [[!DNL Google Cloud Storage] källöversikt](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Bifoga målgrupps-ID till målgruppsnamn"
>abstract="Välj det här alternativet om målgruppsnamnet i det här målet ska innehålla målgrupps-ID:t från Experience Platform, så här: `Audience Name (Audience ID)`"

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL Bucket name]**: Ange namnet på [!DNL Google Cloud Storage] bucket som ska användas för detta mål.
* **[!UICONTROL Account ID]**: Ange [!DNL Audience Link ID] från [!DNL Google] konto. Detta är en specifik identifierare som är associerad med din [!DNL Google Ad Manager] nätverk (inte ditt [!DNL Network code]). Du hittar den här under **[!UICONTROL Admin > Global settings]** i [!DNL Google Ad Manager] gränssnitt.
* **[!UICONTROL Account Type]**: Välj ett alternativ, beroende på [!DNL Google] konto:
   * Använd `AdX buyer` for [!DNL Google AdX]
   * Använd `DFP by Google` for [!DNL DoubleClick] för utgivare
* **[!UICONTROL Append audience ID to audience name]**: Välj det här alternativet om du vill att målgruppsnamnet i Google Ad Manager 360 ska innehålla målgrupps-ID:t från Experience Platform: `Audience Name (Audience ID)`.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I steget för identitetsmappning ser du följande förifyllda mappningar:

| Mappning i förväg | Beskrivning |
|---------|----------|
| `ECID` -> `ppid` | Detta är den enda användaranpassade förifyllda mappningen. Du kan välja dina attribut eller identitetsnamnutrymmen från Platform och mappa dem till `ppid`. |
| `metadata.segment.alias` -> `list_id` | Mappar Experience Platform målgruppsnamn till målgrupps-ID:n i Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Anger Google när diskvalificerade användare ska tas bort från segment. |

Dessa mappningar krävs av [!DNL Google Ad Manager 360] och skapas automatiskt av Adobe Experience Platform för [!DNL Google Ad Manager 360] anslutningar.

![Användargränssnittsbild som visar mappningssteget för Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Exporterade data {#exported-data}

Kontrollera dina [!DNL Google Cloud Storage] och se till att de exporterade filerna innehåller de förväntade profilpopulationerna.

## Felsökning {#troubleshooting}

Om du råkar ut för några fel när du använder det här målet och behöver kontakta antingen Adobe eller Google, ska du ha följande ID:n till hands.

Följande är Adobe Google konto-ID:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775