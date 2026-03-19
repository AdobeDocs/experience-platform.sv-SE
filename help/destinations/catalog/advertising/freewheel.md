---
title: FreeWheel-anslutning
description: Lär dig hur du aktiverar målgrupper från Adobe Experience Platform till FreeWheel för programmatisk annonsering i uppkopplade TV-, display- och videolager.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
source-git-commit: 081832228c2aea6b436cce66a7e9623c5b79d62d
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 1%

---

# [!DNL FreeWheel]-anslutning {#freewheel}

>[!AVAILABILITY]
>
>Målet [!DNL FreeWheel] finns för närvarande i Beta och är endast tillgängligt för vissa kunder. Kontakta din Adobe-representant om du vill få åtkomst.

## Översikt {#overview}

[!DNL FreeWheel] är en global reklamteknikplattform som driver programmatiska inköp och försäljning över uppkopplad TV (CTV), video och displayannonslager. [!DNL FreeWheel] är en datadriven marknadsplats som kopplar samman annonsörer med medieägare världen över.

Använd det här målet om du vill skicka målgrupper från Adobe Experience Platform till [!DNL FreeWheel]. Målgrupper levereras som dagliga gruppfiler och är tillgängliga för målinriktning i [!DNL FreeWheel] erbjudanden och kampanjer.

## Förutsättningar {#prerequisites}

Läs följande krav innan du kan aktivera målgrupper för [!DNL FreeWheel]:

* **FreeWheel-nätverks-ID**: Du måste ha ett giltigt [!DNL FreeWheel] nätverks-ID. Detta tillhandahålls av [!DNL FreeWheel] när ditt konto är konfigurerat.

## Identiteter som stöds {#supported-identities}

[!DNL FreeWheel] stöder aktivering av identiteter som beskrivs i tabellen nedan. Förutom dessa identiteter kan du använda alla identiteter som är tillgängliga i ditt [!DNL FreeWheel]-konto. Se [Mappa attribut och identiteter](#map) för instruktioner om hur du mappar en identitet som inte finns i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `idfa` | Apple ID för annonsörer | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| `aaid` | ANDROID ADVERTISING ID | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| `ctv` | Ansluten tv-enhets-ID | Välj den här målidentiteten när du riktar dig till CTV-enheter. |
| `ip` | IPv4-adress | Välj den här målidentiteten för målanvändare baserat på deras IP-adress. Mappa ett profilattribut som innehåller en giltig IPv4-adress eller använd ett beräkningsfält för att härleda värdet. |
| `ipv6` | IPv6-adress | Välj den här målidentiteten för målanvändare baserat på deras IPv6-adress. Mappa ett profilattribut som innehåller en giltig IPv6-adress, eller använd ett beräkningsfält för att härleda värdet. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Ja | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li>anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li>lookalike-målgrupper,</li><li>federerade målgrupper,</li><li>målgrupper som genererats i andra Experience Platform-appar som Adobe Journey Optimizer,</li><li>med mera.</li></ul> |

{style="table-layout:auto"}

Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Omdirigering av CTV, hämmande av räckvidd |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data som lagras i Adobe Experience Platform Data Lake. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i en målgrupp tillsammans med de önskade identitetsfälten som valts i mappningssteget i [målaktiveringsarbetsflödet](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Den första exporten är en fullständig ögonblicksbild av alla profiler som är kvalificerade för de aktiverade målgrupperna. Efterföljande exporter är dagliga stegvisa uppdateringar som inkluderar nya målgruppskvalifikationer (tillägg) och målgruppsavslutningar (borttagningar). Det finns också ett konfigurerbart uppdateringsintervall (4, 8 eller 12 veckor) som kan aktivera periodisk fullexport utöver de dagliga stegvisa ökningarna. Fullständig export innehåller endast aktuella profiler. Publiken finns inte med och levereras exklusivt via de dagliga stegvisa uppdateringarna. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Autentisering till målet [!DNL FreeWheel] hanteras automatiskt av Adobe. Du behöver inga autentiseringsuppgifter eller API-nycklar under autentiseringen. Adobe hanterar den säkra anslutningen till [!DNL FreeWheel] åt dig.

![Skärmbild av autentiseringssteget för FreeWheel-målet.](../../assets/catalog/advertising/freewheel/connect-destination.png)

Välj **[!UICONTROL Connect to destination]** om du vill fortsätta till steget för målinformation.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_freewheel_backfill"
>title="Fullständigt intervall för målgruppsuppdatering"
>abstract="Välj det intervall med vilket en fullständig målgruppsexport skickas till [!DNL FreeWheel] förutom dagliga inkrementella uppdateringar. En export med fullständig målgrupp hindrar målgruppsmedlemmarna från att förfalla om [!DNL FreeWheel], så att ni inte drabbas av bortfall hos målmedlemmar när kampanjer körs. Tillgängliga alternativ är fyra veckor, åtta veckor och tolv veckor."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Exempelbild som visar hur du fyller i detaljer för FreeWheel-målet.](../../assets/catalog/advertising/freewheel/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Region]**: Regionen [!DNL FreeWheel] där ditt konto finns. Välj något av följande alternativ:
   * **[!UICONTROL US East]**
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Asia Pacific]**
* **[!UICONTROL FreeWheel network ID]**: Ditt [!DNL FreeWheel] nätverks-ID. Det här värdet tillhandahålls av [!DNL FreeWheel] och identifierar din organisation unikt i plattformen [!DNL FreeWheel].
* **[!UICONTROL Full audience refresh interval]**: Den frekvens med vilken en fullständig målgruppsexport skickas till [!DNL FreeWheel] förutom dagliga stegvisa uppdateringar. En export med fullständig målgrupp hindrar målgruppsmedlemmarna från att förfalla om [!DNL FreeWheel], så att ni inte drabbas av bortfall hos målmedlemmar när kampanjer körs. Välj ett intervall i listrutan.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till det här målet.

