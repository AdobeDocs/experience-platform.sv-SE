---
title: (Beta) [!DNL Google Ad Manager 360] anslutning
description: Google Ad Manager 360 är en annonseringsplattform från Google som ger utgivare möjlighet att hantera annonser på sina webbplatser, via video och i mobilappar.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: f163b1e3c60953192b2ddf543eb4f3e8df88799b
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

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
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med tillämpliga schemafält (till exempel ditt PPID), som du väljer på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Förutsättningar {#prerequisites}

### Tillåt listning {#allow-listing}

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar din första [!DNL Google Ad Manager] mål i Platform. Se till att tillåtelselista-processen som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.

>[!IMPORTANT]
>
>Google har förenklat processen att ansluta externa målgruppshanteringsplattformar till Google Ad Manager 360. Nu kan du gå igenom processen för att länka till Google Ad Manager 360 på ett självbetjäningssätt. Läs [Segment från datahanteringsplattformar](https://support.google.com/admanager/answer/3289669?hl=en) i Google-dokumentationen. Du bör ha ID:n listade nedan till hands.

* **Konto-ID**: Adobe konto-ID hos Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID hos Google. Kund-ID: 89690775.
* **Nätverkskod**: Det här är din [!DNL Google Ad Manager] nätverksidentifierare, hittades under **[!UICONTROL Admin > Global settings]** i Google-gränssnittet och i URL-adressen.
* **Målgruppslänks-ID**: Detta är en specifik identifierare som är associerad med din [!DNL Google Ad Manager] nätverk (inte ditt [!DNL Network code]), som också finns under **[!UICONTROL Admin > Global settings]** i Google gränssnitt.
* Din kontotyp. DFP av Google eller AdX-köpare.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Access key ID]**: En 61-siffrig alfanumerisk sträng som används för att autentisera [!DNL Google Cloud Storage] konto till plattform.
* **[!UICONTROL Secret access key]**: En 40-siffrig, base-64-kodad sträng som används för att autentisera [!DNL Google Cloud Storage] konto till plattform.

Mer information om dessa värden finns i [Google Cloud Storage HMAC-nycklar](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guide. Anvisningar om hur du skapar ditt eget ID för åtkomstnyckel och hemlig åtkomstnyckel finns i [[!DNL Google Cloud Storage] källöversikt](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Bucket name]**: Ange namnet på [!DNL Google Cloud Storage] bucket som ska användas för detta mål.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL Account ID]**: Fyll i ditt Audience Link ID med [!DNL Google].
* **[!UICONTROL Account Type]**: Välj ett alternativ beroende på ditt konto hos Google:
   * Använd `DFP by Google` for [!DNL DoubleClick] för utgivare
   * Använd `AdX buyer` for [!DNL Google AdX]

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

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
