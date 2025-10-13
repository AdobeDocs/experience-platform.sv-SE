---
title: Anpassa
description: Adform är en ledande leverantör av programmatiska mediainköp och säljlösningar. Genom att ansluta Adform till Adobe Experience Platform kan du aktivera dina första målgrupper via Adform baserat på Experience Cloud ID (ECID).
source-git-commit: 823b2142366ac218ad93279de5f31d60bdc07bbf
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---


# Anpassa anslutning {#adform}

## Översikt {#overview}

Adform är en ledande leverantör av programmatiska mediainköp och säljlösningar. Genom att ansluta Adform till Adobe Experience Platform kan du aktivera dina första målgrupper via Adform baserat på Experience Cloud ID (ECID).

>[!IMPORTANT]
>
>Målanslutnings- och dokumentationssidan skapas och underhålls av Adform team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på `support@adform.com`.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda Adform-målet finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Aktivera Adobe Real-Time CDP {#use-case-1}

Använd det här målet för att skicka Adobe Real-Time CDP-målgrupper till Adform för aktivering baserat på Experience Cloud ID (ECID) och Adforms ID Fusion. Adforms ID Fusion är Adforms ID-matchningstjänst som gör att du kan aktivera dina första målgrupper baserat på Experience Cloud ID (ECID).

Ett vanligt fall är omdirigering av webbplatsbesökare till din webbplats eller app baserat på Experience Cloud-id (ECID). Allt du behöver göra är att skicka Experience Cloud ID (ECID) till Adform via de [Event Streaming](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) eller [Adform Extensions på klientsidan](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/analytics/adform) som är tillgängliga. Efter det kan du dela målgrupper med Adobe via Adform-målet för aktivering - enbart baserat på Experience Cloud ID (ECID).

## Förhandskrav {#prerequisites}

* Du måste vara en befintlig Adobe-kund för att kunna använda den här destinationen.
* Du måste ha autentiseringsuppgifterna för Adform Audience Base Data Connection.
   * Om du inte har autentiseringsuppgifter för Adform Audience Base Data Connection kontaktar du din Adobe-representant.
* För att synkroniseringen ska fungera på rätt sätt måste du antingen ha en [händelsedirektuppspelning](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) eller [klientanslutning](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/analytics/adform) från dina enheter till Adform Site Tracking.
   * Om du inte har någon händelsedirektuppspelning eller klientanslutning från dina enheter till Adform Site Tracking kontaktar du din Adobe-representant.
   * Adform innehåller Adobe Experience Cloud-tillägg för både [händelsedirektuppspelning](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) och [klientsidan](https://experienceleague.adobe.com/sv/docs/experience-platform/destinations/catalog/analytics/adform).


## Identiteter som stöds {#supported-identities}

Adform stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| ECID | EXPERIENCE CLOUD ID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras av följande alias:&quot;Adobe Marketing Cloud ID&quot;,&quot;Adobe Experience Cloud ID&quot;,&quot;Adobe Experience Platform ID&quot;. Mer information finns i följande dokument på [ECID](/help/identity-service/features/ecid.md). |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med identifierarna (namn, telefonnummer eller andra) som används i målet *YourDestination*. |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

![Autentisera till målet](../../assets/catalog/advertising/adform/authenticate-destination.png)

* **[!UICONTROL Account name]**: Ange ett kontonamn som du kan använda för att identifiera den här målanslutningen i framtiden.
* **[!UICONTROL S3 Access Key ID]**: Fyll i S3-åtkomstnyckeln från Adform.
* **[!UICONTROL S3 Secret Access Key]**: Fyll i den S3-hemliga åtkomstnyckeln som tillhandahålls av Adform.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Fyll i målinformationen](../../assets/catalog/advertising/adform/configure-destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Provider Name]**: Ditt Adform-kontonamn tillhandahålls av Adform.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

* **ECID** (Experience Cloud-ID)

Använd bara målidentitetsmappningen [!DNL ECID] under mappningssteget. Inkludera inga andra identitetsfält eftersom aktiveringen då inte kan slutföras.

## Exporterade data/Validera dataexport {#exported-data}

Målkopplingen exporterar endast ECID-identiteten till målet. Ingen annan identitet exporteras. Om du vill kontrollera om dataexporten lyckades loggar du in på ditt Adform Audience Base-konto och kontrollerar om målgrupperna är tillgängliga.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Mer information om Adform Audience Base finns i [Adform Audience Base-dokumentationen](https://www.adformhelp.com/hc/en-us/categories/9738365991697-Data-Management-Platform).