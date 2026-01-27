---
title: Indexutbyte
description: Anslut till Index Exchange (Index) och aktivera data så att målgruppssegmenten kan hanteras av avtal som skapas i Index-gränssnittet.
source-git-commit: 4ecd3b60a6b45a94285785049fd4dee99d7c9bdf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---


# [!DNL Index Exchange] {#index-exchange}

## Översikt {#overview}

[!DNL Index] är en global plattform för annonsleveranser som hjälper mediekonstruktörer att maximera värdet av sitt innehåll på alla skärmar. Med över 20 års branschledarskap knyter [!DNL Index] samman världens största varumärken med förstklassiga upplevelsemakare för att leverera högkvalitativa kundupplevelser.

Använd den här målkopplingen om du vill exportera målgruppssegment från Adobe Experience Platform direkt till [!DNL Index Exchange]s programmatiska annonsplattform.

När dessa målgruppssegment har exporterats kan de användas för att rikta avtal mellan medieägare, marknadspartners eller utgivare eller delas med marknadsföringsleverantörer och kuratorer.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av [!DNL Index]-teamet. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på [technical_am_marketplace@indexexchange.com](mailto:technical_am_marketplace@indexexchange.com).

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Index Exchange] finns det exempel på användning som Experience Platform-kunder kan lösa genom att använda det här målet.

### Rikta användarna mot mobiler, webben och CTV-plattformar {#targeting-users}

Medieägare, marknadsplatspartners eller marknadsföringsleverantörer som vill skicka målgrupper från Experience Platform till [!DNL Index] för målanvändare på mobil-, webb- och CTV-plattformar med ett stort antal identifierare.

### Skräddarsy specifikt innehåll på mobil-, webb- och CTV-plattformar {#targeting-content}

Medieägare, marknadsplatspartners eller marknadsplatsleverantörer som vill skicka målgrupper från Experience Platform till [!DNL Index] för att rikta in sig på användare som tittar på visst innehåll på olika mobil-, webb- och CTV-plattformar med hjälp av specifika URL:er, apppaket eller innehålls-ID:n.

## Förhandskrav {#prerequisites}

Målgruppssegment måste registreras hos [!DNL Index] med en extra process när det här målet används, innan de visas på ditt konto. Kontakta din [!DNL Index Exchange]-kontorepresentant om du behöver hjälp med den här processen.

## Identiteter som stöds {#supported-identities}

[!DNL Index] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

Observera att [!DNL Index Exchange] mål bara stöder en identitetstyp per överföring. Du måste ange lämplig identifierartyp när du konfigurerar målinformationen (se avsnittet [&quot;Fyll i målinformation&quot;](#destination-details) nedan).

Om du vill överföra flera identitetstyper skapar du separata instanser av målet [!DNL Index Exchange] för varje identitetstyp.

| Målidentitet | Beskrivning | Överväganden |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | Om källidentiteten är ett GAID-namnutrymme väljer du GAID som målidentitet. |
| IDFA | Apple ID för annonsörer | Om din källidentitet är ett IDFA-namnutrymme väljer du IDFA-målidentitet. |
| Windows AID | Windows Advertising ID | Om källidentiteten är ett Windows AID-namnområde väljer du Windows AID-målidentiteten. |
| extern_id | Anpassade användar-ID:n | Om källidentiteten är ett anpassat namnutrymme väljer du den här målidentiteten. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet förklaras vilka målgruppstyper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
| --------- | ---------- | --------- | 
| Exporttyp | **[!UICONTROL Segment export]** | Exporterar alla medlemmar i ett segment (publik) med identifierarna (IDFA, GAID eller andra) som används i målet [!DNL Index Exchange]. |
| Exportfrekvens | **[!UICONTROL Batch]** | Exporterar filer till underordnade plattformar med intervallen 3, 6, 8, 12 eller 24 timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Målinformation](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name]: Ange ett namn som hjälper dig att identifiera det här målet senare.
* [!UICONTROL Description]: Ange en beskrivning som hjälper dig att identifiera det här målet senare.
* [!UICONTROL Identifier Type]: Välj den identifierartyp som tillhandahålls av index och som matchar den identifierare som du skickar till [!DNL Index]. Se tabellen med identifierartyper som stöds nedan. Om du är osäker på vilken identifierartyp som ska användas kontaktar du [!DNL Index]-representanten. Om du vill skicka flera identifierartyper skapar du separata instanser av det här målet.
* [!UICONTROL Account ID]: Ange ditt konto-ID för [!DNL Index]. Detta är inte detsamma som ditt utgivar-ID. Kontakta din [!DNL Index]-representant om du är osäker på vilket ID du ska använda.

#### Identifierartyper som stöds

| Identifierartyp | Beskrivning |
|------------------ | ------------- |
| [!DNL appbundle] | Mobile App Bundle |
| [!DNL contentid] | Innehålls-ID |
| [!DNL deviceid] | Enhets-ID (t.ex. IDFA, GAID, WAID osv.) |
| [!DNL ip] | IP-adress |
| [!DNL postcode] | Postnummer |
| [!DNL url] | Webbplats-URL |
| [!DNL ppid_xxx] | Kontakta din [!DNL Index Exchange]-kontorepresentant om du behöver hjälp med PPID-identifierare. |

{style="table-layout:auto"}

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om status för dataflödet till det här målet. Välj en eller flera aviseringar i listan om du vill prenumerera på statusmeddelanden för ditt dataflöde. Mer information finns i guiden om att [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).
Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Välja källfält:

* Välj en identifierare (vanligtvis namnutrymmen som IDFA eller ett anpassat ID-namnutrymme). Detta måste motsvara den identifierartyp som valts när målet konfigureras. Om du till exempel använder IDFA-identifierare som källfält måste målet ha ställts in med identifierartypen &quot;deviceid&quot;.

Markera målfält:

* Namn på målfält ignoreras och är inte viktiga. Målet bryr sig bara om vilken typ av identifierare som skickas, vilket bestäms av den identifierartyp som valts när målet konfigureras.

![Mappa attribut och identiteter](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### Registrera segment med [!DNL Index] {#register-segments}

Kontakta din [!DNL Index]-representant för att registrera de segment som du vill aktivera innan eller efter att du har aktiverat data till målet. Din representant kommer att ge anvisningar om hur du registrerar ytterligare segmentdetaljer, inklusive namn, ID, beskrivningar och priser, om tillämpligt.

## Exporterade data/Validera dataexport {#exported-data}

När registreringen är klar är segmenten tillgängliga för målinriktning i ditt [!DNL Index]-konto. Om du vill bekräfta att data tas emot på rätt sätt kontaktar du [!DNL Index]-representanten som kan ge information om den mängd segmentdata som tas emot.

## Dataanvändning och styrning {#data-usage-governance}

Alla Experience Platform-destinationer följer dataanvändningsprinciper när data hanteras. Mer information om hur Experience Platform använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
