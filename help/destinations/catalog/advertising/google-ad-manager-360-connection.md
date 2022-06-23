---
title: (Beta) [!DNL Google Ad Manager 360] anslutning
description: Google Ad Manager 360 är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# (Beta) [!DNL Google Ad Manager 360] anslutning

## Översikt {#overview}

The [!DNL Google Ad Manager 360] anslutning aktiverar batchöverföring för [!DNL publisher provided identifiers] (PPID) till [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Mer information om hur utgivarens identifierare fungerar i Google Ad Manager 360 finns i [officiell Google-dokumentation](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Den här destinationen finns för närvarande i betaversionen och är endast tillgänglig för ett begränsat antal kunder. Om du vill begära åtkomst till [!DNL Google Ad Manager 360] kontakta din Adobe-representant och uppge [!DNL IMS Organization ID].

The [!DNL Google Ad Manager 360] destinationsexport [!DNL CSV] filer till [!DNL Google Cloud Storage] bucket. När du har exporterat [!DNL CSV] -filer måste du importera dem till [!DNL Google Ad Manager 360] konto.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Ad Manager 360] destinationer.

* Aktiverade målgrupper skapas programmatiskt i Google-plattformen och fylls i i CSV-filen.

## Identiteter som stöds {#supported-identities}

[!DNL This integration] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Välj den här målidentiteten för att skicka målgrupper till [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Förutsättningar {#prerequisites}

### Tillåt listning {#allow-listing}

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar din första [!DNL Google Ad Manager] mål i Platform. Se till att tillåtelselista-processen som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ad Manager 360] mål i plattform måste du kontakta [!DNL Google] för att Adobe ska föras upp på listan över tillåtna dataleverantörer och för att ditt konto ska läggas till tillåtelselista. Kontakt [!DNL Google] och lämna följande information:

* **Konto-ID**: Adobe konto-ID hos Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID hos Google. Kund-ID: 89690775.
* **Nätverks-ID**: det här är ditt konto med [!DNL Google Ad Manager]
* **Målgruppslänks-ID**: det här är ditt konto med [!DNL Google Ad Manager]
* Din kontotyp. DFP av Google eller AdX-köpare.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Bucket name]**: ange namnet på [!DNL Google Cloud Storage] bucket som ska användas för detta mål.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

I steget för identitetsmappning ser du följande förifyllda mappningar:

| Mappning i förväg | Beskrivning |
|---------|----------|
| `ECID` -> `ppid` | Detta är den enda användaranpassade förifyllda mappningen. Du kan välja dina attribut eller identitetsnamnutrymmen från Platform och mappa dem till `ppid`. |
| `metadata.segment.alias` -> `list_id` | Mappar Experience Platform-segmentnamn till segment-ID i Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Anger Google när diskvalificerade användare ska tas bort från segment. |

Dessa mappningar krävs av [!DNL Google Ad Manager 360] och skapas automatiskt av Adobe Experience Platform för alla [!DNL Google Ad Manager 360] anslutningar.

![Användargränssnittsbild som visar mappningssteget för Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Exporterade data {#exported-data}

Kontrollera dina [!DNL Google Cloud Storage] och se till att de exporterade filerna innehåller de förväntade profilpopulationerna.