### Schemalägg målgruppsexporter {#schedule}

![Skärmbild av schemaläggningssteget i FreeWheel-aktiveringsarbetsflödet.](../../assets/catalog/advertising/freewheel/scheduling.png)

Konfigurera exportschemat för varje målgrupp i steget **[!UICONTROL Scheduling]**. [!DNL FreeWheel] använder en hybridexportmodell: den första exporten för varje aktiverad målgrupp är en fullständig ögonblicksbild, följt av dagliga stegvisa uppdateringar.

Konfigurera följande fält:

* **[!UICONTROL File export options]**: **[!UICONTROL Export incremental files]** är förmarkerat och är det enda alternativ som stöds. Den första exporten innehåller automatiskt en fullständig ögonblicksbild av alla kvalificerade profiler. Efterföljande exporter ger endast nya målgruppskvalifikationer och utgångar sedan den senaste exporten.
* **[!UICONTROL Frequency]**: Välj **[!UICONTROL Daily]**. [!DNL FreeWheel] förväntar sig daglig inkrementell filleverans.
* **[!UICONTROL Scheduled start time]**: Ange den tid i UTC som den dagliga exporten ska köras vid.
* **[!UICONTROL Date]**: Ange start- och slutdatum för aktiveringen. Startdatumet avgör när den första fullständiga ögonblicksbildsexporten skickas.

>[!NOTE]
>
>Fullständig export (både den inledande ögonblicksbilden och periodiska fullständiga uppdateringar) innehåller endast aktuella kvalificerade profiler. Målgruppsutgångar ingår inte i den fullständiga exporten och levereras endast via de dagliga stegvisa uppdateringarna.

### Mappa attribut och identiteter {#map}

I mappningssteget väljer du källfälten från dina Experience Platform-profiler och mappar dem till de identitetstyper som stöds av [!DNL FreeWheel]. Minst en mappning krävs.

>[!IMPORTANT]
>
>Identitetstyperna som stöds av [!DNL FreeWheel] visas som **målattribut** i mappningsgränssnittet, inte som identitetsnamnutrymmen.

Om ditt [!DNL FreeWheel]-konto har stöd för identitetstyper som inte finns med i tabellen [identiteter som stöds](#supported-identities) kan du mappa till dem genom att ange identitetsnamnet manuellt i målfältet i stället för att välja från den fördefinierade listan.

![Skärmbild med ett anpassat identitetsnamn som skrivs direkt i målfältet i mappningssteget.](../../assets/catalog/advertising/freewheel/custom-identity.png)

Följande är exempelmappningar. De faktiska mappningarna beror på ditt profilschema och de identitetstyper som ditt [!DNL FreeWheel]-konto stöder.

| Source | Målfält |
| --- | --- |
| `identityMap.IDFA` | `idfa` |
| `identityMap.GAID` | `aaid` |
| `homeAddress.ipAddress` | `ip` |

{style="table-layout:auto"}

>[!NOTE]
>
>Inga obligatoriska mappningar används. Profiler utan minst en giltig identitetsmappning inkluderas dock inte i de exporterade filerna.

## Exporterade data/Validera dataexport {#exported-data}

[!DNL FreeWheel] tar emot två typer av filer per export. Båda filtyperna genereras och levereras automatiskt. Du behöver inte göra något.

**Identitetsfiler (data)** innehåller data om målgruppsmedlemskap. Varje rad mappar en användaridentifierare till ett eller flera målgrupps-ID:n. Filerna levereras till [!DNL FreeWheel] i CSV-format utan kolumnrubriker. Separata filer skapas för varje identitetstyp som finns i exporten (till exempel en fil för `aaid` och en separat fil för `idfa`).

Exempel på datafilformat:

```csv
aebc1234-56f7-89ab-cdef-0123456789ab,segment_1,segment_2
f7c9a8b0-4d33-11ec-81d3-0242ac130003,segment_1,segment_3
123e4567-e89b-12d3-a456-426614174000,segment_2
```

**Taxonomifiler** beskriver målgrupperna som ingår i exporten. Dessa filer levereras tillsammans med datafilerna och innehåller målgrupps-ID, namn och TTL (time to live) i dagar. Den maximala TTL som stöds av [!DNL FreeWheel] är 90 dagar. Värdena i exemplet nedan är illustrativa.

Exempel på taxonomifilformat:

```csv
Segment ID,Segment Name,TTL
segment_1,my_first_segment,30
segment_2,my_second_segment,30
segment_3,my_third_segment,30
```

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Mer information om [!DNL FreeWheel] och dess annonseringsteknologiplattform finns på webbplatsen [FreeWheel](https://www.freewheel.com){target="_blank"}.
